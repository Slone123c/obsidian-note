Data are store in a key-value pair.

### Design A key-value store
It should be able to support these operations:
1. put(key,value)
2. get(key,value)

### Tradeoffs in Design
In each design, we need to achieve a balance among **read, write and memory** usage. Also, there is a choice between **consistency** and **availability**

### Design Following Characteristics
- The size of a key-value pair is small: less than 10 KB.
- Ability to store big data.
- High availability: The system responds quickly, even during failures.
- High scalability: The system can be scaled to support large data set.
- Automatic scaling: The addition/deletion of servers should be automatic based on traffic.
- Tunable consistency.
- Low latency.
### CAP theorem
- Consistency
	- In a distributed system, all nodes have the same view of data at the same time.
	- Any changes made to data must be propagated to all nodes in a timely manner.
	- Any conflicts must be resolved to ensure that the data remains consistent across all nodes.
- Availability
	- The system remains operational and responsive at all times, even in the face of failures or network issue.
	- Users should be able to access the syste
- Partition Tolerance
![[Pasted image 20230502194623.png]]