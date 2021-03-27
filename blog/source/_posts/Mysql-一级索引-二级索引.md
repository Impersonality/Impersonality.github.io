---
title: Mysql 一级索引 二级索引
date: 2021-03-27 15:46:35
tags: mysql
---

#### Mysql explain

转载：https://blog.csdn.net/AAA821/article/details/86440722

表物理上是一个b+树，innodb使用聚簇索引来组织表，默认使用主键作为聚簇索引

未定义主键，则取第一个唯一索引，并且不包含Null。

如果没有这样的列，innodb自建一个6位数的id值，并且是隐藏的。

其他索引就是二级索引

