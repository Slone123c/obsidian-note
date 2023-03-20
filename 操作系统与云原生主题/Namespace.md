[[Cgroup]]


在Linux操作系统中，namespace技术是一种轻量级的虚拟化机制，用于在同一台主机上隔离和限制进程的访问权限。namespace的主要目的是为进程提供一个独立的、与其他进程隔离的视图。这使得进程可以在相互隔离的环境中运行，类似于运行在单独的虚拟机中。

Linux内核支持多种类型的namespace，每种类型负责隔离不同的系统资源：

1.  Mount namespace（挂载）：独立进程对文件系统挂载点的视图。每个挂载namespace中的进程只能看到属于自己namespace的挂载点。

2.  PID namespace（进程ID）：隔离进程ID的分配，使得不同PID namespace中的进程可以有相同的进程ID，但在不同namespace间互相不可见。

3.  Network namespace（网络）：独立进程对网络接口、路由表和防火墙规则等网络资源的视图。每个网络namespace中的进程都有自己的网络栈，无法直接访问其他namespace的网络资源。

4.  IPC namespace（进程间通信）：隔离进程间通信资源，如System V IPC对象和POSIX消息队列。不同IPC namespace中的进程无法直接通信。

5.  UTS namespace（Unix Timesharing System）：隔离主机名和域名。每个UTS namespace中的进程可以有自己的主机名，互不影响。

6.  User namespace（用户）：隔离用户ID和组ID，使得一个namespace中的进程可以在另一个namespace中具有不同的用户和组权限。这有助于实现更细粒度的权限控制和资源限制。

7. Time namespace（时间）：隔离进程对系统时间和时钟的视图。这可以让进程在一个独立的、与其他进程隔离的时间环境中运行。
