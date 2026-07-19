# Competing Consumers Pattern

## Introduction

The Competing Consumers Pattern is a communication pattern where multiple consumers listen to the same message queue, but **each message is processed by only one consumer**.

As the number of messages increases, additional consumers can be added to process messages in parallel, improving throughput and scalability.

The main goals of the Competing Consumers pattern are:

- Increase message processing throughput.
- Distribute workload across multiple workers.
- Improve scalability.
- Prevent duplicate message processing.

---

## Why was it Introduced?

Imagine an order processing system where a single worker processes all incoming orders.

```text
Orders Queue

      |

      ▼

 Worker

      |

Process Orders
```

As order volume grows:

- Messages accumulate in the queue.
- Processing becomes slow.
- Customers experience delays.

Instead of using one worker, multiple workers can consume messages from the same queue.

---

## Architecture Diagram

```text
              Message Queue

                    |

        ┌───────────┼───────────┐

        ▼           ▼           ▼

     Worker 1    Worker 2    Worker 3

         \           |           /

          Each message is processed
             by only one worker
```

The queue automatically distributes messages among available consumers.

---

## How It Works

The communication flow:

```text
1. Producer sends messages to a queue.

2. Multiple consumers listen to the queue.

3. The queue delivers each message to only one consumer.

4. The consumer processes the message.

5. The message is acknowledged and removed from the queue.
```

Example:

```text
Queue

Message 1 → Worker A

Message 2 → Worker B

Message 3 → Worker C

Message 4 → Worker A
```

No two workers process the same message.

---

# Core Characteristics

## 1. Shared Queue

Multiple consumers subscribe to the same queue.

---

## 2. Single Processing

Each message is delivered to only one consumer.

---

## 3. Parallel Processing

Multiple workers process different messages simultaneously.

---

## 4. Dynamic Scaling

Workers can be added or removed based on workload.

---

## 5. Load Distribution

The messaging system balances messages across consumers.

---

# Advantages

## 1. Higher Throughput

Multiple workers increase processing capacity.

---

## 2. Horizontal Scalability

More consumers can be added without changing producers.

---

## 3. Better Resource Utilization

Available workers share the workload efficiently.

---

## 4. Improved Fault Tolerance

If one worker fails, remaining workers continue processing new messages.

---

## 5. Loose Coupling

Producers are unaware of how many consumers exist.

---

# Disadvantages

## 1. Message Ordering

Order is generally not guaranteed when multiple consumers process messages.

---

## 2. Duplicate Delivery

Some messaging systems may redeliver messages if acknowledgements fail.

Consumers should therefore be idempotent.

---

## 3. Uneven Workloads

Long-running tasks can cause some workers to remain busy while others become idle.

---

## 4. Monitoring Complexity

Tracking processing across many workers requires proper observability.

---

## 5. Shared Resource Contention

Workers accessing the same database or external service may create bottlenecks.

---

# Real-World Examples

## E-Commerce

Workers process:

- Order creation.
- Invoice generation.
- Shipping requests.

---

## Image Processing

Each uploaded image is processed by one available worker.

---

## Email Systems

Email jobs are distributed across multiple email workers.

---

## Video Processing

Video encoding tasks are assigned to available encoding servers.

---

# When to Use

Use the Competing Consumers pattern when:

- Large numbers of independent messages must be processed.
- Processing can occur in parallel.
- High throughput is required.
- Message order is not critical.

---

# When NOT to Use

Avoid the Competing Consumers pattern when:

- Messages must be processed strictly in order.
- Every consumer must receive every message.
- Tasks are tightly coupled and cannot execute independently.

---

# Comparison

| Feature | Publish-Subscribe | Competing Consumers |
|---|---|---|
| Message Delivery | Every subscriber receives the message | Only one consumer receives each message |
| Purpose | Broadcast events | Distribute workload |
| Processing | One-to-Many | One-to-One |
| Scalability | Consumer scaling | Worker scaling |
| Common Use Case | Notifications | Background job processing |

---

# Interview Questions

## 1. What is the Competing Consumers pattern?

A messaging pattern where multiple consumers read from the same queue, but each message is processed by only one consumer.

---

## 2. Why is it called "Competing Consumers"?

Because all consumers compete to receive the next available message from the shared queue.

---

## 3. How does it improve scalability?

By allowing multiple workers to process different messages simultaneously.

---

## 4. What happens if one consumer crashes?

Unacknowledged messages are typically returned to the queue and processed by another consumer, depending on the messaging system.

---

## 5. Which technologies commonly support this pattern?

- RabbitMQ
- Amazon SQS
- Apache ActiveMQ
- Azure Service Bus
- Google Cloud Pub/Sub (pull subscriptions)

---

# Key Takeaways

- Multiple consumers share the same message queue.
- Each message is processed by only one consumer.
- The pattern improves throughput through parallel processing.
- Consumers should be idempotent to handle possible duplicate deliveries.
- It is widely used for scalable background job processing.

---

## Previous & Next

← Previous: [Scatter-Gather](05-Scatter-Gather.md)

→ Next: [Work Queue](07-Work-Queue.md)