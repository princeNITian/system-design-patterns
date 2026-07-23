# Quorum

## Introduction

Quorum is a distributed system pattern that **requires a minimum number of nodes to agree before a read or write operation is considered successful**.

Rather than requiring every node to participate, Quorum uses **majority agreement** to balance consistency, availability, and fault tolerance.

The main goals of Quorum are:

- Maintain data consistency.
- Tolerate node failures.
- Prevent conflicting updates.
- Improve availability while preserving correctness.

---

## Why was it Introduced?

Suppose data is replicated across three nodes.

```text
Node A

Node B

Node C
```

If a client writes only to Node A:

```text
Node A → Version 2

Node B → Version 1

Node C → Version 1
```

Different nodes now contain different versions of the data.

Quorum ensures that enough replicas participate in every operation so the latest data can always be determined.

---

## Architecture Diagram

```text
                Client

                   |

                   ▼

          Quorum Coordinator

         /        |        \

        ▼         ▼         ▼

     Node A    Node B    Node C

        ✓         ✓         ✗

      Majority Achieved
```

The operation succeeds because a majority of nodes responded.

---

## How It Works

The general flow:

```text
1. Client sends a read or write request.

2. Request is forwarded to multiple replicas.

3. Nodes respond.

4. Quorum requirement is evaluated.

5. Operation succeeds if the quorum is reached.
```

Example:

```text
Replication Factor (N) = 3

Write Quorum (W) = 2

Read Quorum (R) = 2
```

Since:

```text
R + W > N
```

the latest write can always be observed by a successful read.

---

# Quorum Terminology

## 1. Replication Factor (N)

The total number of replicas storing the same data.

Example:

```text
N = 3
```

---

## 2. Write Quorum (W)

The minimum number of replicas that must acknowledge a write.

Example:

```text
W = 2
```

---

## 3. Read Quorum (R)

The minimum number of replicas that must participate in a read.

Example:

```text
R = 2
```

---

## 4. Quorum Rule

To guarantee strong consistency:

```text
R + W > N
```

This ensures that every successful read overlaps with the most recent successful write.

---

# Core Characteristics

## 1. Majority-Based Decisions

Operations require acknowledgments from enough replicas to satisfy the quorum.

---

## 2. Fault Tolerance

Operations continue as long as the required number of replicas remain available.

---

## 3. Configurable Consistency

Different values of **R** and **W** provide different consistency and availability trade-offs.

---

## 4. Replicated Data

Multiple nodes maintain copies of the same data.

---

## 5. Overlapping Reads and Writes

Proper quorum configuration prevents stale reads.

---

# Advantages

## 1. Stronger Consistency

Clients can reliably observe the latest committed data.

---

## 2. High Availability

Operations can succeed even when some replicas fail.

---

## 3. Fault Tolerance

Node failures do not necessarily interrupt service.

---

## 4. Flexible Trade-Offs

Read-heavy and write-heavy workloads can use different quorum configurations.

---

## 5. Foundation for Distributed Databases

Many distributed databases rely on quorum-based replication.

---

# Disadvantages

## 1. Higher Latency

Operations wait for multiple replica acknowledgments.

---

## 2. Increased Network Traffic

Requests must be sent to several nodes.

---

## 3. Configuration Complexity

Poor quorum settings can reduce consistency or availability.

---

## 4. Temporary Unavailability

Operations may fail if the required quorum cannot be reached.

---

## 5. Conflict Resolution

Systems using weaker quorum settings may still require conflict resolution mechanisms.

---

# Real-World Examples

## Apache Cassandra

Uses configurable read and write quorum levels.

---

## Amazon DynamoDB

Supports strongly consistent reads and replicated storage across multiple nodes.

---

## Riak

Uses quorum-based replication for distributed key-value storage.

---

## Apache Couchbase

Uses replica-based reads and writes for fault tolerance.

---

# When to Use

Use Quorum when:

- Data is replicated across multiple nodes.
- Strong consistency is important.
- Node failures are expected.
- Distributed databases require fault tolerance.

---

# When NOT to Use

Avoid Quorum when:

- Single-node storage is sufficient.
- Maximum write throughput is more important than consistency.
- Eventual consistency without coordination is acceptable.

---

# Comparison

| Feature | Quorum | Leader-Based Replication |
|---|---|---|
| Decision Method | Majority Agreement | Leader Coordinates |
| Writes | Multiple Replicas | Leader First |
| Fault Tolerance | High | High |
| Latency | Higher | Lower |
| Consistency | Configurable | Strong (Leader Dependent) |

---

# Interview Questions

## 1. What is Quorum?

A distributed system pattern that requires a minimum number of replicas to participate before read or write operations succeed.

---

## 2. What do **N**, **R**, and **W** represent?

- **N** – Number of replicas
- **R** – Read quorum
- **W** – Write quorum

---

## 3. Why is the rule **R + W > N** important?

It ensures that every successful read overlaps with the latest successful write, preventing stale reads.

---

## 4. Which distributed databases commonly use Quorum?

- Apache Cassandra
- Amazon DynamoDB
- Riak
- Couchbase

---

## 5. What is the trade-off of using Quorum?

Improved consistency and fault tolerance at the cost of additional latency and communication.

---

# Key Takeaways

- Quorum requires majority participation for distributed operations.
- Read and write quorum sizes determine consistency guarantees.
- The rule **R + W > N** is fundamental for strong consistency.
- Quorum balances consistency, availability, and fault tolerance.
- It is widely used in replicated distributed databases.

---

## Previous & Next

← Previous: [Leader Election](02-Leader-Election.md)

→ Next: [Distributed Transactions](04-Distributed-Transactions.md)