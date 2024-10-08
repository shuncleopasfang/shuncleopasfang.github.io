---
layout: post
title: "[Notes] SQL Optimizer Parsing"
date: 2024-07-05
categories: [Computer Science]
tags: [SQL]
---

<br>

# Table of Contents

- [Preview](#Preview)
    - [大数据体系和 SQL](#大数据体系和-SQL-1)
    - [常见的查询优化器](#常见的查询优化器-1)
    - [查询优化器的社区开源实践](#查询优化器的社区开源实践-1)
    - [SQL 相关的前沿趋势](#SQL-相关的前沿趋势-1)
    
- [Learning](#Learning)
    - [大数据体系和 SQL](#大数据体系和-SQL-2)
    - [常见的查询优化器](#常见的查询优化器-2)
    - [查询优化器的社区开源实践](#查询优化器的社区开源实践-2)
    - [SQL 相关的前沿趋势](#SQL-相关的前沿趋势-2)
    
- [References](#References)

<br>

# Preview <a name="Preview"></a>

<br>

## 大数据体系和 SQL <a name="大数据体系和-SQL-1"></a>

- 生产系统中的大数据体系
    - 云厂商 (火山引擎, 阿里云, 腾讯云, 华为云, Google Cloud, Microsoft Azure) 提供的大数据相关的产品, 包括计算、存储、调度、应用等
    - 批式计算、流式计算、交互分析引擎、YARN、Kubernetes 等  

- SQL 的基本用法和关系代数基础知识 (选择、投影、连接、集合操作等)

- 编译原理相关的基础知识
    - 词法分析 (Lexical Analysis)
    - 语法分析 (Syntactic Analysis)
    - 抽象语法树 (Abstract Syntax Tree, AST)  

- SQL 里的执行计划
    - 逻辑计划 (Logical Plan)
    - 物理计划 (Physical Plan)
    - 分布式执行计划: Plan Fragment
    - Left-deep tree  

- SQL 执行的基本流程
    - 任务调度: DAG  

- 分布式系统中 shuffle 的实现方式
    - Broadcast shuffle vs. Repartition shuffle
    - 参考 MapReduce 和 Spark 系统  

- SQL 中 group-by 和 join 的执行方式
    - Hash-based vs. Sort-based  

<br>

## 常见的查询优化器 <a name="常见的查询优化器-1"></a>

- Top-down Optimizer

- Bottom-up Optimizer

- Rule-based Optimizer, RBO
    - Rule
    - Pattern  

- Cost-based Optimizer, CBO
    - 动态规划  

- 交换律、结合律、传递性

- RBO 优化规则
    - 列裁剪
    - 谓词下推
    - 传递闭包
    - Runtime Filter (min-max filter, in-list filter, bloom filter)
    - Join 消除
    - 谓词合并  

- CBO 相关概念
    - 统计信息
        - Number of Distinct Value, NDV
        - Selectivity
        - Cardinality
    - 代价模型  

<br>

## 查询优化器的社区开源实践 <a name="查询优化器的社区开源实践-1"></a>

- Apache Calcite

- Orca

- Volcano/Cascade 框架
    - Memo
    - AND/OR Graph
    - Expression group
    - Group expression
    - Pattern
    - Rule
    - Branch-and-Bound Pruning
    - Winner  

<br>

## SQL 相关的前沿趋势 <a name="SQL-相关的前沿趋势-1"></a>

- 存储计算分离

- HSAP, HTAP, HTSAP

- Cloud Native, Serverless

- 数据仓库, 数据湖, 湖仓一体, 联邦查询

- 智能化: AI4DB, DB4AI

<br>

# Learning <a name="Learning"></a>

<br>

## 大数据体系和 SQL <a name="大数据体系和-SQL-2"></a>

- 为什么 SQL 如此流行？
    - 有 MySQL、Oracle 之类使用 SQL 作为交互语言的数据库
    - 有 JDBC、ODBC 之类和各种数据库交互的标准接口
    - 有大量数据科学家和数据分析师等不太会编程语言但又要使用数据的人
    - 多个大数据计算引擎都支持 SQL 作为更高抽象层次的计算入口
        - MapReduce -> Hive SQL
        - Spark -> Spark SQL
        - Flink -> Flink SQL  

- SQL
    - Parser
        - 把文本变成抽象语法树结构 (AST)
        - 涉及词法分析阶段 (拆分字符串, 提取关键字, 字符串, 数值等) 和语法分析阶段 (把词条按照定义的语法规则组装成抽象语法树结构)
        - 和编译原理课程里的"前端"知识相关
    - Analyzer
        - 访问库/表元信息并绑定
        - 判断 SQL 是否合理, 比如数据库, 表和列名是否存在, 列的数据类型是否正确
        - 将 AST 转换成逻辑计划树 (在某些系统中这个工作由一个 Converter 完成)  

- 逻辑计划树
    - 所谓逻辑计划树, 可以理解为**逻辑地**描述一个 SQL 如何一步步地执行查询和计算, 最终得到执行结果的一个分步骤地计划. 树中每个节点是是一个算子, 定义了对数据集合的计算操作 (过滤, 排序, 聚合, 连接), 边代表了数据的流向, 从孩子节点流向父节点. 之所以称它为逻辑的, 是因为算子定义的是逻辑的计算操作, 没有指定实际的算法, 比如对于逻辑的排序算子, 逻辑计划树里没有指定使用快排还是堆排  

- 查询优化
    - SQL 是一种声明式语言, 用户只描述做什么, 没有告诉数据库怎么做
    - 查询优化的目标是为 SQL 找到一个正确的且执行代价最小的执行计划
    - 查询优化器是数据库的大脑, 最复杂的模块, 很多相关问题都是 NP 的
    - 一般 SQL 越复杂, Join 的表越多, 数据量越大, 查询优化的意义就越大, 因为不同执行方式的性能差别可能有成百上千倍
        - 类比 gcc/g++ 编译程序时的编译级别 (-O1, -O2, -O3), 经过编译优化的程序运行效率更高  

- 物理执行计划
    - 优化器的输出是一个分布式的物理执行计划
    - 分布式物理执行计划的目标是在单机 Plan 的基础上最小化数据移动和最大化本地 Scan, 生成 PlanFragment 树
    - 一个 PlanFragment 封装了在一台机器上对数据集的操作逻辑. 每个 PlanFragment 可以在每个 executor 节点生成 1 个或多个执行实例, 不同执行实例处理不同的数据集, 通过并发来提升查询性能
    - Plan 分布式化的方法是增加 shuffle 算子, 执行计划树会以 shuffle 算子为边界拆分为 PlanFragment  

- Executor
    - Executor 按照物理执行计划扫描和处理数据, 充分利用机器资源 (CPU 流水线, 乱序执行, cache, SIMD)  

<br>

## 常见的查询优化器 <a name="常见的查询优化器-2"></a>

- RBO
    - 基于关系代数等价规则对逻辑计划进行变换
    - 实现上:
        - Pattern: 定义了特定结构的 Operator 子树 (结构)
        - Rule: 定义了如何将其匹配的节点替换 (Substitute) 为新形态, 从而生成新的、等价的 Operator 树 (**原地替换**)
        - 优化器搜索过程被抽象为不断匹配 Pattern 然后应用 Rule 转换, 直到没有可以匹配的 rule
    - 局限性:
        - 无法解决多表连接问题
        - 无法确定和选择最优的分布式 Join/Aggregate 执行方式  

- CBO
    - 使用一个模型估算执行计划的代价, 选择代价最小的执行计划
    - 分而治之, 执行计划的代价等于所有算子的执行代价之和
    - 通过 RBO 得到 (所有) 可能的等价执行计划 (**非原地替换**)
    - 算子代价包含 CPU, cache misses, memory, disk I/O, network I/O 等代价
        - 和算子的统计信息有关, 比如输入、输出结果的行数, 每行大小等
        - 叶子算子 scan: 通过统计原始表数据得到
            - 中间算子: 根据一定的推导规则, 从下层算子的统计信息推导得到
            - 和具体的算子类型, 以及算子的物理实现有关 (e.g. hash join vs. sort join)
    - 使用动态规划枚举所有执行计划, 选出执行代价最小的执行计划  

- 统计信息
    - 基表统计信息
        - 表或者分区级别: 行数、行平均大小、表在磁盘中占用了多少字节等
        - 列级别: min、max、num nulls、num、not nulls、num、distinct value (NDV)、histogram 等
    - 推导统计信息
        - **选择率 (selectivity)**: 对于某一个过滤条件, 查询会从表中返回多大比例的数据
        - **基数 (cardinality)**: 基本含义是表的 unique 行数, 在查询计划中常指算子需要处理的行数  

<br>

## 查询优化器的社区开源实践 <a name="查询优化器的社区开源实践-2"></a>

- Volcano/Cascade 框架
    - Memo
        - Cascades Optimizer 在搜索的过程中, 其搜索的空间是一个关系代数算子树所组成的森林, 而保存这个森林的数据结构就是 Memo. Memo 中两个最基本的概念就是 **Expression Group (简称 Group)** 以及 **Group Expression** (对应关系代数算子). 每个 Group 中保存的是逻辑等价的 Group Expression, 而 Group Expression 的子节点是由 Group 组成
    - Memo 本质是 AND/OR Graph, 通过共享相同的子树减少内存开销, 记录搜索过的子树的最优执行计划 (winner)  

- Branch-and-Bound Pruning
    - 已搜索完成的物理计划的代价最小值成为 Cost Upper Bound. 当新的搜索分支的代价高于它时, 不需继续搜索. 初始 Cost Upper Bound 可由优化器根据启发式规则估算  

<br>

## SQL 相关的前沿趋势 <a name="SQL-相关的前沿趋势-2"></a>

- 存储计算分离

- HSAP, HTAP, HTSAP

- Cloud Native, Serverless

- 数据仓库, 数据湖, 湖仓一体, 联邦查询

- 智能化
    - AI4DB
        - 自配置: 智能调参 ([OtterTune](https://www.cs.cmu.edu/~ggordon/van-aken-etal-parameters.pdf), [QTune](https://www.vldb.org/pvldb/vol12/p2118-li.pdf))、负载预测、负载调度
        - 自诊断和自愈合: 软硬件错误、错误恢复和迁移
        - 自优化: 统计信息估计 ([Learned cardinalities ](https://arxiv.org/abs/1809.00677))、代价估计、学习型优化器 ([IBM DB2 LEO](http://diaswww.epfl.ch/courses/adms07/papers/leo.pdf)), 索引推荐, 视图推荐
    - DB4AI
        - 内嵌人工智能算法 (MLSQL, SQLFlow)
        - 内嵌机器学习框架 (SparkML, Alink, dl-on-flink)  

<br>

# References <a name="References"></a>

<br>

- CMU 数据库相关课程
    - [初级] [15445.courses.cs.cmu.edu/fall2021/](https://15445.courses.cs.cmu.edu/fall2021/)
    - [高级] [15721.courses.cs.cmu.edu/spring2020/](https://15721.courses.cs.cmu.edu/spring2020/)  

- [Access Path Selection in a Relational Database Management System](https://courses.cs.duke.edu/compsci516/cps216/spring03/papers/selinger-etal-1979.pdf)  

- Volcano/Cascades 框架相关论文
    - [The Volcano Optimizer Generator : Extensibility and Efficient Search](http://www.seas.upenn.edu/~zives/03s/cis650/P209.PDF)
    - [The Cascades Framework for Query Optimization](https://www.cse.iitb.ac.in/infolab/Data/Courses/CS632/Papers/Cascades-graefe.pdf)
    - [Efficiency in the Columbia Database Query Optimizer](https://15721.courses.cs.cmu.edu/spring2018/papers/15-optimizer1/xu-columbia-thesis1998.pdf)  

- [Apache Calcite: A Foundational Framework for Optimized Query Processing Over Heterogeneous Data Sources](https://arxiv.org/pdf/1802.10233)  

- [github.com/pingcap/awe…](https://github.com/pingcap/awesome-database-learning#query-optimizer)  

- 回顾大数据系统的过去和展望大数据系统的未来
    - [云原生数据库设计新思路](https://pingcap.com/zh/blog/new-ideas-for-designing-cloud-native-database)

<br>
