# Leader Election

## Introduction

The Leader Election pattern is a resilience pattern that **selects one node as the leader among a group of distributed nodes**.

The elected leader is responsible for coordinating specific tasks, while the remaining nodes act as followers. If the leader fails, a new leader is automatically elected.

The main goals of the Leader Election pattern are:

- Coordinate distributed operations.
- Prevent duplicate work.
- Improve fault tolerance.
- Enable automatic failover.

---

## Why was it Introduced?

In distributed systems, multiple instances may perform the same task simultaneously.

Example:

```text
Node A

Node B

Node C

↓

Run Scheduled Job
```

Without coordination:

- Jobs execute multiple times.
- Shared data may become inconsistent.
- Resources are wasted.

Leader Election ensures that only one node performs the coordination task.

---

## Architecture Diagram

```text
           Cluster

     /       |       \

    ▼        ▼        ▼

 Node A   Node B   Node C

             |

             ▼

         Leader

        /   |   \

       ▼    ▼    ▼

Followers Followers Followers
```

Only the leader performs coordination tasks.

---

## How It Works

The communication flow:

```text
1. Nodes join the cluster.

2. A leader election algorithm selects one leader.

3. The leader coordinates shared operations.

4. Followers continue normal work.

5. If the leader fails:
      A new leader election begins.

6. A new leader takes over automatically.
```

Example:

```text
Leader Fails

      |

Election Starts

      |

Node B Wins

      |

New Leader
```

---

# Core Components

## 1. Cluster Nodes

Independent servers participating in leader election.

---

## 2. Leader

Coordinates cluster-wide operations.

---

## 3. Followers

Perform normal workloads and wait for leader changes.

---

## 4. Election Algorithm

Determines which node becomes the leader.

Examples:

- Raft
- Paxos
- ZooKeeper-based election

---

# Core Characteristics

## 1. Single Coordinator

Only one leader performs coordination tasks at a time.

---

## 2. Automatic Failover

Leadership transfers automatically if the current leader fails.

---

## 3. Fault Tolerance

The cluster continues operating despite node failures.

---

## 4. Distributed Coordination

Nodes cooperate without manual intervention.

---

## 5. High Availability

Critical coordination tasks remain available.

---

# Common Use Cases

## 1. Scheduled Jobs

Ensure scheduled tasks run only once across a cluster.

---

## 2. Distributed Databases

One node coordinates replication and metadata updates.

---

## 3. Distributed Locks

A leader manages lock ownership.

---

## 4. Cluster Management

Coordinate resource allocation and membership changes.

---

# Advantages

## 1. Prevents Duplicate Work

Only one node performs coordination tasks.

---

## 2. Automatic Recovery

Leadership transfers automatically after failures.

---

## 3. Improved Consistency

Centralized coordination reduces conflicting operations.

---

## 4. Better Resource Utilization

Eliminates unnecessary duplicate processing.

---

## 5. High Availability

The cluster remains operational despite leader failures.

---

# Disadvantages

## 1. Election Overhead

Leader elections temporarily delay coordination.

---

## 2. Increased Complexity

Election protocols are complex to implement correctly.

---

## 3. Temporary Unavailability

No leader is available while an election is in progress.

---

## 4. Split-Brain Risk

Network partitions may incorrectly produce multiple leaders if not handled properly.

---

## 5. Dependency on Consensus

Reliable leader election often depends on distributed consensus algorithms.

---

# Real-World Examples

## Kubernetes

One control-plane instance acts as the active leader for certain controller operations.

---

## Apache Kafka

One broker acts as the leader for each partition.

---

## Apache ZooKeeper

Coordinates leader election for distributed applications.

---

## Distributed Databases

Leaders coordinate replication and metadata management.

---

# When to Use

Use the Leader Election pattern when:

- Multiple nodes coordinate shared tasks.
- Scheduled jobs should execute only once.
- Distributed coordination is required.
- Automatic failover is important.

---

# When NOT to Use

Avoid the Leader Election pattern when:

- Applications are single-instance.
- All nodes operate independently.
- Coordination between nodes is unnecessary.

---

# Comparison

| Feature | No Leader Election | Leader Election |
|---|---|---|
| Task Coordination | Multiple Nodes | Single Leader |
| Duplicate Processing | Possible | Prevented |
| Automatic Failover | No | Yes |
| Fault Tolerance | Lower | Higher |
| Operational Complexity | Lower | Higher |

---

# Interview Questions

## 1. What is the Leader Election pattern?

A resilience pattern that selects one node to coordinate operations in a distributed system.

---

## 2. Why is Leader Election important?

It prevents duplicate work and enables coordinated operations across multiple nodes.

---

## 3. What happens if the leader fails?

The remaining nodes run an election to select a new leader automatically.

---

## 4. Which algorithms are commonly used for Leader Election?

- Raft
- Paxos
- ZooKeeper-based election

---

## 5. Where is Leader Election commonly used?

- Kubernetes.
- Apache Kafka.
- Distributed databases.
- Cluster management systems.

---

# Key Takeaways

- Leader Election designates one node as the coordinator in a distributed system.
- It prevents duplicate execution of shared tasks.
- Automatic failover maintains system availability.
- Consensus algorithms are commonly used to elect leaders.
- It is a fundamental coordination pattern in distributed systems.

---

## Previous & Next

← Previous: [Health Check](07-Health-Check.md)

→ Next: [Distributed Lock](09-Distributed-Lock.md)