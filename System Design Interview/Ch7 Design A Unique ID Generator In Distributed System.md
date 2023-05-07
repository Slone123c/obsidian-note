### Requirements of IDs
1. Unique
2. Numerical values only
3. Fit into 64-bit
4. Ordered by date

### Approaches to Generate Unique ID
1. Multi-master replication
2. Universally Unique Identifier (UUID)
3. Ticket Server
4. Twitter snowflake approach

#### Multi-master replication
Instead of increasing the next ID by 1, we increase it by k, where k is the number of database servers in use.
- **Drawbacks**
	- Hard to scale with multiple data centers
	- IDs do not go up with time accross multiple servers
	- It does not scale well when a server is added or removed