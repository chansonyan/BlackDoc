---
layout: post
title: 初识Hadoop
categories: BigData hadoop
tags: BigData hadoop
---


###初识Hadoop

---

####大数据:
1. Volume    容量    （超大文件）
2. Velocity    速度    （读，存速度，数据分析处理速度）
3. Variety     种类    （结构化程度）

####数据结构化程度：
1. structured data
2. semi-structured data
3. unstructured data

####构建分布式： 

- 数据存储
- 数据分析
- 协调处理

---

####Hadoop

Hadoop 泛指一组使用hadoop基础平台进行__分布式计算__和__海量数据处理__的项目。

####Hadoop生态系统：

1. Common
>一系列组件和接口，用于分布式文件系统和通用I/O（序列化，Java RPC 和 持久化数据结构）
2. Avro
>一种序列化系统，用于支持高效，跨语言的RPC 和 持久化数据存储）
3. MapReduce
>分布式数据处理模型 和 执行环境， 运行于大型商用机集群
4. HDFS （DFS )
>Hadoop Distributed File System, 分布式文件系统，运行于大型商用机集群
5. Pig 
>数据流语言和运行环境，用于探索非常庞大的数据集。Pig运行在MapReduce和HDFS集群上
6. Hive
>一种分布式的，按列存储的数据仓库。
>Hive管理HDFS存储的数据，并提供基于SQL的查询语言用以数据查询（运行时翻译成MapReduce作业）
7. HBase
>一种分布式的，按列存储的数据库。
>HBase使用HDFS作为底层存储，同时支持MapReduce的批量式计算和点查询（随机读取）
8. ZooKeeper
> 一种分布式的，可用性高的协调服务。
> ZooKeeper提供分布式锁之类的基本服务用于构建分布式应用
9. Sqoop
> 该工具用于在结构化数据存储（如关系型数据库）和HDFS之间高效批量传输数据
10. Oozie
> 该服务用于运行和调度Hadoop作业（如MapReduce，Pig，Hive及Sqoop作业）
