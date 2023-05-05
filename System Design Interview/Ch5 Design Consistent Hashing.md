### Why Consistent Hashing
In order to distribute requests / data efficiently and evenly across servers.

### Definition of Consistent Hashing
With k number of keys, and n number of slots, only k/n keys need to be remapped on average.

### Some Definitions About Consistency
#### N = The number of replicas.

#### W = A write quorum of size W.
For a write operation to be considered as successful, it must be acknowledged from W **replicas**.
#### R = A read quorum of size R.
For a read operation to be considered as successful, it must wait for responses from at least R **replicas**.

The configuration of W, R and N is a typical tradeoff between **latency** and **consistency**.



