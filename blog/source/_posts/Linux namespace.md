#### Linux namespace

链接：https://zhengyinyong.com/post/introduction-to-linux-namespace/

​		   https://zhengyinyong.com/post/how-to-use-uts-namespace/



docker 是基于namespace实现，namespace概念和容易很像，抽象出一个资源独立的空间，可以独立进程id，网络，域名等等。

namespace开放了3个接口，clone，setns，unshare。用户用c语言实现该接口，就可以调用namespace，其他语言也进行了封装。

```go
cmd := exec.Command("sh")
cmd.SysProcAttr = &syscall.SysProcAttr{
  Cloneflags: syscall.CLONE_NEWUTS,
}
```



| **Namespace** | `clone()` **使用的 flag** | **所隔离的资源**             |
| ------------- | ------------------------- | ---------------------------- |
| Cgroup        | CLONE_NEWCGROUP           | Cgroup 根目录                |
| IPC           | CLONE_NEWIPC              | System V IPC，POSIX 消息队列 |
| Network       | CLONE_NEWNET              | 网络设备、协议栈、端口等     |
| Mount         | CLONE_NEWNS               | 挂载点                       |
| PID           | CLONE_NEWPID              | 进程 ID                      |
| User          | CLONE_NEWUSER             | 用户和组 ID                  |
| UTS           | CLONE_NEWUTS              | 主机名和域名                 |

