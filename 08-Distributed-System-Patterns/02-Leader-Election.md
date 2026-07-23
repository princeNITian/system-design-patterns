# Leader Election

## Introduction

Leader Election is a distributed system pattern that **selects one node from a group of nodes to act as the coordinator or leader**.

The elected leader is responsible for coordinating operations, making decisions, and managing shared resources, while the remaining nodes act as followers.

The main goals of Leader Election are:

- Prevent conflicting decisions.
- Coordinate distributed operations.
- Simplify distributed system management.
- Ensure high availability through automatic leader replacement.

---

## Why was it Introduced?

Consider a distributed system with multiple nodes.

```text
Node A

Node B

Node C
```

If every node independently accepts writes or coordinates operations:

- Multiple conflicting decisions may occur.
- Data consistency becomes difficult.
- Split-brain scenarios may arise.

Leader Election ensures that only one node coordinates critical operations at a time.

---

## Architecture Diagram

### Before Election

```text
           Cluster

      -----------------

      |       |       |

      ▼       ▼       ▼

    Node A  Node B  Node C

        No Leader
```

---

### After Election

```text
           Cluster

      -----------------

      |       |       |

      ▼       ▼       ▼

 Leader A   Node B   Node C

      |

Coordinates Cluster
```

Only the leader performs coordination tasks.

---

## How It Works

The election flow:

```text
1. Nodes join the cluster.

2. Nodes participate in an election.

3. One node becomes the leader.

4. Remaining nodes become followers.

5. Followers monitor the leader.

6. If the leader fails, a new election begins.
```

Example:

```text
Leader A

↓

Leader Fails

↓

Election

↓

Leader C
```

---

# Core Characteristics

## 1. Single Coordinator

Only one node acts as the leader at any given time.

---

## 2. Automatic Failover

A new leader is elected if the current leader becomes unavailable.

---

## 3. Distributed Coordination

Followers rely on the leader for coordinated operations.

---

## 4. Mutual Exclusion

Critical operations are performed by only one leader.

---

## 5. Dynamic Membership

Nodes can join or leave while the cluster continues operating.

---

# Election Strategies

## 1. Consensus-Based Election

Consensus algorithms such as Raft or Paxos elect a leader.

---

## 2. Highest Priority

The node with the highest priority or identifier becomes the leader.

---

## 3. External Coordinator

A coordination service manages leader election.

Examples:

- etcd
- ZooKeeper
- Consul

---

# Advantages

## 1. Prevents Conflicting Decisions

Only one node coordinates critical operations.

---

## 2. Simplifies Coordination

Followers do not compete for leadership responsibilities.

---

## 3. High Availability

Leadership automatically transfers when failures occur.

---

## 4. Scalable Coordination

Supports clusters with many distributed nodes.

---

## 5. Foundation for Consensus

Many consensus algorithms rely on leader-based coordination.

---

# Disadvantages

## 1. Leader Bottleneck

The leader may become a performance bottleneck under heavy workloads.

---

## 2. Election Overhead

Leader failures trigger election processes.

---

## 3. Temporary Unavailability

Some operations may pause while a new leader is elected.

---

## 4. Implementation Complexity

Correct election handling requires careful protocol design.

---

## 5. Split-Brain Risk

Poorly implemented systems may temporarily elect multiple leaders.

---

# Real-World Examples

## Kubernetes

The Kubernetes control plane uses leader election for certain controller components.

---

## Apache Kafka

Each partition has a leader responsible for handling reads and writes.

---

## Apache ZooKeeper

Coordinates leader election for distributed applications.

---

## etcd

Uses the Raft algorithm to elect a cluster leader.

---

# When to Use

Use Leader Election when:

- Coordinating distributed services.
- Managing replicated state.
- Preventing conflicting writes.
- Building distributed databases.
- Implementing distributed schedulers.

---

# When NOT to Use

Avoid Leader Election when:

- Every node can safely operate independently.
- Eventual consistency is acceptable.
- The workload is fully decentralized.

---

# Comparison

| Feature | Leader Election | Leaderless Architecture |
|---|---|---|
| Coordinator | Single Leader | No Leader |
| Decision Making | Centralized | Distributed |
| Coordination Complexity | Lower | Higher |
| Bottleneck Risk | Possible | Lower |
| Fault Tolerance | High | High (Design Dependent) |

---

# Interview Questions

## 1. What is Leader Election?

A process that selects one node in a distributed system to coordinate operations while other nodes act as followers.

---

## 2. Why is Leader Election important?

It prevents conflicting decisions and simplifies distributed coordination.

---

## 3. What happens if the leader fails?

A new election is triggered, and another node becomes the leader.

---

## 4. Which systems commonly use Leader Election?

- Kubernetes
- Apache Kafka
- etcd
- ZooKeeper
- Consul

---

## 5. How is Leader Election commonly implemented?

Using consensus algorithms such as Raft or Paxos, or external coordination systems.

---

# Key Takeaways

- Leader Election selects a single coordinator within a distributed system.
- It prevents conflicting operations and simplifies coordination.
- Automatic failover maintains system availability.
- Consensus algorithms frequently include leader election mechanisms.
- Leader Election is widely used in distributed databases, coordination services, and orchestration platforms.

---

## Previous & Next

← Previous: [Consensus Algorithms](01-Consensus-Algorithms.md)

→ Next: [Quorum](03-Quorum.md)