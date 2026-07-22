# Sharding

## Introduction

Sharding is a data management pattern where **a large database is horizontally partitioned into multiple smaller databases called shards**.

Each shard stores a **subset of the total data**, allowing the system to distribute storage and write workloads across multiple servers.

The main goals of the Sharding pattern are:

- Scale write operations.
- Distribute data across multiple databases.
- Eliminate storage bottlenecks.
- Improve overall scalability.

---

## Why was it Introduced?

As applications grow, a single database eventually reaches its limits.

Problems include:

- Storage capacity limits.
- High write traffic.
- Increasing query latency.
- Hardware limitations.

Instead of storing all records in one database, the data is divided into multiple shards.

```text
Users

1 - 1 Billion

        |

Single Database

        |

Performance Bottleneck
```

Sharding distributes both the data and workload.

---

## Architecture Diagram

```text
                Application

                     |

               Shard Router

      /-----------|-----------\

      ▼           ▼            ▼

   Shard 1     Shard 2      Shard 3

(User A-H)   (User I-P)   (User Q-Z)
```

Each shard stores a different portion of the data.

---

## How It Works

The communication flow:

```text
1. Client sends a request.

2. Shard Router determines the correct shard.

3. Request is routed to that shard.

4. The shard processes the request.

5. Response is returned to the client.
```

Example:

```text
User ID = 125

        |

Hash(User ID)

        |

Shard 2

        |

Retrieve User
```

---

# Core Components

## 1. Shards

Independent databases storing different subsets of data.

---

## 2. Shard Key

The attribute used to determine where data is stored.

Examples:

- User ID
- Customer ID
- Region
- Tenant ID

---

## 3. Shard Router

Routes requests to the appropriate shard based on the shard key.

---

## 4. Application

Interacts with the shard router rather than individual shards.

---

# Core Characteristics

## 1. Horizontal Partitioning

Data is divided across multiple databases.

---

## 2. Independent Storage

Each shard manages only its own data.

---

## 3. Write Scalability

Write traffic is distributed across shards.

---

## 4. Parallel Processing

Different shards process requests simultaneously.

---

## 5. Independent Scaling

Shards can often be scaled individually.

---

# Common Sharding Strategies

## 1. Range-Based Sharding

Data is partitioned using value ranges.

Example:

```text
Shard 1 → User ID 1–1,000

Shard 2 → User ID 1,001–2,000
```

---

## 2. Hash-Based Sharding

A hash function determines the target shard.

Example:

```text
Hash(User ID)

↓

Shard 3
```

---

## 3. Geographic Sharding

Data is partitioned by region.

Example:

```text
India

US

Europe
```

---

## 4. Directory-Based Sharding

A lookup service maps each record to its shard.

---

# Advantages

## 1. High Write Scalability

Write operations are distributed across multiple databases.

---

## 2. Better Storage Capacity

Data is spread across multiple servers.

---

## 3. Improved Performance

Each shard manages a smaller dataset.

---

## 4. Fault Isolation

A failure in one shard typically affects only part of the data.

---

## 5. Horizontal Growth

Additional shards can be added as the system grows.

---

# Disadvantages

## 1. Increased Complexity

Applications need shard routing logic.

---

## 2. Cross-Shard Queries

Queries involving multiple shards are more complex and slower.

---

## 3. Rebalancing Challenges

Adding or removing shards may require moving large amounts of data.

---

## 4. Uneven Data Distribution

Poor shard key selection can create hotspots.

---

## 5. Operational Overhead

Managing many database instances increases maintenance effort.

---

# Real-World Examples

## Social Media

Users are distributed across shards using User ID.

---

## E-Commerce

Customer or Order IDs determine the target shard.

---

## SaaS Platforms

Tenant data is partitioned across multiple shards.

---

## Gaming Platforms

Player accounts are distributed across regional shards.

---

# When to Use

Use Sharding when:

- The database has become too large for a single server.
- Write throughput is very high.
- Storage capacity must grow horizontally.
- Applications serve millions of users.

---

# When NOT to Use

Avoid Sharding when:

- The database is small.
- Most queries require data from multiple shards.
- Simplicity is more important than scalability.
- Vertical scaling is still sufficient.

---

# Comparison

| Feature | Replication | Sharding |
|---|---|---|
| Data Stored | Same data on every node | Different data on each shard |
| Primary Goal | Read scalability | Write scalability |
| Storage | Duplicate copies | Partitioned data |
| Write Scaling | Limited | High |
| Read Scaling | High | Moderate to High |

---

# Interview Questions

## 1. What is Sharding?

A pattern that horizontally partitions a database into multiple smaller databases called shards.

---

## 2. What is a shard key?

An attribute used to determine which shard stores a particular record.

---

## 3. Why is choosing the right shard key important?

A poor shard key can create uneven data distribution and overload specific shards.

---

## 4. How is Sharding different from Replication?

Replication copies the same data to multiple databases.

Sharding distributes different subsets of data across multiple databases.

---

## 5. Where is Sharding commonly used?

- Social media platforms.
- E-commerce systems.
- SaaS applications.
- Large-scale distributed databases.

---

# Key Takeaways

- Sharding horizontally partitions data across multiple databases.
- It primarily improves write scalability and storage capacity.
- Requests are routed using a shard key.
- Choosing the correct sharding strategy is critical for balanced performance.
- It is one of the most important scaling techniques for large distributed systems.

---

## Previous & Next

← Previous: [Replication](06-Replication.md)

→ Next: [Consistent Hashing](08-Consistent-Hashing.md)