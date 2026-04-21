#!/bin/bash

# ============================================
# Tizen OpenGL/EGL CTS 测试运行脚本 (修复优化版)
# ============================================

SCRIPT_DIR=$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)
RESULT_DIR="${SCRIPT_DIR}/test_results"
TIMESTAMP=$(date +%Y%m%d_%H%M%S)

# 声明关联数组用于存储各套件总数
declare -A SUITE_TOTAL_CASES

# 创建结果目录
mkdir -p "${RESULT_DIR}/qpa" "${RESULT_DIR}/csv" "${RESULT_DIR}/logs"

# 配置区
WAYLAND_DISPLAY="wayland-0"
GROUP_COUNT=50  # 将测试用例分成多少组运行
DEVICE_TEMP_DIR="/tmp/cts_temp"
DEVICE_QPA_DIR="/opt/media/USBDriveA1" # 确保该目录在设备上存在且可写

# 测试套件配置：格式 "用例文件名:二进制文件名:套件简称"
TEST_SUITES=(
    "egl-main-2020-03-01.txt:deqp-egl:egl"
    #"gles2-main-2020-03-01.txt:deqp-gles2:gles2"
)

# 初始化全局统计
total_pass=0; total_fail=0; total_ns=0; total_err=0; total_run=0

echo "========================================"
echo "开始 CTS 测试: ${TIMESTAMP}"
echo "========================================"

# 环境检查
if ! command -v sdb > /dev/null 2>&1; then echo "错误: 未找到 sdb"; exit 1; fi
if ! sdb get-serialno > /dev/null 2>&1; then echo "错误: 设备未连接"; exit 1; fi

# 初始化设备环境
sdb shell "mkdir -p ${DEVICE_TEMP_DIR} ${DEVICE_QPA_DIR}"
sdb shell "rm -f ${DEVICE_TEMP_DIR}/*.txt ${DEVICE_QPA_DIR}/*.qpa"

for suite_config in "${TEST_SUITES[@]}"; do
    IFS=':' read -r case_file binary_name suite_name <<< "$suite_config"
    
    CASE_PATH="${SCRIPT_DIR}/android/cts/main/${case_file}"
    [ ! -f "$CASE_PATH" ] && echo "跳过: 未找到文件 $CASE_PATH" && continue

    # 统计该套件总行数（过滤注释和空行）
    actual_total=$(grep -vE '^(#|[[:space:]]*$)' "$CASE_PATH" | wc -l)
    SUITE_TOTAL_CASES[$suite_name]=$actual_total
    
    echo "--- 正在处理套件: ${suite_name} (共 ${actual_total} 条用例) ---"

    # 根据名称定位目录
    MODULE_DIR="modules/${suite_name}"
    DEBUG_LOG="${RESULT_DIR}/logs/debug_${suite_name}_${TIMESTAMP}.log"
    UNRUN_FILE="${RESULT_DIR}/logs/unrun_${suite_name}_${TIMESTAMP}.txt"
    > "$DEBUG_LOG"
    > "$UNRUN_FILE"

    # 局部统计重置
    s_pass=0; s_fail=0; s_ns=0; s_err=0; s_run=0

    # 分组计算逻辑
    cases_per_group=$(( (actual_total + GROUP_COUNT - 1) / GROUP_COUNT ))

    for ((i=0; i<GROUP_COUNT; i++)); do
        start_line=$(( i * cases_per_group + 1 ))
        [ "$start_line" -gt "$actual_total" ] && break
        
        local_group_file="/tmp/group_${suite_name}_${i}.txt"
        # 提取当前组用例
        grep -vE '^(#|[[:space:]]*$)' "$CASE_PATH" | sed -n "${start_line},+$((cases_per_group-1))p" > "$local_group_file"
        
        group_size=$(wc -l < "$local_group_file")
        [ "$group_size" -eq 0 ] && continue

        # 推送到设备
        target_txt="${DEVICE_TEMP_DIR}/run.txt"
        target_qpa="${DEVICE_QPA_DIR}/group_${i}.qpa"
        sdb push "$local_group_file" "$target_txt" > /dev/null

        echo "运行组 $i/$GROUP_COUNT (用例: $group_size)..."
        
        # 执行测试
        # 增加了 --deqp-surface-type=fbo 减少对屏幕依赖，增加稳定性
        output=$(sdb shell "su -c 'export XDG_RUNTIME_DIR=/run && export WAYLAND_DISPLAY=${WAYLAND_DISPLAY} && cd /usr/bin/VK-GL-CTS-1.4.5/${MODULE_DIR} && cat ${target_txt} | ./${binary_name} --deqp-stdin-caselist --deqp-log-filename=${target_qpa} --deqp-surface-type=fbo'" 2>&1)
        exit_code=$?

        # 结果解析
        g_pass=$(echo "$output" | grep -o "Passed: *[0-9]*" | awk '{print $NF}' || echo 0)
        g_fail=$(echo "$output" | grep -o "Failed: *[0-9]*" | awk '{print $NF}' || echo 0)
        g_ns=$(echo "$output" | grep -o "Not supported: *[0-9]*" | awk '{print $NF}' || echo 0)
        g_total=$((g_pass + g_fail + g_ns))

        # 检查是否崩溃或未跑完
        if [ "$g_total" -lt "$group_size" ]; then
            echo "  警告: 组 $i 异常 (跑完 $g_total/$group_size), 退出码 $exit_code"
            echo "[GROUP $i] Exit: $exit_code | Output: $output" >> "$DEBUG_LOG"
            # 记录未跑完的部分以便后续分析
            sed -n "$((g_total + 1)),\$p" "$local_group_file" >> "$UNRUN_FILE"
            ((s_err++))
        fi

        # 累加统计
        s_pass=$((s_pass + g_pass)); s_fail=$((s_fail + g_fail))
        s_ns=$((s_ns + g_ns)); s_run=$((s_run + g_total))

        # 拉取结果并清理
        sdb pull "$target_qpa" "${RESULT_DIR}/qpa/${suite_name}_group_${i}.qpa" >/dev/null 2>&1
        rm -f "$local_group_file"
    done

    # 汇总计算
    pass_rate="0.00"
    [ "$s_run" -gt 0 ] && pass_rate=$(awk -v p=$s_pass -v t=$s_run 'BEGIN {printf "%.2f", (p/t)*100}')

    # 生成套件 Summary
    SUMMARY="${RESULT_DIR}/summary_${suite_name}.txt"
    {
        echo "Suite: $suite_name"
        echo "Result: Pass:$s_pass, Fail:$s_fail, NS:$s_ns, Total_Run:$s_run, Groups_With_Errors:$s_err"
        echo "Pass Rate: $pass_rate%"
    } > "$SUMMARY"

    # 全局累加
    total_pass=$((total_pass + s_pass)); total_fail=$((total_fail + s_fail))
    total_ns=$((total_ns + s_ns)); total_run=$((total_run + s_run))

    echo "套件 ${suite_name} 完成. 通过率: ${pass_rate}%"
    echo ""
done

echo "========================================"
echo "全部测试完成!"
echo "总运行数: $total_run | 总通过: $total_pass | 总失败: $total_fail"
echo "报告目录: ${RESULT_DIR}"
echo "========================================"
