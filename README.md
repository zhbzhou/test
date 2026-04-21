# ============================================
# 测试收尾：生成报告与 CSV 转换
# ============================================

echo "----------------------------------------"
echo "正在生成最终测试报告..."
echo "----------------------------------------"

# 遍历每个测试套件
for suite_config in "${TEST_SUITES[@]}"; do
    IFS=':' read -r case_file binary_name suite_name <<< "$suite_config"
    
    SUITE_QPA_DIR="${RESULT_DIR}/qpa"
    SUITE_CSV_DIR="${RESULT_DIR}/csv"
    FINAL_SUMMARY="${RESULT_DIR}/summary_${suite_name}_${TIMESTAMP}.txt"
    
    # 1. 汇总所有统计数据 (从各组 Log 中提取)
    # 这里的统计逻辑是读取我们在循环中生成的局部 summary
    final_pass=0; final_fail=0; final_ns=0; final_total=0
    
    # 简单解析日志中的 Passed/Failed 行进行汇总
    mapfile -t logs < <(ls ${RESULT_DIR}/logs/${suite_name}_group_*.log 2>/dev/null)
    for log in "${logs[@]}"; do
        p=$(grep "Passed:" "$log" | awk '{sum+=$NF} END {print sum+0}')
        f=$(grep "Failed:" "$log" | awk '{sum+=$NF} END {print sum+0}')
        n=$(grep "Not supported:" "$log" | awk '{sum+=$NF} END {print sum+0}')
        final_pass=$((final_pass + p))
        final_fail=$((final_fail + f))
        final_ns=$((final_ns + n))
    done
    final_total=$((final_pass + final_fail + final_ns))
    
    # 计算通过率
    if [ "$final_total" -gt 0 ]; then
        final_rate=$(awk -v p=$final_pass -v t=$final_total 'BEGIN {printf "%.2f", (p/t)*100}')
    else
        final_rate="0.00"
    fi

    # 2. 将设备上的 QPA 文件转换为 CSV
    # 注意：由于分成了多组运行，最稳妥的方法是逐个转换并合并 CSV
    echo "正在将 ${suite_name} 的 QPA 转换为 CSV..."
    
    COMBINED_CSV="${SUITE_CSV_DIR}/${suite_name}_all_${TIMESTAMP}.csv"
    > "$COMBINED_CSV"

    # 拉取设备上可能残留的所有 QPA 并转换
    # 逻辑：在设备上逐个转换，然后拉取到本地追加
    for ((i=0; i<GROUP_COUNT; i++)); do
        # 这里的路径需与你运行时的 --deqp-log-filename 一致
        DEVICE_QPA="${DEVICE_QPA_DIR}/group_${i}.qpa"
        DEVICE_CSV="${DEVICE_TEMP_DIR}/temp.csv"
        
        # 检查设备文件是否存在
        check=$(sdb shell "ls $DEVICE_QPA 2>/dev/null")
        if [ -n "$check" ]; then
            # 调用转换工具
            sdb shell "/usr/bin/VK-GL-CTS-1.4.5/executor/testlog-to-csv $DEVICE_QPA > $DEVICE_CSV"
            # 拉取并追加到本地总表
            sdb pull "$DEVICE_CSV" "/tmp/current_group.csv" > /dev/null 2>&1
            if [ -f "/tmp/current_group.csv" ]; then
                # 如果是第一个 CSV，保留表头；否则去掉表头追加
                if [ ! -s "$COMBINED_CSV" ]; then
                    cat "/tmp/current_group.csv" >> "$COMBINED_CSV"
                else
                    sed '1d' "/tmp/current_group.csv" >> "$COMBINED_CSV"
                fi
                rm "/tmp/current_group.csv"
            fi
        fi
    done

    # 3. 打印摘要报告
    {
        echo "========================================"
        echo "Tizen CTS 测试摘要: ${suite_name}"
        echo "========================================"
        echo "完成时间: $(date)"
        echo "总测试用例数: ${SUITE_TOTAL_CASES[$suite_name]}"
        echo "实际运行总数: $final_total"
        echo "----------------------------------------"
        echo "Passed:        $final_pass"
        echo "Failed:        $final_fail"
        echo "Not Supported: $final_ns"
        echo "通过率:        $final_rate%"
        echo "----------------------------------------"
        echo "结果文件:"
        echo "CSV 报告: $COMBINED_CSV"
        echo "日志目录: ${RESULT_DIR}/logs/"
        echo "========================================"
    } | tee "$FINAL_SUMMARY"

done

# 清理设备临时文件
sdb shell "rm -rf ${DEVICE_TEMP_DIR}/*.txt ${DEVICE_TEMP_DIR}/*.csv ${DEVICE_QPA_DIR}/*.qpa"

echo "测试任务全部结束。"
