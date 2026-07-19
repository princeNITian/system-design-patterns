# Event-Driven Architecture (EDA)

## Introduction

Event-Driven Architecture (EDA) is an architectural style in which services communicate by producing and consuming events instead of directly calling one another.

An **event** represents something that has already happened, such as an order being placed, a payment being completed, or a user signing up.

Instead of waiting for an immediate response, services react to events asynchronously, making the system more scalable and loosely coupled.

---

## Why was it Introduced?

Traditional synchronous communication creates tight coupling between services.

For example, if the Order Service directly calls the Inventory, Payment, and Notification services, a failure in one service can delay or fail the entire request.

Event-Driven Architecture was introduced to:

- Reduce coupling between services.
- Improve scalability.
- Increase system resilience.
- Enable asynchronous processing.
- Support real-time event processing.

---

## Architecture Diagram

```text
                 Event Producer
                       │
             Publishes an Event
                       │
                       ▼
               Message Broker
          (Kafka / RabbitMQ / SNS)
           ┌──────────┼──────────┐
           ▼          ▼          ▼
   Inventory     Notification   Analytics
     Service         Service      Service
```

The producer publishes an event to a message broker, and multiple consumers process the event independently.

---

## How It Works

When an important action occurs, a service publishes an event to a message broker.

Interested services subscribe to the event and process it independently.

For example:

1. Customer places an order.
2. Order Service publishes an **Order Created** event.
3. Inventory Service reserves stock.
4. Notification Service sends a confirmation.
5. Analytics Service updates reports.

The Order Service does not need to know who consumes the event.

---

## Core Characteristics

- Asynchronous communication.
- Loose coupling between services.
- Event producers and consumers are independent.
- Supports multiple consumers.
- Highly scalable.
- Fault tolerant.
- Event-based workflows.

---

## Advantages

- Loose coupling between services.
- Improved scalability.
- Better fault isolation.
- Easier integration of new services.
- Supports real-time processing.
- Multiple services can react to the same event.
- Better system extensibility.

---

## Disadvantages

- Increased architectural complexity.
- Eventual consistency.
- More difficult debugging.
- Event ordering challenges.
- Duplicate event handling.
- Monitoring distributed events can be difficult.

---

## Real-World Examples

Event-Driven Architecture is widely used by:

- Amazon
- Netflix
- Uber
- LinkedIn
- Spotify
- PayPal

Common use cases include:

- Order processing
- Payment notifications
- Email notifications
- Activity feeds
- Analytics pipelines
- Fraud detection

---

## When to Use

Use Event-Driven Architecture when:

- Multiple services need the same information.
- High scalability is required.
- Asynchronous processing is acceptable.
- Loose coupling is important.
- Events trigger downstream workflows.

---

## When NOT to Use

Avoid Event-Driven Architecture when:

- Immediate responses are required.
- Business logic is simple.
- Strong consistency is mandatory.
- The application is small.
- Additional infrastructure is unnecessary.

---

## Comparison

| Feature | Request-Response | Event-Driven |
|----------|------------------|--------------|
| Communication | Synchronous | Asynchronous |
| Coupling | Higher | Lower |
| Response | Immediate | Eventual |
| Scalability | Moderate | High |
| Fault Tolerance | Lower | Higher |

---

## Interview Questions

### 1. What is an event?

An event is a record that something has already happened within the system.

---

### 2. What is Event-Driven Architecture?

It is an architectural style where services communicate by publishing and consuming events instead of making direct synchronous calls.

---

### 3. What are the benefits of Event-Driven Architecture?

Loose coupling, scalability, fault tolerance, extensibility, and asynchronous processing.

---

### 4. What are common message brokers?

Apache Kafka, RabbitMQ, Amazon SNS, Amazon SQS, Google Pub/Sub, and Azure Service Bus.

---

### 5. What is the biggest challenge in Event-Driven Architecture?

Managing eventual consistency, duplicate events, event ordering, and debugging distributed event flows.

---

## Key Takeaways

- Event-Driven Architecture enables asynchronous communication through events.
- Producers publish events without knowing the consumers.
- Message brokers distribute events to interested services.
- The architecture improves scalability, flexibility, and fault isolation.
- It is ideal for loosely coupled, distributed systems.
- Eventual consistency is a common trade-off.

---

## Previous & Next

← Previous: [Microservice Architecture (SOA)](05-Microservices.md)

→ Next: [Serverless Architecture](07-Serverless-Architecture.md)