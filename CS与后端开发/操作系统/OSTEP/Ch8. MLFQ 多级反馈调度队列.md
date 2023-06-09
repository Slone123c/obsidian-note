● 规则1：如果A的优先级 > B的优先级，运行A（不运行B）。
● 规则2：如果A的优先级 = B的优先级，轮转运行A和B。
● 规则3：工作进入系统时，放在最高优先级（最上层队列）。
● 规则 4：一旦工作用完了其在某一层中的时间配额（无论中间主动放弃了多少次CPU），就降低其优先级（移入低一级队列）。
● 规则5：经过一段时间S，就将系统中所有工作重新加入最高优先级队列。

通过观察工作的运行来给出对应的优先级，使得MLFQ可以满足各种工作的需求，因此许多系统用MLFQ作为基础调度程序。
# 问题
1．只用两个工作和两个队列运行几个随机生成的问题。针对每个工作计算MLFQ的执行记录。限制每项作业的长度并关闭I/O，让你的生活更轻松。

2．如何运行调度程序来重现本章中的每个实例？

3．将如何配置调度程序参数，像轮转调度程序那样工作？

4．设计两个工作的负载和调度程序参数，以便一个工作利用较早的规则4a和4b（用-S标志打开）来“愚弄”调度程序，在特定的时间间隔内获得99%的CPU。

5．给定一个系统，其最高队列中的时间片长度为10ms，你需要如何频繁地将工作推回到最高优先级级别（带有-B标志），以保证一个长时间运行（并可能饥饿）的工作得到至少5%的CPU？

6．调度中有一个问题，即刚完成I/O的作业添加在队列的哪一端。-I标志改变了这个调度模拟器的这方面行为。尝试一些工作负载，看看你是否能看到这个标志的效果。