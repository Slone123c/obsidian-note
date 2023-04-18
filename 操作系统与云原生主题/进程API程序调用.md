[[进程]]

# fork()
```c
#include <stdio.h>  
#include <stdlib.h>  
#include <unistd.h>  
  
int  
main(int argc, char *argv[])  
{  
    printf("hello world (pid:%d)\n", (int) getpid());  
    int rc = fork();  
    printf("this is rc: %d", rc);  
    if (rc < 0) {  
        // fork failed; exit  
        fprintf(stderr, "fork failed\n");  
        exit(1);  
    } else if (rc == 0) {  
        // child (new process)  
        printf("hello, I am child (pid:%d)\n", (int) getpid());  
    } else {  
        // parent goes down this path (original process)  
        printf("hello, I am parent of %d (pid:%d)\n",  
          rc, (int) getpid());  
    }  
    return 0;  
}
```
调用`fork()`函数并不会重新执行整个程序。在程序执行到`fork()`函数时，它会创建一个新的子进程，子进程会从`fork()`函数后面的代码行继续执行，而父进程则继续执行`fork()`函数后面的代码行。也就是说，程序的执行流程并没有从头开始。

子进程是由父进程复制而来的，因此它们共享相同的代码段和数据段。子进程会从父进程的状态中继承一些信息，例如打开的文件描述符、信号处理程序、进程权限等。但是子进程拥有自己的进程ID和内存空间，它们之间互相独立。

因此，调用`fork()`函数并不会重新执行整个程序，而是在当前程序的基础上创建一个新的子进程，使得程序可以同时运行在多个独立的进程中。

# wait()
```c
#include <stdio.h>  
#include <stdlib.h>  
#include <unistd.h>  
#include <sys/wait.h>  
  
int  
main(int argc, char *argv[])  
{  
    printf("hello world (pid:%d)\n", (int) getpid());  
    int rc = fork();  
    if (rc < 0) {  
        // fork failed; exit  
        fprintf(stderr, "fork failed\n");  
        exit(1);  
    } else if (rc == 0) {  
        // child (new process)  
        printf("hello, I am child (pid:%d)\n", (int) getpid());  
   sleep(1);  
    } else {  
        // parent goes down this path (original process)  
        int wc = wait(NULL);  
        printf("hello, I am parent of %d (wc:%d) (pid:%d)\n",  
          rc, wc, (int) getpid());  
    }  
    return 0;  
}
```

在父亲进程中调用了wait，因此会延迟它的执行，等到子进程执行完毕后，才会返回到父进程。如果父进程碰巧先运行，它会马上调用wait()。该系统调用会在子进程运行结束后才返回

# exec()
这个系统调用可以让子进程执行与父进程不同的程序。