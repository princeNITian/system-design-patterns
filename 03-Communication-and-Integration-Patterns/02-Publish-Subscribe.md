# Publish-Subscribe (Pub/Sub) Pattern

## Introduction

The Publish-Subscribe (Pub/Sub) Pattern is an asynchronous communication pattern where publishers send messages to a topic, and subscribers receive those messages without the publisher knowing who the subscribers are.

Unlike the Request-Response pattern, publishers do not communicate directly with consumers. Instead, a message broker acts as an intermediary.

The main goals of the Publish-Subscribe pattern are:

- Decouple services.
- Enable asynchronous communication.
- Broadcast events to multiple consumers.
- Improve scalability and flexibility.

---

## Why was it Introduced?

In a distributed system, one event often needs to trigger multiple independent actions.

Example:

When a customer places an order:

- Inventory Service updates stock.
- Payment Service processes payment.
- Notification Service sends an email.
- Analytics Service records the event.

Direct communication would tightly couple these services.

Publish-Subscribe allows a publisher to send one event while multiple subscribers react independently.

---

## Architecture Diagram

```text
               Publisher

                   |

             Publish Event

                   |

                   ▼

            Message Broker

          /       |       \

         ▼        ▼        ▼

 Subscriber  Subscriber  Subscriber

 Inventory   Email      Analytics
```

The publisher never communicates directly with subscribers.

---

## How It Works

The communication flow:

```text
1. Publisher creates an event.

2. Event is sent to a topic.

3. Message broker stores/routes the event.

4. All subscribed consumers receive the event.

5. Each subscriber processes the event independently.
```

Example:

```text
Order Placed

      |

      ▼

Topic: orders.created

      |

      ├── Inventory Service

      ├── Email Service

      └── Analytics Service
```

---

# Core Components

## 1. Publisher

Produces events.

Example:

```text
Order Service
```

---

## 2. Topic

A logical channel where events are published.

Example:

```text
orders.created
```

---

## 3. Message Broker

Routes published messages to subscribers.

Examples:

- Kafka
- RabbitMQ
- Amazon SNS
- Google Pub/Sub

---

## 4. Subscriber

Consumes events from subscribed topics.

Example:

```text
Notification Service
```

---

# Core Characteristics

## 1. Asynchronous Communication

Publishers do not wait for subscribers.

---

## 2. Loose Coupling

Publishers do not know who consumes the event.

---

## 3. One-to-Many Communication

One published event can be consumed by many subscribers.

---

## 4. Independent Processing

Each subscriber processes events independently.

---

## 5. Easy Scalability

New subscribers can be added without changing publishers.

---

# Advantages

## 1. Loose Coupling

Services evolve independently.

---

## 2. High Scalability

Multiple subscribers can process the same event simultaneously.

---

## 3. Easy Extensibility

Adding a new subscriber requires no publisher changes.

---

## 4. Better Fault Isolation

Failure of one subscriber usually does not affect others.

---

## 5. Supports Event-Driven Systems

Forms the backbone of modern event-driven architectures.

---

# Disadvantages

## 1. Eventual Consistency

Subscribers may process events at different times.

---

## 2. Increased Complexity

Requires message brokers and event management.

---

## 3. Debugging Is Harder

Tracing event flow across multiple services can be challenging.

---

## 4. Duplicate Message Handling

Subscribers should be idempotent because duplicate events may occur.

---

## 5. Delivery Guarantees

Different brokers provide different delivery semantics, requiring careful design.

---

# Real-World Examples

## E-Commerce

Order Created event triggers:

- Payment Service.
- Inventory Service.
- Shipping Service.
- Notification Service.

---

## Social Media

New Post event triggers:

- Feed Generation.
- Notifications.
- Search Indexing.
- Analytics.

---

## Banking

Transaction Completed event triggers:

- Fraud Detection.
- Notifications.
- Reporting.
- Audit Logging.

---

# When to Use

Use Publish-Subscribe when:

- Multiple services react to the same event.
- Services should remain loosely coupled.
- Asynchronous communication is acceptable.
- New consumers may be added in the future.

---

# When NOT to Use

Avoid Publish-Subscribe when:

- Immediate responses are required.
- Only one consumer processes a request.
- Strong synchronous consistency is required.

---

# Comparison

| Feature | Request-Response | Publish-Subscribe |
|---|---|---|
| Communication | Synchronous | Asynchronous |
| Coupling | Higher | Lower |
| Communication Type | One-to-One | One-to-Many |
| Response | Immediate | Event Driven |
| Scalability | Moderate | High |

---

# Interview Questions

## 1. What is the Publish-Subscribe pattern?

A messaging pattern where publishers send events to a topic and subscribers receive them asynchronously.

---

## 2. What is the role of a message broker?

The broker receives published messages and delivers them to all subscribed consumers.

---

## 3. How is Pub/Sub different from Request-Response?

Request-Response is synchronous and direct.

Publish-Subscribe is asynchronous and broker-based.

---

## 4. Can multiple subscribers receive the same event?

Yes. That is one of the primary advantages of the Pub/Sub pattern.

---

## 5. Name some technologies that implement Pub/Sub.

- Apache Kafka
- RabbitMQ
- Amazon SNS
- Google Cloud Pub/Sub
- Azure Event Grid

---

# Key Takeaways

- Publish-Subscribe enables asynchronous one-to-many communication.
- Publishers and subscribers are loosely coupled.
- Message brokers handle event distribution.
- It is widely used in event-driven architectures.
- Pub/Sub improves scalability, extensibility, and fault isolation.

---

## Previous & Next

← Previous: [Request-Response](01-Request-Response.md)

→ Next: [Fan-Out](03-Fan-Out.md)