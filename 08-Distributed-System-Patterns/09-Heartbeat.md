# Heartbeat

## Introduction

Heartbeat is a distributed system pattern in which **nodes periodically send small messages to indicate that they are alive and functioning correctly**.

Other nodes or monitoring systems use these heartbeat messages to detect failures and determine whether a node is healthy.

The main goals of Heartbeat are:

- Detect node failures.
- Monitor cluster health.
- Trigger automatic failover.
- Maintain high availability.

---

## Why was it Introduced?

Consider a distributed cluster.

```text
Node A

Node B

Node C
```

If Node B crashes unexpectedly:

```text
Node A

Node B ✗

Node C
```

Without a mechanism to detect failures, the cluster may continue sending requests to Node B.

Heartbeat messages enable the cluster to quickly recognize that Node B is no longer operational.

---

## Architecture Diagram

```text
             Heartbeat Monitor

                    ▲

          Heartbeat |

                    |

      ----------------------------

      |            |            |

      ▼            ▼            ▼

    Node A      Node B      Node C
```

Each node periodically sends heartbeat messages to indicate it is alive.

---

## How It Works

The execution flow:

```text
1. Node starts.

2. Node periodically sends heartbeat messages.

3. Monitor or peers receive the heartbeats.

4. Heartbeats stop arriving.

5. Timeout expires.

6. Node is marked as failed.

7. Recovery or failover begins.
```

Example:

```text
Node A

↓

Heartbeat

↓

Heartbeat

↓

Heartbeat

↓

No Heartbeat

↓

Failure Detected
```

---

# Types of Heartbeat

## 1. Centralized Heartbeat

Nodes send heartbeat messages to a central monitoring service.

```text
Nodes

↓

Central Monitor
```

---

## 2. Peer-to-Peer Heartbeat

Nodes exchange heartbeat messages directly with one another.

```text
Node A ↔ Node B ↔ Node C
```

---

## 3. Gossip-Based Heartbeat

Heartbeat information spreads through gossip communication.

This approach is common in very large distributed systems.

---

# Core Characteristics

## 1. Periodic Health Checks

Nodes transmit heartbeat messages at regular intervals.

---

## 2. Failure Detection

Missing heartbeats indicate possible node failures.

---

## 3. Timeout-Based Monitoring

A node is considered failed after a configurable timeout.

---

## 4. Lightweight Communication

Heartbeat messages are intentionally small to minimize network overhead.

---

## 5. Automatic Recovery Trigger

Failure detection can initiate leader election, failover, or workload redistribution.

---

# Advantages

## 1. Fast Failure Detection

Node failures are identified quickly.

---

## 2. Improved Availability

Clusters can react automatically to failures.

---

## 3. Simple Implementation

Heartbeat protocols are straightforward to implement.

---

## 4. Low Communication Cost

Heartbeat packets are small and efficient.

---

## 5. Foundation for High Availability

Heartbeat monitoring supports leader election, failover, and cluster management.

---

# Disadvantages

## 1. False Positives

Temporary network delays may incorrectly indicate node failures.

---

## 2. Timeout Tuning

Choosing timeout values involves balancing detection speed and false alarms.

---

## 3. Additional Network Traffic

Periodic heartbeat messages consume bandwidth, especially in large clusters.

---

## 4. Monitoring Infrastructure

Centralized heartbeat systems introduce additional components.

---

## 5. Does Not Diagnose Failures

A missing heartbeat indicates a potential failure but not its root cause.

---

# Real-World Examples

## Kubernetes

The control plane monitors node health using periodic heartbeats.

---

## Apache ZooKeeper

Uses heartbeat-like mechanisms to detect server failures.

---

## Apache Cassandra

Combines gossip communication with heartbeat information for failure detection.

---

## etcd

Monitors cluster members and leader health through periodic communication.

---

# When to Use

Use Heartbeat when:

- Monitoring distributed nodes.
- Detecting failures.
- Supporting automatic failover.
- Building highly available systems.
- Managing clusters.

---

# When NOT to Use

Avoid Heartbeat when:

- Single-node applications are sufficient.
- Failures are handled manually.
- Continuous health monitoring is unnecessary.

---

# Comparison

| Feature | Heartbeat | Health Check API |
|---|---|---|
| Purpose | Detect Node Liveness | Verify Service Health |
| Frequency | Periodic | On Demand or Scheduled |
| Data | Minimal Status | Detailed Health Information |
| Typical Users | Cluster Members | Load Balancers, Monitoring Systems |
| Failure Detection | Yes | Yes |

---

# Interview Questions

## 1. What is a Heartbeat?

A periodic message sent by a node to indicate that it is alive and operational.

---

## 2. Why are Heartbeats important?

They enable distributed systems to detect failures and initiate recovery actions.

---

## 3. What happens when heartbeats stop?

After a timeout, the node is marked as failed, and recovery or failover procedures begin.

---

## 4. What are common heartbeat implementations?

- Centralized monitoring
- Peer-to-peer heartbeats
- Gossip-based heartbeats

---

## 5. Which systems commonly use Heartbeats?

- Kubernetes
- ZooKeeper
- Cassandra
- etcd

---

# Key Takeaways

- Heartbeat messages indicate node liveness.
- Missing heartbeats trigger failure detection.
- Heartbeats are lightweight and periodic.
- They are fundamental to cluster management and high availability.
- Modern distributed systems often combine heartbeats with leader election, gossip, and service discovery.

---

## Previous & Next

← Previous: [Service Discovery](08-Service-Discovery.md)

→ Next: [Vector Clocks](10-Vector-Clocks.md)