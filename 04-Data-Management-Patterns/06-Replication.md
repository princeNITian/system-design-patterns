# Replication

## Introduction

Replication is a data management pattern where **the same data is copied from one database to one or more replica databases**.

Its primary purpose is to improve **availability, fault tolerance, and read scalability** by maintaining multiple copies of the same data.

The main goals of the Replication pattern are:

- Improve read performance.
- Increase system availability.
- Provide fault tolerance.
- Support disaster recovery.

---

## Why was it Introduced?

As applications grow, a single database becomes a bottleneck.

Problems include:

- Too many read requests.
- Single point of failure.
- Limited availability.

Instead of serving all traffic from one database, replicas are created.

```text
Application

      |

      ▼

Primary Database

      |

Thousands of Read Requests
```

Replication distributes read traffic across multiple databases.

---

## Architecture Diagram

```text
                Write

                  |

                  ▼

          Primary Database

          /       |       \

         ▼        ▼        ▼

    Replica 1  Replica 2  Replica 3

         ▲        ▲        ▲

         |        |        |

      Read Requests
```

The primary database handles writes, while replicas primarily handle reads.

---

## How It Works

The communication flow:

```text
1. Application writes data to the Primary Database.

2. Primary commits the transaction.

3. Changes are replicated to Replica Databases.

4. Applications send read requests to replicas.

5. Replicas return query results.
```

Example:

```text
Customer Places Order

        |

Primary Database

        |

Replicate Changes

        |

Read from Replicas
```

---

# Core Components

## 1. Primary Database

Handles all write operations.

Also called:

- Leader
- Master

---

## 2. Replica Database

Maintains a copy of the primary database.

Also called:

- Follower
- Secondary
- Read Replica

---

## 3. Replication Process

Copies changes from the primary to replicas.

---

## 4. Read Routing

Applications or load balancers direct read requests to replicas.

---

# Core Characteristics

## 1. Data Duplication

Multiple databases store identical data.

---

## 2. Read Scaling

Read traffic is distributed across replicas.

---

## 3. Single Write Node

Writes are generally performed on the primary database.

---

## 4. Fault Tolerance

Replicas improve system resilience.

---

## 5. Eventual Consistency

Replicas may briefly lag behind the primary.

---

# Types of Replication

## 1. Synchronous Replication

The primary waits for replicas to confirm the write before completing the transaction.

Advantages:

- Strong consistency.

Disadvantages:

- Higher write latency.

---

## 2. Asynchronous Replication

The primary acknowledges the write immediately and replicas are updated afterward.

Advantages:

- Better write performance.

Disadvantages:

- Temporary replication lag.

---

# Advantages

## 1. Improved Read Performance

Multiple replicas serve read requests.

---

## 2. Higher Availability

If one replica fails, others continue serving reads.

---

## 3. Fault Tolerance

Data exists in multiple locations.

---

## 4. Disaster Recovery

Replicas can be promoted if the primary fails.

---

## 5. Better Scalability

Read capacity increases by adding replicas.

---

# Disadvantages

## 1. Replication Lag

Replicas may temporarily contain stale data.

---

## 2. Increased Storage

Each replica stores a full copy of the data.

---

## 3. Failover Complexity

Promoting a replica requires coordination.

---

## 4. Write Bottleneck

Writes still go through the primary in primary-replica architectures.

---

## 5. Operational Overhead

Replication health and synchronization must be monitored.

---

# Real-World Examples

## E-Commerce

- Primary → Order updates.
- Replicas → Product searches and order history.

---

## Banking

Primary handles:

- Transactions.

Replicas handle:

- Balance inquiries.
- Statement generation.

---

## Social Media

Primary:

- Create posts.
- Like posts.

Replicas:

- News Feed.
- User profiles.
- Search.

---

## Content Platforms

Serve millions of read requests from replicas while writes go to the primary.

---

# When to Use

Use Replication when:

- Read traffic is much higher than write traffic.
- High availability is required.
- Disaster recovery is important.
- Multiple copies of data improve reliability.

---

# When NOT to Use

Avoid Replication when:

- Write throughput is the primary bottleneck.
- Immediate consistency across all nodes is mandatory.
- Storage overhead is unacceptable.

---

# Comparison

| Feature | Replication | Sharding |
|---|---|---|
| Data Stored | Same data on every replica | Different data on each shard |
| Purpose | Read scalability & availability | Write scalability & data partitioning |
| Read Scaling | High | Moderate to High |
| Write Scaling | Limited | High |
| Fault Tolerance | High | Depends on implementation |

---

# Interview Questions

## 1. What is Replication?

A pattern that copies data from one database to one or more replica databases.

---

## 2. Why is Replication used?

To improve read scalability, availability, and fault tolerance.

---

## 3. What is replication lag?

The delay between a successful write on the primary database and the time that change becomes visible on replicas.

---

## 4. What is the difference between synchronous and asynchronous replication?

Synchronous replication waits for replicas before confirming a write.

Asynchronous replication confirms the write immediately and updates replicas later.

---

## 5. Where is Replication commonly used?

- Relational databases.
- NoSQL databases.
- Cloud-managed databases.
- Large-scale distributed systems.

---

# Key Takeaways

- Replication maintains multiple copies of the same data.
- It improves read performance and system availability.
- Primary databases usually handle writes, while replicas handle reads.
- Replication introduces eventual consistency due to possible lag.
- It is a foundational pattern for highly available distributed databases.

---

## Previous & Next

← Previous: [Materialized View](05-Materialized-View.md)

→ Next: [Sharding](07-Sharding.md)