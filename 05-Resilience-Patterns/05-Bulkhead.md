# Bulkhead

## Introduction

The Bulkhead Pattern is a resilience pattern that **isolates system components so that a failure in one component does not affect the others**.

The name comes from ships, where watertight bulkheads divide the vessel into separate compartments. If one compartment floods, the others remain intact, preventing the entire ship from sinking.

Similarly, in software systems, resources such as threads, connection pools, or service instances are isolated to prevent cascading failures.

The main goals of the Bulkhead pattern are:

- Isolate failures.
- Prevent cascading failures.
- Improve system stability.
- Protect critical services.

---

## Why was it Introduced?

Consider an application with multiple services sharing the same thread pool.

```text
          Thread Pool

      /      |      \

     ▼       ▼       ▼

 Payment  Orders  Search
```

If the Payment Service becomes slow and consumes all available threads:

- Orders become slow.
- Search becomes unavailable.
- The entire application suffers.

The Bulkhead Pattern isolates resources.

---

## Architecture Diagram

```text
                Client

                   |

                   ▼

             API Gateway

                   |

      ----------------------------

      |            |            |

      ▼            ▼            ▼

 Payment Pool  Order Pool  Search Pool

      |            |            |

      ▼            ▼            ▼

 Payment      Order       Search
 Service      Service     Service
```

Each service has its own dedicated resources.

---

## How It Works

The communication flow:

```text
1. Client sends a request.

2. Request is routed to the appropriate resource pool.

3. Service processes the request.

4. If one resource pool becomes exhausted:
      Only that service is affected.

5. Other services continue operating normally.
```

Example:

```text
Payment Threads Full

        |

Payment Requests Fail

        |

Order Service Continues

        |

Search Continues
```

---

# Core Components

## 1. Resource Pools

Dedicated resources for each component.

Examples:

- Thread pools.
- Connection pools.
- Worker pools.

---

## 2. Service Isolation

Each service uses its own resources.

---

## 3. Failure Containment

Failures remain confined to one isolated compartment.

---

## 4. Resource Limits

Each pool has a maximum capacity to prevent resource exhaustion.

---

# Core Characteristics

## 1. Resource Isolation

Components do not compete for the same resources.

---

## 2. Failure Containment

One failing component does not impact unrelated components.

---

## 3. Improved Stability

Healthy services continue operating during localized failures.

---

## 4. Independent Capacity

Each component has its own resource allocation.

---

## 5. Better Fault Tolerance

The system continues providing partial functionality even when one component fails.

---

# Types of Bulkheads

## 1. Thread Pool Isolation

Each service has its own thread pool.

---

## 2. Connection Pool Isolation

Separate database or network connection pools for different services.

---

## 3. Service Isolation

Run services independently using separate containers or instances.

---

## 4. Queue Isolation

Each workload has its own message queue to prevent one queue from blocking others.

---

# Advantages

## 1. Prevents Cascading Failures

Failures are isolated to a single component.

---

## 2. Improves Availability

Healthy services remain responsive.

---

## 3. Better Resource Utilization

Critical services retain reserved resources.

---

## 4. Easier Failure Recovery

Only the affected component requires recovery.

---

## 5. Increased System Stability

Resource exhaustion is less likely to impact the entire application.

---

# Disadvantages

## 1. Increased Complexity

Managing multiple resource pools requires additional configuration.

---

## 2. Resource Underutilization

Reserved resources may remain idle while other pools are overloaded.

---

## 3. Capacity Planning

Each pool must be sized appropriately.

---

## 4. Operational Overhead

More monitoring and tuning are required.

---

## 5. Additional Infrastructure

Large systems may require more containers, instances, or hardware.

---

# Real-World Examples

## E-Commerce

Separate thread pools for:

- Payments.
- Orders.
- Search.

---

## Banking

Dedicated resources for:

- Transactions.
- Account Balance.
- Notifications.

---

## Cloud Platforms

Separate worker pools for different background jobs.

---

## Microservices

Each service runs independently with its own CPU, memory, and connection limits.

---

# When to Use

Use the Bulkhead pattern when:

- Building distributed systems.
- Services have different workloads.
- Preventing cascading failures is important.
- Critical services require dedicated resources.

---

# When NOT to Use

Avoid the Bulkhead pattern when:

- Applications are small.
- Resource isolation adds unnecessary complexity.
- Workloads are simple and predictable.

---

# Comparison

| Feature | Shared Resources | Bulkhead Pattern |
|---|---|---|
| Resource Usage | Shared | Isolated |
| Cascading Failures | More Likely | Less Likely |
| Fault Isolation | Low | High |
| System Stability | Lower | Higher |
| Operational Complexity | Lower | Higher |

---

# Interview Questions

## 1. What is the Bulkhead pattern?

A resilience pattern that isolates resources so failures in one component do not affect others.

---

## 2. Why is it called the Bulkhead pattern?

It is inspired by ship bulkheads, which isolate flooding to prevent the entire ship from sinking.

---

## 3. What resources can be isolated?

- Thread pools.
- Connection pools.
- Worker pools.
- Containers.
- Message queues.

---

## 4. How does the Bulkhead pattern prevent cascading failures?

By ensuring each component has dedicated resources, preventing one overloaded service from consuming resources needed by others.

---

## 5. Which patterns are commonly used with Bulkhead?

- Retry
- Timeout
- Circuit Breaker
- Fallback

---

# Key Takeaways

- The Bulkhead pattern isolates resources between system components.
- It prevents failures from spreading across the application.
- Dedicated resource pools improve system stability and availability.
- Capacity planning is essential for effective isolation.
- It is widely used in microservices and cloud-native architectures.

---

## Previous & Next

← Previous: [Fallback](04-Fallback.md)

→ Next: [Dead Letter Queue (DLQ)](06-Dead-Letter-Queue-DLQ.md)