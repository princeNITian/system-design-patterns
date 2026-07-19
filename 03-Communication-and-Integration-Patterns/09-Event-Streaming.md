# Event Streaming

## Introduction

Event Streaming is a communication pattern where events are continuously produced, stored, and consumed as an ordered stream.

Unlike traditional messaging, where messages are removed after being processed, event streams are typically retained for a configurable period, allowing multiple consumers to read the same events independently.

The main goals of Event Streaming are:

- Process events in real time.
- Handle massive data volumes.
- Support multiple independent consumers.
- Maintain an ordered event log.
- Enable replay of historical events.

---

## Why was it Introduced?

Traditional message queues work well for background processing, but they have limitations:

- Messages are often deleted after consumption.
- New consumers cannot process historical events.
- Large-scale event analytics become difficult.

Modern applications generate millions of events every second.

Examples:

- User clicks.
- Payment transactions.
- IoT sensor readings.
- Log events.
- Stock market updates.

Event Streaming enables continuous processing of these event streams.

---

## Architecture Diagram

```text
             Producers

        /       |       \

       ▼        ▼        ▼

 Order Service  App  IoT Devices

                |

                ▼

         Event Streaming Platform

                |

      ┌─────────┼─────────┐

      ▼         ▼         ▼

 Analytics   Notification   Search

      ▼         ▼         ▼

 Independent Consumers
```

---

## How It Works

The communication flow:

```text
1. Producers generate events.

2. Events are written to an event stream.

3. Events are stored in order.

4. Multiple consumers read events independently.

5. Consumers maintain their own reading position.
```

Example:

```text
User Login Event

        |

        ▼

Kafka Topic

        |

        ├── Fraud Detection

        ├── Analytics

        ├── Notification

        └── Audit Logging
```

---

# Core Components

## 1. Producer

Generates events.

Example:

```text
Payment Service
```

---

## 2. Event Stream

An ordered sequence of events.

Example:

```text
payments
```

---

## 3. Broker

Stores and distributes events.

Examples:

- Apache Kafka
- Apache Pulsar
- Amazon Kinesis
- Redpanda

---

## 4. Consumer

Reads events from the stream.

Each consumer tracks its own progress independently.

---

# Core Characteristics

## 1. Ordered Events

Events are stored in the order they are produced.

---

## 2. Event Retention

Events remain available even after being consumed.

---

## 3. Multiple Independent Consumers

Each consumer processes events independently.

---

## 4. Replay Capability

Consumers can reprocess historical events.

---

## 5. High Throughput

Designed to process millions of events per second.

---

# Advantages

## 1. Real-Time Processing

Events are processed almost immediately after they occur.

---

## 2. High Scalability

Supports massive event volumes.

---

## 3. Event Replay

Consumers can replay events for recovery or analytics.

---

## 4. Loose Coupling

Producers and consumers remain independent.

---

## 5. Fault Tolerance

Events remain available even if consumers are temporarily unavailable.

---

# Disadvantages

## 1. Operational Complexity

Streaming platforms require proper management and monitoring.

---

## 2. Event Ordering Challenges

Maintaining ordering across partitions requires careful design.

---

## 3. Storage Requirements

Retaining events increases storage usage.

---

## 4. Eventual Consistency

Consumers process events asynchronously.

---

## 5. Learning Curve

Concepts such as partitions, offsets, and consumer groups require additional understanding.

---

# Real-World Examples

## E-Commerce

Stream:

- Orders.
- Payments.
- Inventory updates.

---

## Banking

Process:

- Transactions.
- Fraud detection.
- Audit events.

---

## Social Media

Stream:

- Posts.
- Likes.
- Comments.
- Notifications.

---

## IoT Platforms

Continuously process:

- Sensor readings.
- Device status.
- Telemetry.

---

# When to Use

Use Event Streaming when:

- Events are generated continuously.
- Real-time analytics are required.
- Multiple systems consume the same events.
- Historical event replay is important.
- High throughput is needed.

---

# When NOT to Use

Avoid Event Streaming when:

- Communication is simple and synchronous.
- Event replay is unnecessary.
- Application traffic is very small.
- Operational complexity cannot be justified.

---

# Comparison

| Feature | Message Queue | Event Streaming |
|---|---|---|
| Message Lifetime | Usually removed after consumption | Retained for a configured period |
| Replay | Generally No | Yes |
| Consumer Tracking | Queue manages delivery | Consumer manages offsets |
| Throughput | High | Very High |
| Best For | Background jobs | Real-time event processing |

---

# Interview Questions

## 1. What is Event Streaming?

A communication pattern where events are continuously produced, stored, and consumed as an ordered stream.

---

## 2. How is Event Streaming different from a Message Queue?

Message queues typically remove messages after processing.

Event streaming platforms retain events, allowing multiple consumers to replay and process them independently.

---

## 3. What is an offset?

An offset represents the position of a consumer within an event stream.

---

## 4. Name some Event Streaming platforms.

- Apache Kafka
- Apache Pulsar
- Amazon Kinesis
- Redpanda

---

## 5. Where is Event Streaming commonly used?

- Real-time analytics.
- Fraud detection.
- Activity tracking.
- IoT systems.
- Log aggregation.

---

# Key Takeaways

- Event Streaming stores events as an ordered stream.
- Multiple consumers can process the same events independently.
- Events can be replayed when needed.
- It provides extremely high throughput.
- Event Streaming powers many modern real-time distributed systems.

---

## Previous & Next

← Previous: [Message Broker](08-Message-Broker.md)

→ Next: [Webhook](10-Webhook.md)