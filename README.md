# Dynamically-Updates-the-Difficulty-Values-algorithm
这是一个名为"TSV_Architecture"的C++项目，主要实现了一个TSV(Through-Silicon Via)架构的模拟和分析工具。TSV是3D集成电路中的垂直互连技术，该项目模拟了TSV网络的故障检测和修复机制。

文件结构
CMakeLists.txt - 构建配置文件
main.cpp - 主程序入口
findQ.h/cpp - 查找最佳Q值的功能实现
timer.h/cpp - 计时器工具类
TSVGraph.h/cpp - TSV图结构的核心实现

核心组件分析
1. TSVGraph类
这是项目的核心类，实现了TSV网络的结构和功能：
节点结构(TSVNode):
包含三种TSV类型标志：FTSV(故障)、RTSV(冗余)、UTSV(使用中)
存储块ID和组ID
包含目标指针和三个next指针

主要功能:
初始化TSV故障
多种故障模型窗口：随机与不同大小窗口聚簇
评估修复难度
查找修复路径(BFS算法)
执行修复操作
统计可达节点
计算相应修复率
重要方法:
assignRandomFaults(): 随机标记故障节点
evaluateRepairDifficulty(): 评估修复难度
findRepairPathBFS(): 使用BFS查找修复路径
repairAllFaults(): 修复所有故障节点

2. findQ功能（最佳跨步值）
用于查找最佳的Q值组合(q0, q1, q2):
findAllBestQvals(): 遍历所有可能的Q值组合，找出能覆盖最多组的最优组合
fineAvgSuccessTime(): 测量查找最佳Q值的平均时间

3. 主程序
设置块数和组数
查找最佳Q值
进行性能测试(多线程模拟故障和修复)
输出结果表格

算法分析
Q值搜索算法:
暴力枚举所有可能的Q值组合
使用TSVGraph评估每种组合的有效性
选择能覆盖最多组的组合

修复路径查找:
基于BFS的路径搜索
有限制的搜索深度(MAX_ROUTING_DEPTH)
优先处理修复难度高的节点
考虑连接节点的故障状态
使用加权公式动态更新难度值从而计算出修复率大小
