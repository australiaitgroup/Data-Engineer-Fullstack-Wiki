# Lecture 05 SQL Part 2
## 主要知识点
[1. SQL案例1讲解](#1SQL案例1讲解)  
[2. SQL案例2讲解](#2SQL案例2讲解)  
[3. SQL案例3讲解](#3SQL案例3讲解)  
[4. SQL基础介绍](#4SQL基础介绍)  



## 课堂笔记

### 1.SQL案例1讲解

### 2.SQL案例2讲解

### 3.SQL案例3讲解

### 4.SQL基础介绍
+ Summary, ***做到第七层面试第一轮基本OK***
   1. SELECT & WHERE
   2. GROUP BY & Having
   3. Nested Query
   4. Rank/Row Number
   5. Partition By
   6. Range Selection
   7. Further Analytic function
+ 表(Table)与视图(View)的比较
   - Table 物理存在, View 逻辑存在
+ SQL tuning
+ 了解索引index的优点，分类，语法
+ 介绍窗口分析函数window analytic function
   - DENSE_RANK
      - Rank of current row within its partition without gaps
      - DENSE_RANK () OVER (order by COLUNM_NAME)
   - RANK
      - Rank of current row within its partition gaps
      - RANK() OVER (order by COLUNM_NAME) 
   - ROW_NUMBER
      - Number of current row within its partition
      - ROW_NUMBER() OVER (order by COLUNM_NAME)   
+ 窗口分析函数高阶:
   - partition by 的使用，如:rank()over(partition by XXX order by XXX)
      - 结合rank实现分组排序
   - lead(XXX, n)over(partition by XXXX order by XXXX)
      - 提取下面第n行的数据 （例如下次订单时间），未找到则返回null
   - lag(XXX, n) over(partition by XXXX order by XXXX)
      - 提取上面第n行的数据 （例如上次订单时间），未找到则返回null
+ Snowflake query 的json格式语法讲解
+ Snowflake flatten function to parse arrays 语法讲解， snowflake实操演示
+ 讲解如何用command line把本地数据导入snowflake
   1. Check the input source (e.g. csv, txt)  Data Profiling, 重要
   2. Create & Run target table SQL
   3. Open CLI/ Web Interface
   4. Select database & table
   5. Create File Format
   6. Create Stage
   7. Put the file into Stage
   8. Copy data into table
+ SQL Cumulative sum & moving average
   - SUM(XXX) OVER ( ORDER BY XXX ROWS BETWEEN M PRECEDING AND N FOLLOWING) AS XXX
   - AVG(XXX) OVER ( ORDER BY XXX ROWS BETWEEN M PRECEDING AND N FOLLOWING) AS XXX
+ Common table expression CTE 实例讲解
   - WITH XXX AS (select ...)
   - CTE can be self-referencing
+ NTILE 案例讲解
   - NTILE(N) OVER (PARTITION BY XXX ORDER BY XXX) AS XXX
   - Divide data into N groups
+ Recursive CTE: 语法，案例讲解
   - 消耗资源，效率低
   - Syntax: <br />
     WITH RECURSIVE cte_name AS (<br />
     &emsp;initial_query -- anchor member<br />
     &emsp;UNION ALL<br />
     &emsp;recursive_query -- recursive member that<br />
     &emsp;references to the CTE name<br />
     )<br />
     SELECT * FROM cte_name;
   - Example: <br />
     WITH RECURSIVE employee_rec AS (<br />
     &emsp;SELECT emp_name,<br />
     &emsp;emp_manager,<br />
     &emsp;1 as Band<br />
     &emsp;FROM emp_test<br />
     &emsp;WHERE emp_manager IS NULL<br />
     &emsp;UNION ALL<br />
     &emsp;SELECT e.emp_name,<br />
     &emsp;e.emp_manager,<br />
     &emsp;Band+1<br />
     &emsp;FROM emp_test e<br />
     &emsp;INNER JOIN employee_rec ep<br />
     &emsp;ON ep.emp_name = e.emp_manager )<br />
     select * From employee_rec
   

