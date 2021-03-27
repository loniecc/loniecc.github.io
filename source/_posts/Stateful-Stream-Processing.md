---
title: 有状态的流处理
date: 2021-03-27 11:29:47
tags:
categories: 
- Flink
---

###  [原文链接](https://ci.apache.org/projects/flink/flink-docs-release-1.12/concepts/stateful-stream-processing.html)

### 什么是状态
当在一个数据流中，很多算子看起来都是每次只独立处理一个事件的时候（比如event parser），有一些算子能够通过其他事件记住一些信息（比如窗口操作相关的算子）
，这些算子就是**有状态的**
下面是一些例子
* 当一个应用检索确定的事件模式时，Flink状态会把所有已发生的事件存储到一个队列中
* 当按 天/时/分聚合事件时，Flink的状态会保存那些等待聚合的事件
* 当使用流式数据训练机器学习模型时，Flink状态会存储当前模型版本的参数
* 当需要管理历史数据的时候，Flink状态能提供高效的历史的数据访问

Flink 需要感知状态，这样才能使用CheckPoint 和SavePoint 进行容错处理

