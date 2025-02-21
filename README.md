# smartmem2025_baseline

## 比赛链接

https://www.codabench.org/competitions/3586

## 比赛背景

内存故障预测，与天池 PAKDD2021 很类似。

（某老运维说，华为云来炒四年前阿里云的冷饭了，大概说明了这四年间内存故障预测还是个赛博算命的伪需求。）

## baseline 思路

官方的 baseline：https://github.com/hwcloud-RAS/SmartHW/tree/main/competition_starterkit

官方的 baseline 写的还是不错的，就是模块化设计比较臃肿，于是自己重新写了，比较短小精悍，适合魔改；

同时添加了线下的验证，本 baseline 线下 0.21，线上 0.24。

其他说明：

1. 重新设计了 window 特征，加了不少 diff 特征，窗口大小设置为 1h，可以多尝试其他窗口大小
2. 五折 sn 划分验证可能不太准确，也可以改成 时间+sn 划分
3. 标签采用了线性指标变换: 第一次出现故障为 1, 往后的正样本进行标签衰减, 最小值截断为 0.5，改为回归任务
4. row wise 和 sn wise 指标割裂比较严重
5. 0.05 训练负采样
