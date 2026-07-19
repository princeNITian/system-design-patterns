# Fan-Out Pattern

## Introduction

The Fan-Out Pattern is a communication pattern where a single request, event, or message is distributed to multiple downstream services or workers for parallel processing.

Unlike the Publish-Subscribe pattern, which focuses on broadcasting events to interested subscribers, Fan-Out focuses on **executing multiple independent tasks in parallel**.

The main goals of the Fan-Out pattern are:

- Parallelize processing.
- Reduce overall processing time.
- Improve scalability.
- Distribute workload across multiple services.

---

## Why was it Introduced?

Some operations require multiple independent tasks to be executed after a single event occurs.

Example:

A customer places an order.

Several actions must happen:

- Process payment.
- Update inventory.
- Generate invoice.
- Send notification.
- Update analytics.

Executing these tasks sequentially increases response time.

The Fan-Out pattern allows them to run simultaneously.

---

## Architecture Diagram

```text
              Order Service

                    |

             Order Created Event

                    |

                    ▼

              Message Broker

         /       |       |       \

        ▼        ▼       ▼        ▼

   Payment   Inventory  Email  Analytics
    Service    Service  Service  Service
```

A single event is distributed to multiple independent consumers.

---

## How It Works

The communication flow:

```text
1. A service publishes an event.

2. The message broker receives the event.

3. The broker distributes the event.

4. Multiple services process it independently.

5. Each service completes its own task.
```

Example:

```text
User Uploads Image

        |

        ▼

Image Uploaded Event

        |

        ├── Generate Thumbnail

        ├── Virus Scan

        ├── AI Image Tagging

        └── Backup Storage
```

All tasks execute in parallel.

---

# Core Characteristics

## 1. One-to-Many Distribution

A single event is sent to multiple consumers.

---

## 2. Parallel Processing

Consumers process the event simultaneously.

---

## 3. Independent Execution

Each consumer performs its own business logic.

---

## 4. Asynchronous Communication

The publisher does not wait for consumers to finish.

---

## 5. Loose Coupling

Consumers can be added or removed without changing the publisher.

---

# Advantages

## 1. Faster Processing

Parallel execution reduces total processing time.

---

## 2. Better Scalability

Each consumer can scale independently.

---

## 3. Improved Fault Isolation

Failure in one consumer typically does not stop others.

---

## 4. Easy Extensibility

New processing steps can be added easily.

---

## 5. Better Resource Utilization

Workloads are distributed across multiple services.

---

# Disadvantages

## 1. More Infrastructure

Requires messaging systems and multiple consumers.

---

## 2. Harder Debugging

Tracking one event across many services is more difficult.

---

## 3. Duplicate Processing

Consumers should be idempotent because duplicate events may occur.

---

## 4. Eventual Consistency

Different consumers finish at different times.

---

## 5. Monitoring Complexity

Each consumer must be monitored independently.

---

# Real-World Examples

## E-Commerce

Order Created event triggers:

- Payment processing.
- Inventory update.
- Invoice generation.
- Shipping preparation.
- Email notification.

---

## Video Streaming

Video Uploaded event triggers:

- Transcoding.
- Thumbnail generation.
- Metadata extraction.
- Content moderation.

---

## Social Media

New Post event triggers:

- Feed generation.
- Notifications.
- Search indexing.
- Recommendation engine.

---

# When to Use

Use the Fan-Out pattern when:

- One event triggers multiple independent tasks.
- Tasks can execute in parallel.
- High throughput is required.
- Services should remain loosely coupled.

---

# When NOT to Use

Avoid the Fan-Out pattern when:

- Processing must occur in a strict sequence.
- Only one service handles the request.
- Immediate synchronous responses are required.

---

# Comparison

| Feature | Publish-Subscribe | Fan-Out |
|---|---|---|
| Primary Goal | Broadcast events | Parallel task execution |
| Communication | One-to-Many | One-to-Many |
| Processing | Event notification | Concurrent processing |
| Typical Use Case | Notify interested subscribers | Execute multiple independent operations |
| Scalability | High | High |

---

# Interview Questions

## 1. What is the Fan-Out pattern?

A communication pattern where one event is distributed to multiple consumers for parallel processing.

---

## 2. How is Fan-Out different from Publish-Subscribe?

Publish-Subscribe focuses on event distribution to interested subscribers.

Fan-Out focuses on executing multiple independent tasks concurrently after a single event.

---

## 3. Why is Fan-Out useful?

It reduces overall processing time by allowing multiple services to work simultaneously.

---

## 4. Can one Fan-Out consumer fail without affecting others?

Yes. Consumers are typically independent, so one failure usually does not stop the remaining consumers.

---

## 5. Where is the Fan-Out pattern commonly used?

- Order processing.
- Image processing.
- Video processing.
- Notification systems.
- Analytics pipelines.

---

# Key Takeaways

- Fan-Out distributes one event to multiple consumers.
- Independent tasks execute in parallel.
- It improves throughput and scalability.
- Consumers remain loosely coupled.
- Fan-Out is widely used in event-driven architectures for parallel processing.

---

## Previous & Next

← Previous: [Publish-Subscribe](02-Publish-Subscribe.md)

→ Next: [Fan-In](04-Fan-In.md)