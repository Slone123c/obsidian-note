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

