# Consistent Hashing

## Introduction

Consistent Hashing is a data management pattern used to **distribute data evenly across multiple nodes while minimizing data movement when nodes are added or removed**.

Unlike traditional hashing, where adding or removing a server causes most data to be remapped, Consistent Hashing ensures that only a small portion of the data needs to move.

The main goals of Consistent Hashing are:

- Evenly distribute data.
- Minimize data movement.
- Improve scalability.
- Support dynamic cluster membership.

---

## Why was it Introduced?

Traditional hash-based partitioning works well until the number of servers changes.

Example:

```text
Shard = Hash(Key) % 4
```

If a fifth server is added:

```text
Shard = Hash(Key) % 5
```

Almost every key maps to a different server, causing massive data migration.

Consistent Hashing solves this by moving only the keys affected by the added or removed node.

---

## Architecture Diagram

```text
              Hash Ring

                  ○

        Node A         Node B

      ○                   ○

         \               /

          \             /

           ○---------○

        Node D      Node C


Keys are placed on the ring and assigned
to the next node in the clockwise direction.
```

---

## How It Works

The communication flow:

```text
1. Hash each server onto a hash ring.

2. Hash each data key onto the same ring.

3. Move clockwise from the key.

4. Store the key on the first server encountered.

5. If a server is added or removed,
   only nearby keys are reassigned.
```

Example:

```text
User123

      |

Hash(User123)

      |

Position on Ring

      |

Next Clockwise Node

      |

Store Data
```

---

# Core Components

## 1. Hash Ring

A circular hash space where both nodes and data keys are placed.

---

## 2. Nodes

Servers responsible for storing data.

Examples:

- Database servers
- Cache servers
- Storage nodes

---

## 3. Keys

Business data mapped onto the ring.

Examples:

- User IDs
- Session IDs
- Cache Keys

---

## 4. Hash Function

Generates positions for both nodes and keys on the hash ring.

---

## 5. Virtual Nodes

Multiple logical positions assigned to each physical server to improve load distribution.

---

# Core Characteristics

## 1. Minimal Data Movement

Only a small percentage of keys move when cluster membership changes.

---

## 2. Dynamic Scalability

Servers can be added or removed with minimal disruption.

---

## 3. Even Distribution

Keys are spread more evenly across nodes, especially when using virtual nodes.

---

## 4. Fault Tolerance

If a node fails, only its assigned keys are redistributed.

---

## 5. Decentralized Routing

Any client can determine the correct node using the same hash function.

---

# Advantages

## 1. Minimal Rebalancing

Adding or removing nodes affects only a small portion of the data.

---

## 2. Excellent Scalability

Clusters can grow without massive data migration.

---

## 3. Better Availability

Node failures impact only part of the key space.

---

## 4. Efficient Load Distribution

Virtual nodes help balance uneven workloads.

---

## 5. Widely Used

Adopted in many distributed databases and caching systems.

---

# Disadvantages

## 1. Increased Complexity

More complex than simple modulo-based hashing.

---

## 2. Requires Virtual Nodes

Without virtual nodes, data distribution may become uneven.

---

## 3. Data Migration

Some data still needs to move when nodes change.

---

## 4. Hotspots

Poor key distribution can overload certain nodes.

---

## 5. Operational Challenges

Monitoring and balancing large clusters require additional tooling.

---

# Real-World Examples

## Distributed Caching

Cache keys are distributed across cache servers.

Examples:

- Redis Cluster
- Memcached

---

## NoSQL Databases

Data is partitioned across database nodes.

Examples:

- Apache Cassandra
- Amazon DynamoDB

---

## Distributed Storage

Files are distributed across storage nodes.

---

## Content Delivery Networks (CDNs)

Content is mapped efficiently across edge servers.

---

# When to Use

Use Consistent Hashing when:

- Nodes are frequently added or removed.
- Large-scale distributed storage is required.
- Building distributed caches.
- Minimizing data migration is important.

---

# When NOT to Use

Avoid Consistent Hashing when:

- The system uses a single database.
- Cluster membership rarely changes.
- Simple partitioning is sufficient.

---

# Comparison

| Feature | Traditional Hashing | Consistent Hashing |
|---|---|---|
| Data Movement | High | Low |
| Scalability | Moderate | High |
| Node Addition | Rehash almost all data | Move only affected keys |
| Node Removal | Rehash almost all data | Redistribute nearby keys |
| Complexity | Lower | Higher |

---

# Interview Questions

## 1. What is Consistent Hashing?

A pattern that distributes data across nodes while minimizing data movement when nodes are added or removed.

---

## 2. Why is Consistent Hashing better than modulo hashing?

Because adding or removing nodes affects only a small portion of the data instead of requiring nearly all keys to be remapped.

---

## 3. What is a hash ring?

A circular hash space where both nodes and data keys are mapped.

---

## 4. What are virtual nodes?

Multiple logical positions assigned to a physical server to achieve a more even distribution of data.

---

## 5. Where is Consistent Hashing commonly used?

- Distributed caches.
- NoSQL databases.
- Distributed storage systems.
- Large-scale cloud platforms.

---

# Key Takeaways

- Consistent Hashing minimizes data movement when cluster membership changes.
- Data and servers are mapped onto a hash ring.
- Keys are assigned to the next clockwise node.
- Virtual nodes improve load balancing.
- It is a foundational technique in modern distributed systems.

---

## Previous & Next

← Previous: [Sharding](07-Sharding.md)

→ Next: [Data Lake](09-Data-Lake.md)