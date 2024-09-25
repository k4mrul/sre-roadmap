# SRE Roadmap

An opinionated roadmap to become an SRE (Concepts > Tools)


### Fallacies of Distributed Computing

These are common misconceptions about distributed systems that can lead to design and implementation errors.

-   **Network is reliable:** Networks can experience failures like packet loss, delays, and disconnections.
-   **Latency is zero:** There's always a delay in communication between nodes in a distributed system.
-   **Bandwidth is infinite:** Bandwidth is limited, and excessive data can overwhelm networks.
-   **The network is secure:** Networks are vulnerable to attacks like hacking and data breaches.
-   **Topology is static:** Network topology can change dynamically due to failures or reconfigurations.

### Synchronous vs. Asynchronous

-   **Synchronous:** Communication requires a response before proceeding (e.g., RPC). This can be blocking and might lead to performance issues if the response is slow.
-   **Asynchronous:** Communication doesn't require an immediate response (e.g., messaging). This is often used for non-critical tasks or when the response time is uncertain.

### Event Log vs. Message Queue

-   **Event Log:** Stores a sequence of events for auditing and replay. This is useful for tracking the history of a system and for debugging or troubleshooting issues.
-   **Message Queue:** Temporarily stores messages for later processing. This is used for decoupling components, handling peak loads, and implementing asynchronous workflows.

### Exactly-once Delivery

Ensures that a message is delivered exactly once, even in the face of failures. This is important for ensuring data consistency and preventing duplicate processing.

### Different Types of Message Failure

-   **Loss:** Message is not received.
-   **Duplication:** Message is received multiple times.
-   **Out-of-order:** Messages are received in a different order than sent.

### Orchestration vs. Choreography

-   **Orchestration:** A central entity controls the flow of a distributed process. This can be more complex to manage but provides better control.
-   **Choreography:** Services communicate directly and autonomously. This is often used for loosely coupled systems and can be more scalable but can be harder to reason about.

### Causality

Ensures that events in a distributed system happen in a consistent order. This is important for ensuring data consistency and preventing anomalies.

### CDN (Content Delivery Network)

Distributes content across multiple servers to improve performance and availability. This is often used for static content like images, CSS, and JavaScript.

### Hashing

Maps large data sets to smaller ones for efficient storage and retrieval. This is used for indexing data, caching, and load balancing.

### Consistent Hashing

Ensures that only a small number of keys are affected when a node is added or removed. This is used for distributed caching and data partitioning.

### Geohashing

Maps geographic coordinates to a fixed-length string for efficient indexing and querying. This is used for location-based services and spatial data.

### Perfect Hashing

A hashing technique that guarantees no collisions. This is used for scenarios where collisions are unacceptable, such as in compilers and database indexes.

### Read-heavy vs. Write-heavy Impacts

-   **Read-heavy:** Optimized for frequent reads, often using caching.
-   **Write-heavy:** Optimized for frequent writes, often using replication and batching.

### Federation

A system where multiple autonomous entities collaborate. This is used for large-scale systems like federated learning and blockchain networks.

### Latency

The time it takes for a request to be processed and a response to be received.

### Latency, Throughput, Goodput

-   **Latency:** The time it takes to complete a task.
-   **Throughput:** The rate at which tasks are completed.
-   **Goodput:** The useful data transferred per unit time.

### Latency Numbers Every Programmer Should Know

-   **Network latency:** Typically around 1-10 milliseconds.
-   **Disk access latency:** Typically around 10-20 milliseconds.
-   **Database query latency:** Varies widely depending on complexity.

### How to Prevent Latency Variability

-   **Caching:** Store frequently accessed data in memory.
-   **Batching:** Group multiple operations together to reduce overhead.
-   **Asynchronous processing:** Defer non-critical tasks to improve responsiveness.

### Tail Latency

The latency of the slowest requests in a distribution. This is often used to measure the performance of a system under load.

### How to Reduce Sharing

-   **Vertical scaling:** Increase resources for individual components.
-   **Horizontal scaling:** Distribute load across multiple instances.
-   **Partitioning:** Divide data into smaller, more manageable chunks.

### Idempotency

An operation that can be performed multiple times without changing the result. This is important for fault tolerance and retry mechanisms.

### Load Balancer

Distributes traffic across multiple servers to improve performance and availability.

### Layer 4 vs. Layer 7 Load Balancer

-   **Layer 4:** Balances traffic based on IP address and port.
-   **Layer 7:** Balances traffic based on application-level information.

### Liveness vs. Safety Properties

-   **Liveness:** Guarantees that something good will eventually happen (e.g., a message will be delivered).
-   **Safety:** Guarantees that nothing bad will happen (e.g., a message will not be delivered multiple times).

### Microservices: Pros and Cons

-   **Pros:** Scalability, flexibility, independent development.
-   **Cons:** Complexity, increased overhead, coordination challenges.

### REST (Representational State Transfer)

An architectural style for building distributed systems using HTTP.

### gRPC (Google Remote Procedure Call)

A high-performance RPC framework that uses HTTP/2.

### Service Mesh

A dedicated infrastructure layer for managing service-to-service communication.

### Source of Truth

The authoritative data store for a particular piece of information.

### Stateful vs. Stateless

-   **Stateful:** Retains information about previous interactions.
-   **Stateless:** Does not retain information about previous interactions.

### Total vs. Partial Order

-   **Total order:** All elements can be compared.
-   **Partial order:** Some elements may not be comparable.

### Why Can't We Rely on the System Clock in Distributed Systems

-   **Clock skew:** Clocks on different machines may be out of sync.
-   **Clock drift:** Clocks may gradually become inaccurate over time.

### Vector Clock

A technique for determining the causal relationship between events in a distributed system.

### **Cache**

A cache is a temporary storage layer that keeps frequently accessed data closer to the user or application for faster retrieval.

-   **When to use a cache**: Use a cache when you need to speed up data access by reducing the time it takes to retrieve frequently requested data from a slower data store (like a database or external service).

-   **Cache-aside vs. read-through**:

    -   **Cache-aside**: The application is responsible for loading data into the cache and reading from it when necessary. If the cache misses (data not found), the app fetches it from the primary data store and then caches it.
    -   **Read-through**: The cache automatically loads data from the underlying data store when the data is missing, abstracting the fetching logic away from the application.
-   **Eviction policy**: Determines which data is removed from the cache when the cache is full. Common policies include Least Recently Used (LRU), First In First Out (FIFO), and Least Frequently Used (LFU).

-   **Refresh-ahead**: Preloads the cache with data that is expected to be requested soon, ensuring that it is ready when needed.

-   **Write-through vs. write-back**:

    -   **Write-through**: Data is written to both the cache and the main storage simultaneously.
    -   **Write-back**: Data is written only to the cache first, then written to the main storage later (potentially causing data loss in the case of failure).
-   **Distributed cache**: A cache spread across multiple servers to provide high availability and scalability, often used in large-scale applications.

-   **Performance cache vs. capacity cache**:

    -   **Performance cache**: Focuses on improving response times by caching frequently accessed data.
    -   **Capacity cache**: Focuses on reducing the load on the main storage by storing larger volumes of data temporarily.

* * * * *

### **Databases**

-   **Different types of databases**:

    -   **Relational databases** (SQL) store structured data in tables with predefined schemas (e.g., MySQL, PostgreSQL).
    -   **NoSQL databases** store unstructured, schema-less data in various formats (e.g., MongoDB for documents, Cassandra for wide-column stores).
-   **NoSQL vs. SQL databases**:

    -   **SQL** databases are table-based and support structured query languages.
    -   **NoSQL** databases offer flexibility in how data is stored (documents, key-value pairs, columns, graphs) and are better suited for large-scale, distributed, or rapidly changing datasets.
-   **Relational vs. document**:

    -   **Relational**: Data is stored in tables with rows and columns; highly structured (e.g., PostgreSQL).
    -   **Document**: Data is stored as semi-structured documents (JSON, BSON), offering flexibility for complex data types (e.g., MongoDB).
-   **Column-oriented databases**: Store data in columns rather than rows, optimizing read performance for analytical queries (e.g., Apache Cassandra, HBase).

-   **Graph databases**: Designed to store relationships between entities. Nodes represent entities, and edges represent relationships (e.g., Neo4j).

-   **Vector database**: Specialized for handling vector embeddings and performing efficient similarity searches (often used in AI applications).

-   **Object-based storage**: Stores data as objects with metadata, often used in cloud storage solutions (e.g., Amazon S3).

-   **ACID**: A set of properties that ensure reliable database transactions: **Atomicity, Consistency, Isolation, Durability**.

* * * * *

### **Partitioning**

-   **Partitioning criteria**: Strategies for splitting data across multiple partitions, such as by range, hash, or list, to improve scalability and performance.

-   **Partitioning methods**: Includes horizontal partitioning (sharding), vertical partitioning (splitting by columns), and composite partitioning (combining multiple strategies).

-   **Replication vs. partition**:

    -   **Replication**: Making copies of the same data across multiple nodes for fault tolerance.
    -   **Partitioning**: Dividing data into smaller pieces to distribute across nodes.
-   **Hotspot**: A situation where one partition receives more traffic than others, causing performance bottlenecks.

* * * * *

### **Theorems & Consistency Models**

-   **CALM theorem**: Consistency and Logical Monotonicity---if a system is monotonic, it can ensure consistency without coordination.

-   **CAP theorem**: In a distributed system, you can only have two of the following: **Consistency**, **Availability**, and **Partition tolerance**.

-   **PACELC theorem**: An extension of CAP that adds latency into the equation: "If there is a partition (P), a system must choose between availability (A) and consistency (C), but else (E), it must choose between latency (L) and consistency (C)."

-   **Cardinality**: The uniqueness of data values in a column. Higher cardinality means more unique values.

-   **Chain replication**: A technique where replicas form a chain, and updates propagate sequentially from one replica to the next.

* * * * *

### **Consensus & Concurrency**

-   **Consensus**: A protocol that ensures distributed systems agree on a single value or state (e.g., Paxos, Raft).

-   **Concurrency control**: Mechanisms that handle multiple transactions happening simultaneously to avoid conflicts (e.g., locks, timestamps).

-   **Consistency models**: Models that describe the rules and guarantees for reading and writing data in a distributed system (e.g., eventual consistency, strong consistency).

-   **Isolation levels**: Define the extent to which the operations of one transaction are isolated from others (e.g., read uncommitted, serializable).

-   **Serializability**: The strongest isolation level, ensuring that transactions occur as if they were executed serially.

-   **Linearizability**: A stronger form of consistency than serializability, ensuring that reads reflect the most recent writes across all nodes.

* * * * *

### **Data Structures & Indexes**

-   **CRDT**: Conflict-free Replicated Data Types allow distributed systems to converge to the same state without coordination.

-   **Indexes**: Data structures that improve query performance by allowing faster lookups. They come with trade-offs in terms of write performance and storage cost.

    -   **Primary vs. secondary indexes**: Primary indexes are based on the primary key, while secondary indexes can be created on other columns to optimize query performance.
-   **Denormalization**: Storing redundant data to improve read performance, at the cost of potential data inconsistency.

-   **View & materialized view**:

    -   **View**: A virtual table created from a query.
    -   **Materialized view**: A view whose data is stored and updated, offering faster reads at the cost of more complex writes.

* * * * *

### **Transactions**

-   **Distributed transactions downsides**: Complexity and performance issues due to the need for coordination between multiple systems.

-   **Strategies to handle rebalancing**: Techniques like consistent hashing, data movement minimization, and partition rebalancing are used to avoid disruptions during rebalancing in distributed systems.

-   **Leader election**: A process in distributed systems for selecting a leader node to manage coordination (e.g., Raft, Paxos).

-   **MVCC**: Multi-Version Concurrency Control allows multiple versions of data to be stored, improving read performance without locking.

-   **N+1 select problem**: A performance problem where one query leads to multiple additional queries, causing inefficiency.

* * * * *

### **Quorum & Replication**

-   **Quorum**: The minimum number of nodes that must agree for an operation (read/write) to succeed in a distributed system.

-   **Raft**: A consensus algorithm for managing replicated state machines, designed to be simpler than Paxos.

-   **Read repair**: Fixes inconsistencies between replicas by synchronizing the data when reads are made.

-   **Single-leader, multi-leader, leaderless replication**:

    -   **Single-leader**: One node is responsible for all writes.
    -   **Multi-leader**: Multiple nodes can handle writes, but conflicts can occur.
    -   **Leaderless**: Any node can handle writes, often leading to eventual consistency.
-   **Split-brain**: A situation where a network partition causes multiple nodes to think they are the leader, leading to inconsistency.

-   **2PC**: Two-Phase Commit protocol ensures atomic commits across multiple systems but can cause delays if any node is slow.

-   **3PC**: Three-Phase Commit extends 2PC by adding a pre-commit phase to reduce blocking, but is still vulnerable to certain failures.

* * * * *

### **Storage & Data Structures**

-   **WAL**: Write-Ahead Logging ensures data durability by logging changes before they are applied to the database.

-   **Write and read amplification**: Refers to the increased number of write or read operations compared to the original operation, often in storage systems like SSDs or databases.

-   **Probabilistic data structures**: Efficiently approximate answers to queries while using less memory. Common examples:

    -   **Bloom filter**: Used to test whether an element is in a set, with a possibility of false positives.
    -   **Count-min sketch**: Estimates the frequency of elements in a data stream, with some inaccuracies.
    -   **HyperLogLog**: Estimates the number of distinct elements in a dataset (cardinality).
-   **LSM tree**: Log-Structured Merge Tree is a data structure optimized for write-heavy workloads, often used in databases like Cassandra.

-   **B-tree**: A balanced tree data structure used in databases and file systems for efficient reads and writes.

-   **SSTable**: Sorted String Table is a file format used for storing key-value pairs in a sorted order, used by databases like Cassandra
      
## Reliability

* _Concepts_
  * Difference between availability, resiliency, robustness, fault-tolerance, and reliability
  * Why is it wrong to target 100% availability
  * Blast radius
  * Failure domain
  * Cascading failures
  * Hard vs. soft dependencies
  * _Scalability_
    * Concepts
    * Knee point
    * Ceiling
  * Number one source of outages
  * Tail tolerance
  * Toil
* _Patterns/Anti-patterns_
  * Bulkhead pattern
  * Circuit breaker
  * Exponential backoff
  * Jitter
  * Graceful degradation
  * Load shedding
  * Retry amplification
  * Backpressure
  * Rate limiting
  * Request hedging
* _Practices_
  * Chaos engineering 
    
## Observability
 
* _Concepts_
  * What's the difference between monitoring and observability
  * Trace vs. metric vs. log
  * Golden signals
  * Observer effect
  * Percentile
  * Streetlight anti-method
  * Time-series based monitoring lies
  * USE method
  * Main metrics for cache
  * Why should we be careful about average performance metrics
* _Alerting_
  * Alerting strategy
  * Alerting fatigue concept
  * Characteristic of a good alert
  * Slow vs. fast burn alert
     
## Rollout
 
* _Concepts_ 
  * Bake time
  * Feature flag
  * Feature freeze
  * Rollout supervision
* _Rollout types_
  * Blue green rollout
  * Canary rollout
  * Progressive rollout
  * Shadow rollout
  
## SLI/SLO/SLA

* _Concepts_
  * SLI vs. SLO vs. SLA
  * Error budget
* _SLO_
  * Difference between KPIs and SLOs
  * Benefits of having alerts based on SLOs
  * Why is exceeding an SLO not necessarily a good thing
  * SLO for data (freshness, completeness, consistency, etc.)
  * SLO for mobiles
  * SLO for services
     
## Container

* Container
* Container orchestration
   
## Linux

* Scripting
* Filesystem
* Memory
* Processes
* Resource utilization
* Network
   
## Network

* ARP protocol
* Bandwidth
* BGP
* CoDel
* CORS
* DNS
* Ping vs. heartbeat
* _TCP_
  * TCP vs. UDP
  * Congestion control
  * Connection backlog
  * Flow control
  * Handshake
* HTTP
* HTTP/2
* Head of line blocking
* Health checks: passive vs. active
* Internet model
* NTP
* OSI model
* Routers
* Switch
* Network topologies
* What happens if you type google.com in your browser
   
## Security
 
* Authentication
* Certificate
* Certificate authority
* Cipher
* Confidentiality
* Encryption
* TLS
* PKI
* Signature
   
## Analysis

* Core analysis loop
* Correlation vs. causation
* First principle
* Five whys technique
* _Incident management_
  * How to address an incident (assess, mitigate, resolve)
  * Incident roles
  * How to write a postmortem
  * 3C principles (Coordinate, Communicate, maintain Control)
  
## Other

* SRE role
* Version control

## Soft skills

* _Communication_
  * Writing
  * Oral
  * Presentation
  * The XY problem
* Collaboration
* Problem solving
* Curiosity
* Navigating ambiguity
* Staying humble
