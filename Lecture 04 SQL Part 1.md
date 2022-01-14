# Lecture 04 SQL Part 1
## 主要知识点
[1. SQL基础介绍](#1SQL基础介绍)  
[2. SQL案例1讲解](#2SQL案例1讲解)  



## 课堂笔记

### 1.SQL基础介绍
+ 数据类型 Data Type 大类 in Snowflake
   + Numeric数字类型：decimal type等等
      - Data Warehouse中用 NUMBER (DECIMAL) 基本可以替代所有Numeric类型
      - DECIMAL (M,D), M: precision, D: scale
   + 字符串类型/ Binary数据类型
      - VARCHAR (STRING,TEXT) 有优势，支持16MB (uncompressed)， 长度flexible
   + 逻辑数据类型: 布尔boolean 等等
      - TRUE, FALSE, unknown
   + Date & Time   
      - DATE, Time, DATETIME (TIMESTAMP_NTZ)
      - TIMESTAMP_LTZ for TIMESTAMP with local time zone (Timezone 夏令时可能带来影响）
      - TIMESTAMP_NTZ for TIMESTAMP with no time zone (default)
      - TIMESTAMP_TZ　for TIMESTAMP with time zone
   + ***重点***　Semi-structured数据类型 (Snowflake 优势），可以储存json文件
      - VARIANT　包括object 和array， 支持16MB (compressed)
      - OBJECT（Structure）　user-defineｄ structure, can be accessed by name, can have different data types
      - ARRAY 　基准数学格式, can be accessd by index number, must have same data type
      - lateral flatten   A function to parse arrays
+ 几种不同的Join类型: left join, inner join, right join, full join (Snowflake only), natural join(工业中不适用）
   - Left,Right join 统一只使用一种
   - Join multiple tables
      + 两张表一组，一步步找出逻辑关系
+ SQL Select
   - Select
   - FROM
   - JOIN
   - WHERE
   - AND OR
   - GROUP BY
   - HAVING 
   - ORDER BY
+ SQL Operator (数学运算、比较、逻辑运算)
+ SQL Alias
+ SQL 逻辑运算
+ Aggregation function
+ Numberic function
+ 字符串处理
+ 多表间查询操作
   - union vs union all: union would remove duplicate records, union all would keep all records　
   - Better use union all, as union would remove duplicates and consume resources
+ 子查询语句嵌套Nested Query

### 2.SQL案例1讲解


### 作业
+ 
