# Consistent Hashing

## Introduction

Consistent Hashing is a scalability pattern used in distributed systems to efficiently distribute data across multiple servers while minimizing data movement when servers are added or removed.

It is commonly used in:

- Distributed caches.
- NoSQL databases.
- Load balancing.
- Distributed storage systems.

The main goals of consistent hashing are:

- Even data distribution.
- Minimal data redistribution.
- Better scalability.
- Efficient node management.

---

## Why was it Introduced?

Traditional hashing distributes data using a formula like:

```text
server = hash(key) % number_of_servers
```

Example:

```text
hash(user123) % 3

        |

        ▼

     Server 2
```

This works well until servers change.

---

## Problem With Traditional Hashing

Assume:

```text
Current Servers:

Server 1
Server 2
Server 3
```

Hash:

```text
hash(key) % 3
```

Now add another server:

```text
Server 1
Server 2
Server 3
Server 4
```

The formula changes:

```text
hash(key) % 4
```

Most keys are mapped to different servers.

Result:

```text
Before:

User A → Server 1


After:

User A → Server 3
```

Problems:

- Massive data movement.
- Cache misses increase.
- System performance decreases.

Consistent hashing solves this problem.

---

# How Consistent Hashing Works

Instead of directly mapping keys to servers, consistent hashing creates a virtual circular hash space.

This is called a:

**Hash Ring**

---

## Hash Ring

```text
                 0

          Server A


    Server D          Server B


          Server C


                360
```

The hash space is represented as a circle.

---

## Server Placement

Servers are hashed and placed on the ring.

Example:

```text
hash(Server A) → Position 50

hash(Server B) → Position 150

hash(Server C) → Position 250
```

---

## Data Placement

Keys are hashed and placed on the ring.

The key belongs to the first server encountered clockwise.

Example:

```text
User123

   |

Hash

   |

Position 120

   |

Next Server Clockwise

   |

Server B
```

---

# Adding a New Server

Example:

Before:

```text
Server A

Server B

Server C
```

After:

```text
Server A

Server B

Server C

Server D
```

Only nearby keys move.

Example:

```text
Before:

User X → Server C


After:

User X → Server D
```

Most other data remains unchanged.

---

# Removing a Server

If a server fails:

```text
Server B ❌
```

Its keys move to the next available server.

Example:

```text
Server B data

        |

        ▼

Server C
```

Only affected data moves.

---

# Virtual Nodes

A problem with basic consistent hashing:

Some servers may receive more data than others.

Example:

```text
Server A

Large Data


Server B

Small Data
```

Virtual nodes solve this.

---

## Virtual Node Concept

Instead of one position, each server gets multiple positions.

Example:

```text
Server A

A1
A2
A3


Server B

B1
B2
B3
```

Benefits:

- Better distribution.
- Reduced hotspots.
- Improved balancing.

---

# Core Characteristics

## 1. Minimal Data Movement

Only a small portion of data moves when nodes change.

---

## 2. Distributed Data Placement

Data is automatically assigned to nodes.

---

## 3. Horizontal Scalability

New nodes can be added easily.

---

## 4. Fault Tolerance

Failed nodes can be bypassed.

---

## 5. Decentralized Routing

Nodes can determine data ownership.

---

# Advantages

## 1. Easy Scaling

Adding servers requires minimal redistribution.

---

## 2. High Availability

Failures affect only a portion of data.

---

## 3. Better Cache Efficiency

Reduces unnecessary cache invalidation.

---

## 4. Supports Large Distributed Systems

Works well with thousands of nodes.

---

## 5. Reduces Network Transfer

Less data migration during changes.

---

# Disadvantages

## 1. Implementation Complexity

More complex than simple hashing.

---

## 2. Uneven Distribution Without Virtual Nodes

Poor distribution may create hotspots.

---

## 3. Additional Routing Logic

Systems need mechanisms to locate data.

---

## 4. Debugging Complexity

Data placement is less predictable.

---

# Real-World Examples

## Amazon Dynamo

Uses consistent hashing for distributing data across nodes.

---

## Cassandra

Uses consistent hashing to distribute partitions across cluster nodes.

Example:

```text
Node 1

Node 2

Node 3

Node 4
```

---

## Redis Cluster

Uses hash slots to distribute keys across nodes.

---

## Distributed Caching

Used to distribute cache keys across multiple cache servers.

Example:

```text
User Session

        |

Hash

        |

Cache Node Selection
```

---

# When to Use

Use consistent hashing when:

- Servers are frequently added or removed.
- Data is distributed across many nodes.
- Cache clusters need scalability.
- System requires high availability.
- Minimal data movement is important.

---

# When NOT to Use

Avoid consistent hashing when:

- Data is stored in a single database.
- Infrastructure rarely changes.
- Simple routing is sufficient.
- Strong ordering is required.

---

# Comparison

| Feature | Normal Hashing | Consistent Hashing |
|---|---|---|
| Node Addition | Large redistribution | Minimal movement |
| Node Removal | Large redistribution | Limited movement |
| Scalability | Poor | High |
| Complexity | Low | Higher |
| Distributed Systems | Limited | Excellent |

---

# Interview Questions

## 1. What is consistent hashing?

Consistent hashing is a technique that distributes data across nodes while minimizing redistribution when nodes are added or removed.

---

## 2. Why is normal hashing problematic?

Changing the number of servers changes the hash calculation and causes many keys to move.

---

## 3. What is a hash ring?

A hash ring is a circular representation of the hash space where nodes and keys are placed.

---

## 4. What are virtual nodes?

Virtual nodes are multiple logical positions assigned to each physical server to improve data distribution.

---

## 5. Where is consistent hashing used?

Common examples:

- Cassandra.
- DynamoDB-style systems.
- Redis Cluster.
- Distributed caching systems.

---

# Key Takeaways

- Consistent hashing solves the redistribution problem in distributed systems.
- It maps servers and keys onto a hash ring.
- Adding or removing nodes moves only a small amount of data.
- Virtual nodes improve load distribution.
- It is a fundamental pattern for scalable distributed architectures.

---

## Previous & Next

← Previous: [Connection Pooling](10-Connection-Pooling.md)

→ Next: [Geo Replication](12-Geo-Replication.md)