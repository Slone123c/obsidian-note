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

#### UUID
UUID is a 128-bit number used to identify information in computer systems.
- **Pros**
	- No coordination between servers is needed. No synchronization issues.
	- Easy to scale. ID generator can easily scale with web servers.
- **Cons**
	- 128 bits long
	- IDs do not go up with time
	- IDs could be non-numeric

#### Ticket Server
To use a centralized auto_increment feature in a single datavase server(Ticket Server).
- **Pros**
	- Numeric IDs
	- Easy to implement, and it works for small to medium-scale applications.
- **Cons**
	- If the ticket server goes down, all systems that depend on it will face issues. Multiple ticket servers will introduce new challenges such as synchronization.

#### Twitter snowflake approach
To divide an ID into different sections.
![[Pasted image 20230507183347.png]]
- Sign bit: 1 bit. It will always be 0. This is reserved for future uses. It can potentially be used to distinguish between signed and unsigned numbers.
- Timestamp: 41 bits. Milliseconds since the epoch or custom epoch. We use Twitter snowflake default epoch 1288834974657, equivalent to Nov 04, 2010, 01:42:54 UTC.
- Datacenter ID: 5 bits, which gives us 2 ^ 5 = 32 datacenters.
- Machine ID: 5 bits, which gives us 2 ^ 5 = 32 machines per datacenter.
- Sequence number: 12 bits. For every ID generated on that machine/process, the sequence number is incremented by 1. The number is reset to 0 every millisecond.