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
	- Users should be able to access the system even if some nodes are down.
- Partition Tolerance
	- A partition means a communication break between two nodes.
	- Partition Tolerance means the system continues to work despite the network partitions.
***
![[Pasted image 20230502194623.png]]

- Key-value stores are classified based on the two CAP characteristics they have.
	- CP(Consistency and Partition Tolerance)
	- AP(Availability and Partition Tolerance)
	- CA(Consistency and Availability)
		- In the event of a network partition or other types of failures that causes the system to separate, the CA system would not be able to maintain Consistency or Availability.

