# main函数
在每个仿真周期（时间片）中，合法车辆 和 攻击者 发出信号，系统根据信道响应 RSS 来判断谁是“好人谁是坏人”，并通过强化学习不断学习最优的认证策略（即检测阈值 x1 和检测模式 x0），以提升识别率、减少误判，并降低能耗。

本质还是通过合法包与spoof包得到的欧几里得距离归一化后与阈值比较，得到虚警率和漏报率

