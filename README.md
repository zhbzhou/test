#!/bin/bash

# ============================================
# Tizen OpenGL/EGL CTS 测试运行脚本 (带自动重跑功能)
# ============================================

SCRIPT_DIR=$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)
RESULT_DIR="${SCRIPT_DIR}/test_results"
TIMESTAMP=$(date +%Y%m%d_%H%M%S)

declare -A SUITE_TOTAL_CASES
mkdir -p "${RESULT_DIR}/qpa" "${RESULT_DIR}/csv" "${RESULT_DIR}/logs"

# 配置区
WAYLAND_DISPLAY="wayland-0"
GROUP_COUNT=50
DEVICE_TEMP_DIR="/tmp/cts_temp"
DEVICE_QPA_DIR="/opt/media/USBDriveA1"

TEST_SUITES=(
    "egl-main-2020-03-01.txt:deqp-egl:egl"
)

# 环境初始化
sdb shell "mkdir -p ${DEVICE_TEMP_DIR} ${DEVICE_QPA_DIR}"

for suite_config in "${TEST_SUITES[@]}"; do
    IFS=':' read -r case_file binary_name suite_name <<< "$suite_config"
    CASE_PATH="${SCRIPT_DIR}/android/cts/main/${case_file}"
    [ ! -f "$CASE_PATH" ] && continue

    # 提取所有有效用例到临时数组
    mapfile -t ALL_CASES < <(grep -vE '^(#|[[:space:]]*$)' "$CASE_PATH")
    actual_total=${#ALL_CASES[@]}
    
    echo "--- 套件: ${suite_name} (总计: ${actual_total}) ---"
    
    # 分组计算
    cases_per_group=$(( (actual_total + GROUP_COUNT - 1) / GROUP_COUNT ))
    
    for ((i=0; i<GROUP_COUNT; i++)); do
        start_idx=$(( i * cases_per_group ))
        [ "$start_idx" -ge "$actual_total" ] && break
        
        # 获取当前组的用例列表
        CURRENT_GROUP_CASES=("${ALL_CASES[@]:$start_idx:$cases_per_group}")
        group_size=${#CURRENT_GROUP_CASES[@]}
        
        local_txt="/tmp/group_${suite_name}_${i}.txt"
        printf "%s\n" "${CURRENT_GROUP_CASES[@]}" > "$local_txt"
        
        # --- 第一次尝试 ---
        echo "运行组 $i/$GROUP_COUNT (用例: $group_size)..."
        sdb push "$local_txt" "${DEVICE_TEMP_DIR}/run.txt" > /dev/null
        
        run_cmd="su -c 'export XDG_RUNTIME_DIR=/run && export WAYLAND_DISPLAY=${WAYLAND_DISPLAY} && cd /usr/bin/VK-GL-CTS-1.4.5/modules/${suite_name} && cat ${DEVICE_TEMP_DIR}/run.txt | ./${binary_name} --deqp-stdin-caselist --deqp-log-filename=${DEVICE_QPA_DIR}/temp.qpa --deqp-surface-type=fbo'"
        
        output=$(sdb shell "$run_cmd" 2>&1)
        
        # 统计跑完的数量
        g_run=$(echo "$output" | grep -E "Passed:|Failed:|Not supported:" | awk '{sum+=$NF} END {print sum+0}')

        # --- 自动重跑逻辑 ---
        if [ "$g_run" -lt "$group_size" ]; then
            echo "  ⚠️ 检测到崩溃或中断 ($g_run/$group_size)。正在重跑剩余的 $((group_size - g_run)) 条用例..."
            
            # 提取剩余未跑的用例
            retry_txt="/tmp/retry_${suite_name}_${i}.txt"
            printf "%s\n" "${CURRENT_GROUP_CASES[@]:$g_run}" > "$retry_txt"
            sdb push "$retry_txt" "${DEVICE_TEMP_DIR}/run.txt" > /dev/null
            
            # 执行重跑 (将结果追加到 qpa，注意：deqp默认会覆盖，这里我们生成独立的retry.qpa)
            retry_output=$(sdb shell "$run_cmd" 2>&1)
            
            # 更新统计信息（简单合并两次运行的输出进行统计）
            g_run_retry=$(echo "$retry_output" | grep -E "Passed:|Failed:|Not supported:" | awk '{sum+=$NF} END {print sum+0}')
            echo "  ✅ 重跑完成，额外完成: $g_run_retry 条。"
            
            # 合并输出用于日志记录
            output="${output}\n--- RETRY LOG ---\n${retry_output}"
            
            # 尝试拉取重跑后的 QPA
            sdb pull "${DEVICE_QPA_DIR}/temp.qpa" "${RESULT_DIR}/qpa/${suite_name}_group_${i}_retry.qpa" >/dev/null 2>&1
        else
            sdb pull "${DEVICE_QPA_DIR}/temp.qpa" "${RESULT_DIR}/qpa/${suite_name}_group_${i}.qpa" >/dev/null 2>&1
        fi

        # 记录详细日志
        echo -e "$output" >> "${RESULT_DIR}/logs/${suite_name}_group_${i}.log"
        rm -f "$local_txt" "$retry_txt" 2>/dev/null
    done
done
