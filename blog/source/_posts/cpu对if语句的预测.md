---
title: cpu对if语句的预测
date: 2021-05-05 22:42:31
tags: 计组
---

#### 机器指令与流水线

cpu执行机器指令需要4个步骤：取指、译码、执行、回写，这些阶段分别由特定的硬件执行，采用工厂流水线方式。比如硬件A取指 指令1，然后取指 指令2，取指之后的指令都交付给硬件B译码，理论上4个硬件同时工作，在同一时刻就能完成一条指令的执行。



#### if指令

问题：if指令需要等待if条件的结果，他也可以流水线执行么

我想的是不能，cpu让其阻塞等待，或者设置一个if等待区。

事实是可以的，解决办法是**猜**

cpu根据特定策略猜if会走的分支，然后流水线执行，如果猜对无事发生，猜错则该指令的后续指令全部作废，重新执行，该过程叫**分支预测**



#### 总结

一个小细节：编写if语句，最好有一定规律，让cpu猜对（太完美主义了。。。）比如for循环数组时，if判断，这个数组如果有序对分支预测是有帮助的

好吧，实际中没必要这么追求效率，分支预测的性能损失并不大，而且不了解其策略说不定适得其反。

只是觉得改知识点挺有意思

参考：https://zhuanlan.zhihu.com/p/369942218