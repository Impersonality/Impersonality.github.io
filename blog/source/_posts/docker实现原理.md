---
title: docker实现原理
date: 2021-04-08 16:28:22
tags: docker
---

公众号看到github推荐项目：go实现的mini docker（gocker），该作者推荐了1000行shell脚本所实现的bocker，对此产生了些兴趣，去网上查，有本书《自己动手写docker》，通过此书了解了docker的大致实现，也尝试写了点，不过还是基础不够扎实，在之后实现镜像和完善容器时，感觉还需要花费很多时间，觉得暂时琢磨到这了吧，以后有需求可以继续深究。

这里总结一下自己的学习



#### 基础知识

##### namespace

linux的隔离工具，可以创建出一个独立的进程空间（类似于容器的概念），有几种隔离模式，mount，pid，user等等

##### cgroups

linux限制资源的工具，限制cpu，内存，存储等等

##### ufs

联合文件系统，之前用的是aufs，现在用的是overlay，将不同的存储设备（挂载）抽象成一个存储设备，比如一块光盘和一个u盘，将内容抽象成一块磁盘展示给用户



#### 容器

容器就是使用namespace + cgroups创建出一个独立的空间，先用namespace创建一块空间，隔离模式都选上(mount,pid,user,net等等)，然后修改/proc挂载（mount -t proc proc /proc）这样proc才独立了，再使用cgroups限制资源等等，这样一块空间就开辟出来了，不过这里面是空的，程序怎么加载进去呢



#### 镜像

简单将程序copy到容器似乎就可以了，不过这样会有问题：1.没有分层镜像会很大，难以管理，比如flask和django都用到了Python，如果将python和底层unix系统抽象出来好像更好；2.在容器中会修改镜像的内容，那么下次还原或者恢复时又得重新下载。

所以docker使用了ufs，镜像分层，同时镜像都是只读层，最上面有一个可写层，对镜像的修改会在其他的存储。

参考：[coolshell aufs](https://coolshell.cn/articles/17061.html)



总结的很简单，不过docker本身也不复杂，好的设计本身也是用简单的办法去解决“庞大”问题，docker，nginx，redis都是如此。

还有些细节没有去深究了，比如数据卷，网络，以后有兴趣再补