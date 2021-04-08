---
title: linux cgroups
date: 2021-04-08 09:08:11
tags: linux
---



Cgroups是linux用来隔离资源（cpu、mem)的技术，由3个组件组成

Hierarchy：将cgroup串成树状的结构，通过树状结构，cgroup可以继承，可以绑定多个subsystem

cgroup：hierarchy的节点，进程可以加入一个或者多个cgroup（不同的hierarchy）

subsystem：系统资源的限制，比如cpu限制等，需要绑定在一个hierarchy上



##### 创建cgroup

（mount挂载-t标注cgroup即可：mount -t cgroup [filename] ./[filename]

  在cgroup文件夹下创建文件夹，会被自动识别为该cgroup的子cgroup（生成文件		

 /proc/[pid]/cgroup  中可以看到该进程属于哪个cgroup



mount | grep cgroup可以看到hierarchy的根部，挂载了很多subsystem(cgroup类型)，在这些subsystem里创建文件夹(子cgroup)，加入进程id，实现对进程资源的限制。

在cgroup文件夹cgroup.procs和tasks添加删除pid要用sh -c 操作，删除只需要将pid移动到另一个cgroup中即可