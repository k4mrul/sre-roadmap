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

* _Cache_
  * When to use a cache
  * Cache-aside vs. read-through
  * Eviction policy
  * Refresh-ahead
  * Write-through vs. write-back
  * Distributed cache
  * Performance cache vs. capacity cache
* _Databases_
  * _Different types of databases_
    * NoSQL vs. SQL databases
    * Relational vs. document
    * Column-oriented databases
    * Graph databases
    * Vector database
    * Objects-based storage
  * ACID
  * _Partitioning_
    * Criteria
    * Methods
    * Replication vs. partition
  * Hotspot
  * CALM theorem
  * CAP theorem
  * PACELC theorem
  * Cardinality
  * Chain replication
  * Consensus
  * Concurrency control
  * Consistency models
  * Isolation levels
  * Serializability
  * Linearizability
  * CRDT
  * _Indexes_
    * Tradeoff
    * Primary vs. secondary indexes
  * Denormalization
  * View & materialized view
  * Transaction
  * Distributed transactions downsides
  * Strategies to handle rebalancing
  * Leader election
  * MVCC
  * N+1 select problem
  * Quorum
  * Raft
  * Read repair
  * Single-leader, multi-leader, leaderless replication
  * Split-brain
  * 2PC
  * 3PC
  * WAL
  * Write and read amplification
* _Data structure_
  * _Probabilistic data structures_
    * Bloom filter
    * Count-min sketch
    * HyperLogLog
  * _Storage_
    * LSM tree
    * B-tree
    * SSTable
      
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
