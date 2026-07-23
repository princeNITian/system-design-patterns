# Vector Clocks

## Introduction

Vector Clocks are a distributed system pattern used to **determine the ordering of events and detect concurrent updates in distributed systems without relying on synchronized physical clocks**.

Unlike timestamps based on system clocks, Vector Clocks use logical counters maintained by each node to establish causal relationships between events.

The main goals of Vector Clocks are:

- Track event ordering.
- Detect concurrent updates.
- Preserve causality.
- Resolve conflicts in distributed systems.

---

## Why were they Introduced?

Suppose two users update the same document simultaneously.

```text
Node A

↓

Update Document

Node B

↓

Update Document
```

If both nodes rely on local system clocks:

```text
Node A → 10:00:01

Node B → 10:00:00
```

Clock skew may cause the wrong update to be considered newer.

Vector Clocks solve this by tracking the logical history of updates instead of physical time.

---

## Architecture Diagram

```text
          Shared Data

         /           \

        ▼             ▼

     Node A        Node B

        |             |

   VC: [1,0]     VC: [0,1]

        \             /

         ▼           ▼

      Conflict Detection
```

Each node maintains its own vector clock and exchanges it with updates.

---

## How It Works

The execution flow:

```text
1. Every node maintains a vector clock.

2. Before making an update, the node increments its own counter.

3. The update includes the vector clock.

4. Receiving nodes compare vector clocks.

5. The relationship is determined:
      - Older
      - Newer
      - Concurrent

6. Concurrent updates may require conflict resolution.
```

Example:

```text
Node A

[1,0]

↓

Update

↓

[2,0]
```

Node B:

```text
[0,1]

↓

Update

↓

[0,2]
```

Comparing:

```text
[2,0]

vs

[0,2]
```

Neither dominates the other, indicating concurrent updates.

---

# Core Characteristics

## 1. Logical Time

Vector Clocks measure event ordering using logical counters instead of physical clocks.

---

## 2. Per-Node Counters

Each node maintains its own counter within the vector.

---

## 3. Causal Ordering

Vector Clocks identify whether one event happened before another.

---

## 4. Concurrent Update Detection

Independent updates can be detected reliably.

---

## 5. Distributed Operation

No centralized clock or coordinator is required.

---

# Comparing Vector Clocks

Suppose:

```text
A = [2,1,0]

B = [3,2,0]
```

Since every value in **A** is less than or equal to **B**, and at least one value is smaller:

```text
A happened before B
```

---

Suppose:

```text
A = [2,1]

B = [1,2]
```

Neither vector dominates the other.

The events are **concurrent**.

---

# Advantages

## 1. Accurate Event Ordering

Captures causal relationships without relying on synchronized clocks.

---

## 2. Detects Concurrent Updates

Identifies when multiple nodes update data independently.

---

## 3. Distributed

Works without centralized coordination.

---

## 4. Conflict Detection

Supports conflict resolution in replicated systems.

---

## 5. Clock Skew Independent

Physical clock inaccuracies do not affect correctness.

---

# Disadvantages

## 1. Metadata Growth

Vector size increases with the number of participating nodes.

---

## 2. Comparison Complexity

Comparing vectors becomes more expensive as clusters grow.

---

## 3. Membership Changes

Adding or removing nodes requires updating vector structures.

---

## 4. Not Human Readable

Logical counters do not indicate actual timestamps.

---

## 5. Scalability Limitations

Large clusters generate larger vectors.

---

# Real-World Examples

## Amazon Dynamo

Uses Vector Clocks to detect conflicting object versions.

---

## Riak

Maintains Vector Clocks for conflict detection and version management.

---

## Distributed Document Databases

Track concurrent document updates across replicas.

---

## Collaborative Editing Systems

Detect simultaneous edits made by multiple users.

---

# When to Use

Use Vector Clocks when:

- Replicating data across multiple nodes.
- Detecting concurrent updates.
- Maintaining causal ordering.
- Building eventually consistent distributed systems.

---

# When NOT to Use

Avoid Vector Clocks when:

- Physical timestamps are sufficient.
- Strong consistency eliminates concurrent writes.
- The number of participating nodes is extremely large.

---

# Comparison

| Feature | Physical Clock | Vector Clock |
|---|---|---|
| Time Source | System Clock | Logical Counters |
| Clock Synchronization | Required | Not Required |
| Detect Concurrent Events | No | Yes |
| Causal Ordering | Limited | Yes |
| Metadata Size | Small | Grows with Nodes |

---

# Interview Questions

## 1. What is a Vector Clock?

A logical clock mechanism that tracks event ordering and detects concurrent updates in distributed systems.

---

## 2. Why are Vector Clocks needed?

Because physical clocks cannot reliably determine event ordering in distributed environments.

---

## 3. What information does a Vector Clock contain?

A logical counter for each participating node.

---

## 4. What does it mean if two Vector Clocks are incomparable?

The corresponding events occurred concurrently.

---

## 5. Which systems commonly use Vector Clocks?

- Amazon Dynamo
- Riak
- Replicated distributed databases
- Collaborative editing systems

---

# Key Takeaways

- Vector Clocks provide logical event ordering without synchronized clocks.
- They preserve causal relationships between distributed events.
- Concurrent updates can be detected reliably.
- Metadata grows as more nodes participate.
- Vector Clocks are widely used in eventually consistent distributed systems.

---

## Previous & Next

← Previous: [Heartbeat](09-Heartbeat.md)

→ Next: [CRDT (Conflict-Free Replicated Data Types)](11-CRDT-Conflict-Free-Replicated-Data-Types.md)