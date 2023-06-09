[[Namespace]]
cgroup（control group，控制组）是Linux内核中的一个功能，用于限制、监视和隔离进程组的资源使用。cgroup是一种资源管理工具，它可以帮助管理员确保进程之间公平地分配系统资源，例如CPU时间、内存、磁盘I/O和网络带宽。

cgroup通过将进程分组到不同的层次结构（称为层次结构树）中来实现资源管理。每个层次结构树的顶部是一个根cgroup，下面有多个子cgroup。每个cgroup都可以包含一个或多个进程。这使得系统管理员能够针对整个cgroup应用限制，而不仅仅是单个进程。

cgroup有以下主要功能：

1.  限制：为cgroup分配资源限制，例如CPU使用率、内存限制等。
2.  优先级调整：根据优先级，调整cgroup中进程对系统资源的访问。
3.  记录：收集cgroup中进程的资源使用情况统计信息。
4.  隔离：在不同的cgroup中隔离进程，以减少它们之间的相互影响。

cgroup特别适用于容器技术，如Docker和Kubernetes，因为它们依赖于cgroup来限制和隔离每个容器的资源使用。

在Linux系统中，可以通过安装并使用cgroup管理工具（如systemd或cgmanager）来配置和管理cgroup。这些工具提供了创建、修改和删除cgroup，以及为进程分配资源和监控资源使用的功能。

# Cgroup 在容器技术中的主要应用

## 1. 资源限制
  限制容器对于CPU、内存和其他系统资源的使用，有助于防止容器过度消耗资源导致整个系统性能下降。
## 2. 资源隔离
  将容器的资源使用与其他主机系统隔离开，有助于保证容器之间性能不会受到其他容器的影响。
## 3. 资源监控
  收集容器的资源使用情况并统计，以便了解容器的运行状况并做出相应调整。
## 4. 优先级调整
  调整容器中进程的优先级，以便根据需求分配更多或更少的资源。




