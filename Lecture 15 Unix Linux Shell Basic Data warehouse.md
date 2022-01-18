# Lecture 15 Unix Linux Shell Basic Data warehouse
## 主要知识点
[1. 图示讲解什么是数据仓库data warehouse](#1-图示讲解什么是数据仓库data-warehouse)  
[2. 基础概念](#2-基础概念)  
[3. Dimension table技术](#3-dimension-table技术)  ***重要***  
[4. Fact table 技术](#4-fact-table-技术)  ***重要***  
[5. Integration via conformed dimensions](#5-integration-via-conformed-dimensions)  
[6. SCD: slowly changing dimension](#6-scd-slowly-changing-dimension)  ***重要***  
[7. 学习使用Linux命令](#7-学习使用linux命令)  



## 课堂笔记

### 1. 图示讲解什么是数据仓库data warehouse
- Focus on Kimball

### 2. 基础概念
+ 收集业务需求
+ 与团队各业务专家合作设计dimensional model （Collaborative dimensional modeling workshops）***重要***
+ 4 steps dimensional design
  - decide business process; (Why)
  - declare grain (level of details);  (How much)
    - Keep lowest possible garin
    - Must be declared before choosing dimensions or facts
  - identify dimensions;  (3WS)
    - who, what, where, when, why, and how
  - identify facts；  (What)

### 3. Dimension table技术
- Dimension table structure: conceptual 
  - usually wide, flat denormalized tables with many lowcardinality text attributes
- Dimension surrogate keys
  - These dimension surrogate keys are simple integers, assigned in sequence, starting
    with the value 1, every time a new key is needed
  - The date dimension is exempt from the surrogate key rule; this highly predictable
    and stable dimension can use a more meaningful primary key
- Durable key
  - can be added where surrogate keys would change
- Drill down
- Degenerate dimensions
- Denormalized flattened dimensions
- Multiple hierarchies
- Flags and indicators
- Null attributes in dimension
- Calendar table
- Role playing dimensions
- Junk dimension VS cross join等
- Snowflaked dimension
- Outrigger dimensions

### 4. Fact table 技术
- Fact table结构
- Additive, semi-additive, non-additive
- Nulls in fact tables
- Conformed table
- Transaction fact tables
- Periodic snapshot fact tables
- Accumulating snapshot fact table
- Factless fact tables
- Aggregated fact tables
- Consolidated fact tables

### 5. Integration via conformed dimensions

### 6. SCD: slowly changing dimension

### 7. 学习使用Linux命令
