# Kafka

## 消息队列

### 概述

消息队列中间件是分布式系统中重要的组件，主要解决应用耦合、异步消息、流量削峰等问题

> 当不需要立即获得结果，但是并发量又需要进行控制的时候，差不多就是需要使用消息队列额时候

### 消息队列的特点（优点）

+ 解耦： 简单讲是一个事务只关心核心流程，而需要依赖其他系统但不那么重要的事情，有通知即可，无需等待结果
+ 异步： 非核心流程异步化，减少系统响应时间，提高吞吐量。例如：短信通知
+ 广播： 消息队列的一个消息可以广播给多个订阅者
+ 削峰和限流： 广泛应用于秒杀或抢购活动中，避免流量过大导致应用系统挂掉的情况

### 消息队列的两种模式

+ 点对点模式
+ 发布订阅模式

## Kafka -- 分布式流平台

Kafka 不仅是一个消息队列，官方给Kafka的定义是： 一个分布式流平台

### 流平台三个关键能力

1. 可以发布订阅记录流，类似于一个消息队列或企业消息系统
2. 可以持久化记录流，从而具有容错能力
3. 可以在流式记录产生的时候就进行处理

### 适合什么场景

1. 构建实时流数据管道，它可以在系统或应用之间可靠的获取数据
2. 构建实时流式应用程序，对流数据进行响应或转换

### kafka几个概念

+ kafka是运行在一个或多个服务器的集群上的
+ kafka集群分类存储的记录流被称为主题(topic)
+ 每个消息记录包含一个键，一个值和时间戳

### 主题和分区

Kafka的消息通过主题进行分类。主题可以被分为若干个分区，一个分区就是一个提交日志。消息以追加的方式写入分区，然后以先入先出的顺序读取。无法保证主题范围内的顺序，只能保证消息在单个分区内的顺序。分区中的每个记录都有一个连续的ID，称为offset，唯一标识分区内的记录。

### 生产者和消费者

生产者创建消息，发送数据到它选择的topic。生产者负责决定将数据发送到topic的哪个分区上，这可以通过简单的循环方式来平衡负载，或者可以根据某些语义来决定分区。

消费者使用一个group name来标识自己的身份，消费者是消费者群组的一部分，也就是说一个或多个消费者共同读取一个主题。群组保证每个分区只能被一个消费者使用。