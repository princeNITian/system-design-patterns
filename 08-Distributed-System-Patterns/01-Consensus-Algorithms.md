# Consensus Algorithms

## Introduction

Consensus Algorithms are distributed system patterns that **allow multiple nodes to agree on a single value or decision, even in the presence of failures**.

In a distributed system, different nodes may receive requests at different times, experience network delays, or fail unexpectedly. Consensus algorithms ensure that all healthy nodes eventually agree on the same system state.

The main goals of Consensus Algorithms are:

- Maintain consistency across distributed nodes.
- Tolerate node and network failures.
- Prevent conflicting decisions.
- Ensure reliable coordination.

---

## Why were they Introduced?

In a single-server application, there is only one source of truth.

```text
Client

   |

Server

   |

Database
```

In distributed systems, multiple nodes maintain copies of data.

```text
Client

      |

-------------------------

|          |           |

▼          ▼           ▼

Node A    Node B     Node C
```

Without coordination:

- Nodes may accept conflicting updates.
- Network partitions may create inconsistent states.
- Multiple leaders may exist simultaneously.

Consensus algorithms solve these problems by ensuring distributed agreement.

---

## Architecture Diagram

```text
               Clients

                  |

                  ▼

        ---------------------

        |        |          |

        ▼        ▼          ▼

      Node A   Node B    Node C

        |        |          |

        --------Consensus-----

                  |

                  ▼

          Agreed System State
```

Every healthy node reaches the same decision.

---

## How It Works

The general flow:

```text
1. A proposal is created.

2. Nodes exchange messages.

3. Nodes vote or acknowledge.

4. Majority agreement is reached.

5. The decision is committed.

6. All nodes apply the same result.
```

Example:

```text
Node A proposes:

Value = X

↓

Majority Approval

↓

Commit X
```

---

# Core Characteristics

## 1. Distributed Agreement

All participating nodes agree on the same value.

---

## 2. Fault Tolerance

Consensus continues despite node failures, within algorithm limits.

---

## 3. Majority Decision

Most consensus algorithms require agreement from a majority of nodes.

---

## 4. Consistent State

Healthy nodes eventually converge on the same system state.

---

## 5. Deterministic Outcome

Given the same inputs, all nodes reach the same decision.

---

# Popular Consensus Algorithms

## 1. Paxos

One of the earliest consensus algorithms, designed for fault-tolerant distributed systems.

---

## 2. Raft

A consensus algorithm designed to be easier to understand and implement than Paxos.

---

## 3. Zab

Used by Apache ZooKeeper for distributed coordination.

---

## 4. Viewstamped Replication (VR)

A consensus protocol for replicated state machines with leader-based coordination.

---

# Advantages

## 1. Strong Consistency

All nodes agree on the same committed value.

---

## 2. High Fault Tolerance

Consensus can continue even if some nodes fail.

---

## 3. Reliable Coordination

Supports leader election, distributed locking, and replicated state machines.

---

## 4. Prevents Split-Brain

Majority agreement avoids conflicting system states.

---

## 5. Foundation for Distributed Systems

Many distributed databases and coordination systems rely on consensus.

---

# Disadvantages

## 1. Communication Overhead

Nodes exchange multiple messages before reaching agreement.

---

## 2. Increased Latency

Consensus requires coordination before committing changes.

---

## 3. Implementation Complexity

Consensus algorithms are difficult to design and implement correctly.

---

## 4. Majority Requirement

Progress usually requires a majority of nodes to remain available.

---

## 5. Reduced Availability During Partitions

Minority partitions cannot continue making consensus-based decisions.

---

# Real-World Examples

## etcd

Uses the Raft consensus algorithm to store Kubernetes cluster state.

---

## Apache ZooKeeper

Uses the Zab protocol for distributed coordination.

---

## Consul

Uses Raft for service discovery and configuration management.

---

## CockroachDB

Uses Raft to replicate data consistently across nodes.

---

# When to Use

Use Consensus Algorithms when:

- Building distributed databases.
- Coordinating distributed services.
- Maintaining replicated state.
- Performing leader election.
- Ensuring strong consistency.

---

# When NOT to Use

Avoid Consensus Algorithms when:

- Eventual consistency is sufficient.
- High write latency is unacceptable.
- Distributed agreement is unnecessary.

---

# Comparison

| Feature | Consensus Algorithms | Eventual Consistency |
|---|---|---|
| Consistency | Strong | Eventual |
| Coordination | Required | Minimal |
| Latency | Higher | Lower |
| Fault Tolerance | High | High |
| Typical Use Case | Metadata, Coordination | Large-Scale Data Replication |

---

# Interview Questions

## 1. What is a Consensus Algorithm?

A distributed algorithm that enables multiple nodes to agree on a single value despite failures.

---

## 2. Why are Consensus Algorithms necessary?

They maintain consistency and coordination across distributed systems.

---

## 3. What is the purpose of majority voting?

It ensures that only one consistent decision is committed.

---

## 4. Name some popular Consensus Algorithms.

- Paxos
- Raft
- Zab
- Viewstamped Replication (VR)

---

## 5. Where are Consensus Algorithms commonly used?

- Kubernetes (etcd)
- ZooKeeper
- Consul
- Distributed databases
- Configuration management systems

---

# Key Takeaways

- Consensus Algorithms allow distributed nodes to agree on a single decision.
- They provide strong consistency and fault tolerance.
- Majority agreement prevents conflicting system states.
- Raft and Paxos are among the most widely known consensus algorithms.
- Consensus is a foundational building block for modern distributed systems.

---

## Previous & Next

← Previous Module: [07-Deployment-Patterns](../07-Deployment-Patterns/README.md)

→ Next: [Leader Election](02-Leader-Election.md)