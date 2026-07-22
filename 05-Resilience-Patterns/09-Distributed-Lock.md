# Distributed Lock

## Introduction

The Distributed Lock pattern is a resilience pattern that **ensures only one node or process can access a shared resource at a time across a distributed system**.

Unlike traditional locks that work within a single process or machine, distributed locks coordinate access across multiple servers, preventing race conditions and maintaining data consistency.

The main goals of the Distributed Lock pattern are:

- Prevent concurrent access to shared resources.
- Ensure data consistency.
- Avoid race conditions.
- Coordinate distributed operations.

---

## Why was it Introduced?

In distributed systems, multiple services may attempt to update the same resource simultaneously.

Example:

```text
Service A

        \

         ▼

      Update Inventory

         ▲

        /

Service B
```

Without coordination:

- Inventory may become inconsistent.
- Duplicate processing may occur.
- Data corruption can happen.

A Distributed Lock allows only one service to modify the resource at a time.

---

## Architecture Diagram

```text
          Service A

               |

               ▼

        Acquire Lock

               |

               ▼

        Lock Manager

          /         \

     Lock Granted  Lock Denied

          |             |

          ▼             ▼

 Update Resource     Wait / Retry

          |

          ▼

      Release Lock
```

Only one service can hold the lock for a resource at any given time.

---

## How It Works

The communication flow:

```text
1. Service requests a lock.

2. Lock manager checks lock ownership.

3. If the lock is available:
      Grant the lock.

4. Perform the operation.

5. Release the lock.

6. Waiting services can now acquire the lock.
```

Example:

```text
Service A

      |

Acquire Lock

      |

Update Inventory

      |

Release Lock

      |

Service B Acquires Lock
```

---

# Core Components

## 1. Client

Requests access to a shared resource.

---

## 2. Lock Manager

Controls lock acquisition and release.

Examples:

- Redis
- ZooKeeper
- etcd
- Consul

---

## 3. Lock

Represents exclusive ownership of a resource.

---

## 4. Shared Resource

The protected resource.

Examples:

- Database row.
- File.
- Inventory record.
- Scheduled job.

---

# Core Characteristics

## 1. Mutual Exclusion

Only one client holds the lock at a time.

---

## 2. Distributed Coordination

Works across multiple servers or services.

---

## 3. Lock Expiration

Locks typically have a timeout (TTL) to prevent deadlocks if the owner crashes.

---

## 4. Safe Release

Only the lock owner should release the lock.

---

## 5. Fault Tolerance

Many distributed lock implementations remain available despite node failures.

---

# Advantages

## 1. Prevents Race Conditions

Ensures shared resources are modified safely.

---

## 2. Maintains Data Consistency

Avoids conflicting updates from multiple services.

---

## 3. Supports Distributed Coordination

Enables synchronization across multiple instances.

---

## 4. Automatic Lock Expiration

TTL helps recover from unexpected failures.

---

## 5. Widely Supported

Many distributed systems provide built-in lock mechanisms.

---

# Disadvantages

## 1. Increased Latency

Acquiring and releasing locks adds network overhead.

---

## 2. Potential Bottlenecks

Highly contended locks can reduce throughput.

---

## 3. Deadlock Risk

Improper lock management can cause deadlocks or prolonged waiting.

---

## 4. Additional Infrastructure

Requires a reliable distributed coordination service.

---

## 5. Implementation Complexity

Correct lock ownership, expiration, and recovery require careful design.

---

# Real-World Examples

## Inventory Management

Prevent overselling by allowing only one service to update stock at a time.

---

## Scheduled Jobs

Ensure a scheduled task runs only once across a cluster.

---

## Payment Processing

Prevent duplicate payment processing for the same transaction.

---

## Distributed Databases

Coordinate metadata updates and administrative operations.

---

# When to Use

Use the Distributed Lock pattern when:

- Multiple services update the same resource.
- Data consistency is critical.
- Duplicate processing must be prevented.
- Distributed coordination is required.

---

# When NOT to Use

Avoid the Distributed Lock pattern when:

- Resources are independent.
- Optimistic concurrency control is sufficient.
- High lock contention would significantly reduce performance.

---

# Comparison

| Feature | Local Lock | Distributed Lock |
|---|---|---|
| Scope | Single Process | Multiple Processes / Servers |
| Network Communication | No | Yes |
| Distributed Coordination | No | Yes |
| Fault Tolerance | Limited | Higher |
| Implementation Complexity | Lower | Higher |

---

# Interview Questions

## 1. What is a Distributed Lock?

A mechanism that ensures only one node or process can access a shared resource at a time in a distributed system.

---

## 2. Why are Distributed Locks needed?

To prevent race conditions and maintain consistency when multiple services access shared resources.

---

## 3. Why do distributed locks use TTL (Time-To-Live)?

TTL automatically releases abandoned locks if the lock owner crashes, reducing the risk of deadlocks.

---

## 4. Which systems commonly implement Distributed Locks?

- Redis
- ZooKeeper
- etcd
- Consul

---

## 5. Where are Distributed Locks commonly used?

- Inventory management.
- Payment processing.
- Distributed schedulers.
- Cluster coordination.

---

# Key Takeaways

- Distributed Locks coordinate access to shared resources across multiple servers.
- They prevent race conditions and inconsistent updates.
- Locks should include expiration (TTL) to improve fault tolerance.
- They are commonly implemented using Redis, ZooKeeper, etcd, or Consul.
- They are an essential coordination mechanism in distributed systems.

---

## Previous & Next

← Previous: [Leader Election](08-Leader-Election.md)

→ Next Module: [06-System-Design-Case-Studies](../06-System-Design-Case-Studies/README.md)