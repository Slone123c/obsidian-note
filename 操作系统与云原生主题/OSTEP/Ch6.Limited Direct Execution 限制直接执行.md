## Restricted Operations


### user mode
Only access limited resources and cannot directly access hardware devices.
Need to use the system call interface to access other processes.
### kernel mode
OS has complete control over the system's resources.
### The diff when running program in kernel mdoe / user mode
Running a program in kernel mode provides unrestricted access to system resources, while running a program in user mode provides a restricted environment that provides a layer of protection and isolation between the program and the rest of the system.
### Why kernel mode?
Running a program in kernel mode is necessary for implementing critical system-level functionality that cannot be implemented in user mode.

However, running a program in kernel mode also introduces potential security risks, since any errors or malicious code executed in kernel mode can directly access and manipulate system resources, potentially causing system crashes or security breaches.

### trap instruction
Using trap instrction to jump to the kernel mode to execute program.
### trap table
The trap table is a data structure used by the operating system to store information about exception and interrupt handlers.


## 理解操作系统的上下文切换
操作系统在运行多个进程时需要将cpu时间片分给不同的程序以便都能执行，其中上下文切换是指cpu在切换所运行程序的时候将当前程序的上下文保存，并读取另外一个程序的上下文，但是操作系统也要保证在完成了另外程序的执行后能切换回原程序的上下文并继续执行。

**更规范的解释是：**
操作系统从当前正在执行的进程或线程中收回CPU控制权，并将它转移到另一个处于就绪状态的进程或线程中。

上下文切换是一项开销较大的操作，因为在切换过程中需要进行大量的上下文保存和加载操作，需要耗费一定的 CPU 时间。因此，操作系统需要尽可能地减少上下文切换的次数，以提高系统的性能。