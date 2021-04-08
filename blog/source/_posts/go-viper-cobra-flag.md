---
title: go viper/cobra/flag
date: 2021-03-22 21:18:42
tags: go
---



#### viper

[viper](https://blog.biezhi.me/2018/10/load-config-with-viper.html)

获取值：viper.Get()

设置待读取配置文件名：vipser.SetconfigName()

设置搜索路径：viper.AddConfigPath(“.”)

读取配置数据（必需）：viper.ReadInConfig()



#### flag

[flag](https://o-my-chenjian.com/2017/09/20/Using-Flag-And-Pflag-With-Golang/)

flag.Int(name, value, usage)：代码中可以设置默认值，然后从命令行读取实际值，当作环境变量使用

flag.Parse()：解析命令行传递的参数



#### cobra

[cobra](https://www.qikqiak.com/post/create-cli-app-with-cobra/)

[cobra](https://www.cnblogs.com/sparkdev/p/10856077.html)

1.用cobra脚手架cobra init --pkg-name [name] 生成cmd文件夹

2.root.go中包含rootCmd，这是根命令，cmd.AddCommand生成子命令

3.command执行是通过command.run实现，在run前后还有几个方法，执行顺序是：

​	1.persistentPreRun	2.PreRun	3.Run	4.PostRun	5.PersistentPostRun	