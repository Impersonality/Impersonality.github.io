---
title: os-异常控制流
date: 2021-06-01 22:03:36
tags: os
---

##### 异常类别

- 中断（interrupt)
- 陷阱（trap)：system call
- 故障（fault)：缺页故障，可能有返回
- 终止（abort)：无返回，直接终止



##### 用户模式和内核模式

通过某个控制寄存器中的一个模式位来识别



##### system call

- fork：1.调用一次，返回两次（父、子）2.并发执行  3.相同但独立的地址空间 4.共享文件
- execve：调用一次从不返回
- waitpid：等待终止或停止时，回收子进程



##### 父子进程

父进程终止，内核会安排init进程（pid=1)成为它孤儿进程的养父

终止但未回收的进程成为僵尸进程



##### 信号

- 内核通过更新目的进程context发送信号
- kill 命令可向其他进程发送信号，kill [signal] (pid) 若pid为负，向该pid所在的进程组所有进程发送信号



##### 非本地跳转

setjmp保存当前context，longjmp取出context