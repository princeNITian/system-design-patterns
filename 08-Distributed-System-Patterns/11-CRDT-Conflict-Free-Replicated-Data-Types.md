# CRDT (Conflict-Free Replicated Data Types)

## Introduction

Conflict-Free Replicated Data Types (CRDTs) are distributed data structures that **allow multiple replicas to be updated independently while automatically converging to the same final state without requiring centralized coordination**.

CRDTs are designed for systems where replicas may temporarily diverge due to network delays or partitions but must eventually become consistent.

The main goals of CRDTs are:

- Eliminate manual conflict resolution.
- Support concurrent updates.
- Enable eventual consistency.
- Improve availability during network partitions.

---

## Why were CRDTs Introduced?

Consider two users editing the same distributed counter.

```text
Replica A

Counter = 5
```

```text
Replica B

Counter = 5
```

While disconnected:

```text
Replica A

+2

Counter = 7
```

```text
Replica B

+3

Counter = 8
```

After reconnection:

Without a conflict resolution mechanism:

```text
7 ?

8 ?
```

Which value should survive?

CRDTs define merge rules that guarantee all replicas eventually converge to the same correct value.

---

## Architecture Diagram

```text
             Client A

                |

                ▼

            Replica A

               ▲  ▼

          Synchronize

               ▼  ▲

            Replica B

                ▲

                |

             Client B
```

Replicas accept local updates independently and synchronize later.

---

## How It Works

The execution flow:

```text
1. Replicas receive local updates.

2. Updates are applied independently.

3. Replicas exchange state or operations.

4. Merge rules resolve differences automatically.

5. All replicas converge to the same final state.
```

Example:

```text
Replica A

Counter +2
```

```text
Replica B

Counter +3
```

After synchronization:

```text
Final Counter = 10
```

No manual conflict resolution is required.

---

# Types of CRDTs

## 1. State-Based CRDT (CvRDT)

Replicas periodically exchange their entire state.

The merge operation is:

- Commutative
- Associative
- Idempotent

---

## 2. Operation-Based CRDT (CmRDT)

Replicas exchange operations rather than complete state.

Operations are delivered reliably and applied in the same causal order.

---

## 3. Delta-State CRDT

Only the changed portion (delta) of the state is exchanged, reducing network overhead.

---

# Common CRDT Examples

## Grow-Only Counter (G-Counter)

Supports increment operations only.

---

## Positive-Negative Counter (PN-Counter)

Supports both increment and decrement operations.

---

## Grow-Only Set (G-Set)

Elements can only be added.

---

## Observed-Remove Set (OR-Set)

Supports both additions and removals while handling concurrent updates safely.

---

## Last-Write-Wins Register (LWW Register)

Stores the value associated with the latest logical timestamp.

---

# Core Characteristics

## 1. Eventual Consistency

All healthy replicas eventually converge to the same state.

---

## 2. Conflict-Free Merging

Concurrent updates are merged automatically.

---

## 3. Decentralized Updates

Replicas accept updates without requiring a central coordinator.

---

## 4. Partition Tolerance

Replicas continue operating during temporary network partitions.

---

## 5. Deterministic Convergence

Given the same updates, all replicas reach the same final state.

---

# Advantages

## 1. High Availability

Replicas continue accepting writes during network failures.

---

## 2. Automatic Conflict Resolution

Applications do not need custom merge logic for supported data types.

---

## 3. Excellent Scalability

CRDTs work efficiently across geographically distributed replicas.

---

## 4. No Central Coordinator

Updates can be processed locally.

---

## 5. Strong Support for Offline Systems

Clients can synchronize changes after reconnecting.

---

# Disadvantages

## 1. Limited Data Structures

Not every data model can be represented as a CRDT.

---

## 2. Additional Metadata

Some CRDTs require metadata to support deterministic merging.

---

## 3. Eventual Consistency Only

Replicas may temporarily hold different values before synchronization.

---

## 4. Increased Memory Usage

Metadata can increase storage requirements.

---

## 5. Design Complexity

Choosing or implementing the correct CRDT requires careful analysis.

---

# Real-World Examples

## Redis Enterprise

Uses CRDTs for active-active geo-distributed databases.

---

## Riak

Supports CRDT-based replicated data structures.

---

## Collaborative Document Editors

Merge concurrent user edits without centralized locking.

---

## Offline-First Mobile Applications

Allow users to modify data while disconnected and synchronize later.

---

# When to Use

Use CRDTs when:

- Eventual consistency is acceptable.
- Replicas must accept concurrent updates.
- Offline operation is required.
- Applications span multiple geographic regions.
- High availability is more important than immediate consistency.

---

# When NOT to Use

Avoid CRDTs when:

- Strong consistency is mandatory.
- Strict transactional guarantees are required.
- Data structures cannot be expressed using CRDT semantics.

---

# Comparison

| Feature | Vector Clocks | CRDT |
|---|---|---|
| Primary Purpose | Detect Conflicts | Avoid Conflicts |
| Conflict Resolution | Application Responsibility | Automatic |
| Eventual Consistency | Yes | Yes |
| Concurrent Updates | Detected | Merged |
| Coordinator Required | No | No |

---

# Interview Questions

## 1. What is a CRDT?

A replicated data structure that automatically resolves concurrent updates while guaranteeing eventual convergence across replicas.

---

## 2. Why were CRDTs introduced?

To eliminate manual conflict resolution while maintaining eventual consistency in distributed systems.

---

## 3. What are the two main categories of CRDTs?

- State-Based (CvRDT)
- Operation-Based (CmRDT)

---

## 4. What property guarantees that replicas converge?

Merge operations are deterministic and designed to be commutative, associative, and idempotent (for state-based CRDTs).

---

## 5. Which systems commonly use CRDTs?

- Redis Enterprise
- Riak
- Collaborative editing platforms
- Offline-first distributed applications

---

# Key Takeaways

- CRDTs enable replicas to update data independently.
- Automatic merge rules eliminate many conflict resolution problems.
- They provide eventual consistency without centralized coordination.
- CRDTs are ideal for highly available, geo-distributed, and offline-capable systems.
- They complement patterns such as Gossip Protocol and Vector Clocks in distributed architectures.

---

## Previous & Next

← Previous: [Vector Clocks](10-Vector-Clocks.md)

→ Next Module: [09-Security-Patterns](../09-Security-Patterns/README.md)