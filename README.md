# SRE Roadmap

An opinionated roadmap to become an SRE (Concepts > Tools)


### **Distributed Computing Concepts**

1. **Fallacies of distributed computing**: These are common misconceptions, like:
   - The network is reliable.
   - Latency is zero.
   - Bandwidth is infinite.
   - The network is secure, etc.

2. **Synchronous vs. Asynchronous**:
   - **Synchronous**: Operations happen one after the other, and each step waits for the previous one to finish.
   - **Asynchronous**: Steps can happen independently; one doesn’t need to wait for the other to finish.

3. **Event log vs. Message queue**:
   - **Event log**: Keeps a permanent record of events in order.
   - **Message queue**: Sends messages between systems, and messages are typically processed and then removed.

4. **Exactly-once delivery**: A guarantee that a message or action will only be processed one time, no more, no less.

5. **Different types of message failure**:
   - **Message loss**: A message gets lost in transit.
   - **Duplicate message**: The same message is received more than once.
   - **Out-of-order delivery**: Messages arrive in a different order than they were sent.

6. **Orchestration vs. Choreography**:
   - **Orchestration**: A central system controls the interactions between services.
   - **Choreography**: Services interact with each other without a central controller, each knowing what to do.

7. **Causality**: Understanding how one event causes another, especially in distributed systems, where things don’t always happen in sequence.

8. **CDN (Content Delivery Network)**: A system of servers spread across the world to deliver content faster to users based on their location.

9. **Hashing**: A way to convert data into a fixed-size string of characters, usually for fast lookups.

10. **Consistent hashing**: A technique used to evenly distribute data across servers in a way that minimizes data movement when servers are added or removed.

11. **Geohashing**: A method to encode geographic locations (like coordinates) into short strings for easy comparison and searching.

12. **Perfect hashing**: A way of hashing where no two different inputs map to the same output (no collisions).

13. **Read-heavy vs. write-heavy impacts**:
    - **Read-heavy**: More reading (retrieving) data than writing (changing) it.
    - **Write-heavy**: More writing (changing data) than reading it. Each affects how you design and optimize a system.

14. **Federation**: A system design where multiple independent systems work together but remain autonomous.

15. **Latency**: The time delay between a request and the system’s response.

16. **Latency, throughput, goodput**:
    - **Latency**: The delay in getting a response.
    - **Throughput**: The amount of data processed in a given time.
    - **Goodput**: The amount of useful data that is processed, excluding things like retries or overhead.

17. **Latency numbers every programmer should know**: Common benchmarks for how long certain operations take, like reading from RAM vs. disk or across a network.

18. **How to prevent latency variability**: Use techniques like load balancing, caching, and avoiding overloaded systems to reduce unpredictable delays.

19. **Tail latency**: The slowest response time experienced by a small percentage of users, usually due to outliers.

20. **How to reduce sharing**: Minimize the number of resources (like memory, files) shared between processes to avoid delays from waiting for access.

21. **Idempotency**: The ability to perform the same operation multiple times without changing the result beyond the first attempt.

22. **Load balancer**: A system that distributes traffic across multiple servers to prevent any one server from being overwhelmed.

---

### **Load Balancer Concepts**

1. **Layer 4 vs. Layer 7 load balancer**:
   - **Layer 4**: Distributes traffic based on network information like IP addresses and ports (lower level).
   - **Layer 7**: Distributes traffic based on application-level information like HTTP requests (higher level).

2. **Liveness vs. Safety properties**:
   - **Liveness**: Guarantees that something good eventually happens (e.g., the system will eventually respond).
   - **Safety**: Guarantees that something bad will not happen (e.g., the system won’t crash).

---

### **Microservices Concepts**

1. **Microservices pros**: Flexibility, scalability, independent deployment.
2. **Microservices cons**: Complexity, harder to manage and debug, need for effective communication between services.

3. **REST**: A way for services to communicate over HTTP, using standard methods like GET, POST, and DELETE.

4. **gRPC**: A faster, more efficient alternative to REST that uses binary data instead of text for communication between services.

5. **Service mesh**: A network layer that helps manage communication, security, and monitoring between microservices.

---

### **State and Time Concepts**

1. **Source of truth**: The authoritative source of data that other systems can rely on to be correct.

2. **Stateful vs. Stateless**:
   - **Stateful**: Keeps track of information (state) across requests.
   - **Stateless**: Does not keep track of past requests; every interaction is independent.

3. **Total vs. Partial order**:
   - **Total order**: All events are arranged in one single sequence.
   - **Partial order**: Only some events are arranged in sequence, not all.

4. **Why can’t we rely on the system clock in distributed systems**: Clocks can drift, and different machines may have slightly different times, which can lead to inconsistencies.

5. **Vector clock**: A way of tracking the order of events across multiple systems to maintain consistency.

---

### **Cache Concepts**

1. **Cache**: A way to store data temporarily so it can be accessed more quickly.

2. **When to use a cache**: When you need to access data frequently and want to reduce the time and resources needed to retrieve it from the main source.

3. **Cache-aside vs. Read-through**:
   - **Cache-aside**: The application checks the cache first, and if the data isn’t there, it fetches it from the main source and stores it in the cache.
   - **Read-through**: The cache is responsible for fetching and storing the data from the main source when needed.

4. **Eviction policy**: Rules for deciding which data to remove from the cache when it’s full. Examples: LRU (Least Recently Used), LFU (Least Frequently Used).

5. **Refresh-ahead**: A strategy where the cache preemptively updates data before it expires so users always get fresh data.

6. **Write-through vs. Write-back**:
   - **Write-through**: Data is written to the cache and the main source at the same time.
   - **Write-back**: Data is written to the cache first and only written to the main source later, usually when the cache is full.

7. **Distributed cache**: A cache spread across multiple machines to handle larger datasets and higher traffic.

8. **Performance cache vs. Capacity cache**:
   - **Performance cache**: Used to reduce response time by storing frequently accessed data.
   - **Capacity cache**: Used to store large amounts of data to offload the main system.



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
      
* * * * *

### **Reliability Concepts**

1\. **Availability**: This is the percentage of time a system is working and accessible. For example, if a website is available 99.9% of the time, it means it's only down 0.1% of the time.

2\. **Resiliency**: This means a system's ability to recover from failures. Even if something goes wrong, the system should bounce back quickly and work as expected.

3\. **Robustness**: This refers to how strong a system is against problems. A robust system can handle unexpected events or conditions without breaking down.

4\. **Fault-tolerance**: This is a system's ability to keep working even when parts of it fail. Imagine a car that still runs if one tire gets a puncture.

5\. **Reliability**: This is about how consistently a system performs without failures over time. A reliable system is one you can depend on to work smoothly.

### **Why is it wrong to target 100% availability?**

- Trying to achieve **100% availability** is very hard and expensive. It would require perfect hardware, software, and operations, which is unrealistic. Instead, most systems aim for a balance like 99.9% or 99.99% availability because aiming for perfection is impractical and often not worth the cost.

### **Blast radius**

- This term describes the extent of damage a failure can cause. A small blast radius means only a small part of the system is affected when something goes wrong.

### **Failure domain**

- This is a section of a system that can fail independently of others. By dividing a system into smaller failure domains, you can prevent one failure from bringing everything down.

### **Cascading failures**

- This is when one failure triggers another, which then causes more failures. It's like a row of dominoes falling---if one piece breaks, it can bring down the whole system.

### **Hard vs. soft dependencies**

- **Hard dependencies**: These are components the system must have to work. If they fail, the whole system fails.

- **Soft dependencies**: These are not critical. If they fail, the system can still function, though maybe not as well.

---

### **Scalability Concepts**

1\. **Knee point**: This is the point where adding more resources (like servers) results in decreasing returns. You're still getting better performance, but each added resource does less.

2\. **Ceiling**: This is the limit of scalability. Beyond this point, adding more resources doesn't help because the system can't handle any more growth.

3\. **Number one source of outages**: The most common cause of outages in systems is often human error---like misconfigurations, poor updates, or accidents.

4\. **Tail tolerance**: This refers to the ability to handle outlier scenarios, or the "long tail" of rare, extreme events that can cause system failures.

5\. **Toil**: Repetitive, manual work that doesn't add value but must be done to keep things running. Automating toil reduces effort and helps systems run more efficiently.

---

### **Patterns/Anti-patterns**

1\. **Bulkhead pattern**: This technique isolates parts of a system, so if one part fails, it won't take down the others. It's like putting different sections of a ship into watertight compartments.

2\. **Circuit breaker**: This pattern stops calls to a service when it's failing. It's like an electrical circuit breaker---when things go wrong, it "flips" to prevent further damage.

3\. **Exponential backoff**: If a service fails, this approach waits increasingly longer periods before retrying. Instead of retrying immediately, the system waits 1 second, then 2 seconds, then 4 seconds, and so on.

4\. **Jitter**: Adding random delays (jitter) to retry logic prevents systems from overwhelming each other with too many requests at once.

5\. **Graceful degradation**: When something goes wrong, the system continues to work at reduced capacity instead of completely failing. For example, a website might show a simplified version when there's too much traffic.

6\. **Load shedding**: This means selectively dropping or ignoring less important requests during high traffic to keep the system running.

7\. **Retry amplification**: This happens when too many retries make a situation worse. For example, if a service fails, lots of retries can overload the system even more.

8\. **Backpressure**: This refers to controlling the flow of data when a system is overwhelmed. It slows things down to prevent overloads.

9\. **Rate limiting**: This controls how many requests a system allows over a certain period. For example, a service might limit each user to 100 requests per minute to avoid overloading.

10\. **Request hedging**: Sending multiple requests to different servers to get a faster response. It's like sending an important message to multiple contacts to make sure someone answers quickly.

---

### **Practices**

1\. **Chaos engineering**: This is the practice of intentionally causing failures to test how well a system can handle them. The goal is to make systems more resilient by learning from these controlled failures.
    
## Observability

### **Monitoring vs. Observability**
- **Monitoring** refers to tracking predefined metrics or system states. It helps detect when something goes wrong but may not explain why.
- **Observability** is broader, focusing on understanding the internal state of systems through metrics, logs, and traces to diagnose complex issues.

### **Trace vs. Metric vs. Log**
- **Trace**: A record of requests as they travel through various services, giving insight into how different components interact.
- **Metric**: Quantitative data (e.g., CPU usage, latency) that helps measure system performance.
- **Log**: Text-based records of events or changes in the system, helpful for diagnosing specific incidents.

### **Golden Signals**
Four key metrics to monitor for system health:
1. **Latency**: Time taken for requests to be processed.
2. **Traffic**: The number of requests served.
3. **Errors**: The rate of failed requests.
4. **Saturation**: How full the system is (e.g., CPU or memory usage).

### **Observer Effect**
- The act of monitoring can affect the performance or behavior of the system itself, potentially skewing the data you are collecting.

### **Percentile**
- **Percentile** metrics (e.g., 90th or 95th percentile latency) are used to show how most users experience a system’s performance, which is often more insightful than averages.

### **Streetlight Anti-Method**
- The tendency to monitor only what’s easy to observe, leading to blind spots. It’s named after the “streetlight effect,” where someone looks for lost keys under a streetlight because that’s where it’s easiest to see, even if they might be elsewhere.

### **Time-Series Based Monitoring Lies**
- Relying only on averages in time-series data can hide spikes or anomalies. Observing patterns over time provides more accurate insights.

### **USE Method**
- A framework for monitoring system performance by checking for:
  - **Utilization**: How much of a resource is being used.
  - **Saturation**: How much demand exceeds the capacity.
  - **Errors**: Failures or issues in the system.

### **Main Metrics for Cache**
- **Hit Rate**: The percentage of cache requests that result in a hit.
- **Miss Rate**: The percentage of requests that require retrieving data from the source.
- **Eviction Rate**: How often data is removed from the cache to make space for new data.
- **Latency**: Time taken to retrieve data from the cache.

### **Why Be Careful with Averages?**
- **Average performance metrics** can be misleading, as they smooth out spikes and hide extremes. It’s better to look at percentiles to see how most users are impacted.

### **Alerting**
- **Alerting Strategy**: Define thresholds for critical conditions and set actionable, clear alerts to reduce noise.
- **Alert Fatigue**: Over-alerting causes teams to ignore or delay response, reducing effectiveness.
- **Characteristics of a Good Alert**:
  - Actionable: Should prompt a necessary response.
  - Clear: Indicate what’s wrong and the urgency.
  - Relevant: Focus on actual, critical issues.
  
### **Slow vs. Fast Burn Alerts**
- **Slow Burn Alerts**: Gradual issues that develop over time (e.g., resource leaks).
- **Fast Burn Alerts**: Immediate issues that require urgent action (e.g., system crashes).

This summary covers the key concepts, including various monitoring strategies, pitfalls, and methods to improve system observability and alerting practices.
     
Here's a comprehensive, organized summary of the key points:

---

### Rollout Concepts

- **Bake Time**: The period a new feature is monitored after deployment to ensure stability and correct functionality.

- **Feature Flag**: A toggle to enable or disable specific features without redeploying code, allowing gradual or controlled rollout.

- **Feature Freeze**: A temporary halt on new feature development to focus on stabilizing and finalizing current versions for release.

- **Rollout Supervision**: The process of monitoring the release for performance, user experience, and potential issues.

### Rollout Types

- **Blue-Green Rollout**: A deployment strategy where two identical environments (blue and green) are used. Traffic is routed to one environment while the other is prepared, allowing easy rollback if issues occur.

- **Canary Rollout**: A small portion of users initially receives the update. If successful, it's gradually released to the rest of the users, reducing risk.

- **Progressive Rollout**: Similar to a canary rollout but with controlled steps and monitoring to ensure each step performs as expected before proceeding.

- **Shadow Rollout**: The new version is deployed alongside the current version, receiving production traffic but not affecting users, useful for testing in live conditions.

---

### SLI, SLO, and SLA

- **SLI (Service Level Indicator)**: A quantitative measure of service performance (e.g., latency, uptime).

- **SLO (Service Level Objective)**: The target or goal for a specific SLI; it defines acceptable performance thresholds.

- **SLA (Service Level Agreement)**: A formal agreement between service providers and customers, with SLIs and SLOs as commitments, often legally binding.

#### Concepts

- **Error Budget**: The allowable margin within which SLOs can be missed, enabling teams to balance reliability with innovation.

- **KPIs vs. SLOs**: KPIs are general performance indicators, while SLOs are specific targets related to service reliability.

- **Benefits of SLO-Based Alerts**: Alerts based on SLOs focus on user experience, reducing noise and prioritizing impactful issues.

- **Exceeding SLOs**: Overachieving on SLOs can imply underutilization of resources or an overly conservative budget, limiting innovation.

- **SLOs for Data**: Key metrics include data freshness, completeness, and consistency, critical for data-dependent services.

- **SLOs for Mobile and Services**: These may address aspects like app responsiveness, network reliability, and service uptime.

---

### Containers and Container Orchestration

- **Containers**: Lightweight, isolated environments to run applications consistently across different infrastructures.

- **Container Orchestration**: Automates the deployment, scaling, and management of containers across clusters, typically handled by platforms like Kubernetes.

---

### Linux and Scripting

- **Filesystem**: Understanding the Linux filesystem is essential for managing files, permissions, and structures within a system.

- **Memory and Processes**: Efficient management of memory and processes is critical for system performance, particularly for services running in containers.

- **Resource Utilization**: Monitoring and optimizing resource usage helps maintain performance, especially under load.

- **Network**: Managing and troubleshooting network configurations is vital in containerized and orchestrated environments to ensure connectivity and data flow.

---
   
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
