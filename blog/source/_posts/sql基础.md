---
title: sql基础
date: 2021-04-21 21:45:37
tags: database
---



#### 知识点

1.注释：单行 --   多行/*

2.group by子句中不能写列的别名（因为select在group by之后）

3.group by时，select中字段要求可汇总（聚合函数/或在group by中出现）

4.想要删除查询结果的重复记录应使用distinct，想要计算汇总结果（聚合函数）使用group by

5.insert 语句中也可以使用子表（insert into table select ...）

6.where中不能写聚合函数，可以用标量子查询替代，如：where price > (select avg(price) from product)

7.标量子查询可以写在select 语句后

8.string拼接用 || 代替 +

9.not in 后面不能写null



#### QA

> Q：select * from table group by column    why failed ?
>
> A：因为group by 是对表切分后汇总（折叠），要求select出的结果字段都是可汇总的，否则会出错



> where 和 having 执行速度
>
> 通常where更快，因为where可以使用索引，另一方面聚合函数操作时会先排序，用where提前过滤查询数据行数会减少排序压力