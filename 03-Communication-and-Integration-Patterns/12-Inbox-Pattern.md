# Inbox Pattern

## Introduction

The Inbox Pattern is a reliability pattern used to ensure that **each incoming event is processed exactly once from the application's perspective**, even if the message broker delivers the same event multiple times.

Instead of directly processing every received event, the application first records the event in an **Inbox table**. If the same event arrives again, it is recognized as a duplicate and ignored.

The main goals of the Inbox Pattern are:

- Prevent duplicate processing.
- Ensure idempotent event handling.
- Improve reliability.
- Support at-least-once message delivery.

---

## Why was it Introduced?

Most message brokers provide **at-least-once delivery**.

This means a message may be delivered more than once.

Example:

```text
Payment Completed Event

        |

        ▼

Inventory Service

        |

Network Failure

        |

Broker Retries

        |

Payment Completed Event Again
```

Without duplicate detection:

- Inventory could decrease twice.
- Emails could be sent multiple times.
- Customers could be charged twice.

The Inbox Pattern prevents duplicate processing.

---

## Architecture Diagram

```text
          Message Broker

                 |

                 ▼

        Consumer Application

                 |

        Check Inbox Table

        /             \

 Event Exists?       Event New?

      |                  |

 Ignore Event      Save Event

                         |

                         ▼

                Execute Business Logic

                         |

                         ▼

                 Mark as Processed
```

---

## How It Works

The communication flow:

```text
1. Consumer receives an event.

2. Check the Inbox table.

3. If the event already exists:
      Ignore it.

4. Otherwise:
      Store the event.

5. Execute business logic.

6. Mark the event as processed.
```

Example:

```text
Order Created Event

        |

Inbox Table

        |

Already Exists?

        |

Yes

        |

Ignore Event
```

---

# Core Components

## 1. Message Broker

Delivers events.

Examples:

- Kafka
- RabbitMQ
- Amazon SQS

---

## 2. Consumer

Receives events from the broker.

---

## 3. Inbox Table

Stores processed event identifiers.

Example:

```text
Event ID

Status

Processed Time
```

---

## 4. Business Logic

Processes the event only once.

---

# Core Characteristics

## 1. Duplicate Detection

Previously processed events are identified.

---

## 2. Idempotent Processing

Each event affects the system only once.

---

## 3. Reliable Consumption

Supports at-least-once delivery guarantees.

---

## 4. Persistent Storage

Processed event information is stored in a database.

---

## 5. Retry Safe

Repeated deliveries do not cause duplicate business operations.

---

# Advantages

## 1. Prevents Duplicate Processing

Each event is processed only once.

---

## 2. Improves Reliability

Network failures no longer cause repeated business actions.

---

## 3. Supports Retries

Consumers can safely retry failed processing.

---

## 4. Works with Existing Brokers

No changes to the messaging system are required.

---

## 5. Complements the Outbox Pattern

Provides reliable event consumption while the Outbox Pattern provides reliable event publishing.

---

# Disadvantages

## 1. Additional Storage

Requires maintaining an Inbox table.

---

## 2. Increased Complexity

Consumers must check and update the Inbox table.

---

## 3. Cleanup Required

Old processed events should be archived or deleted periodically.

---

## 4. Database Overhead

Each message requires an additional database lookup.

---

## 5. Eventual Consistency

Processing still occurs asynchronously.

---

# Real-World Examples

## E-Commerce

Prevent duplicate:

- Order processing.
- Inventory updates.
- Shipping requests.

---

## Banking

Prevent duplicate:

- Money transfers.
- Balance updates.
- Transaction records.

---

## Notification Systems

Prevent sending:

- Duplicate emails.
- Duplicate SMS.
- Duplicate push notifications.

---

# When to Use

Use the Inbox Pattern when:

- Messages may be delivered more than once.
- Duplicate processing is unacceptable.
- Reliable event consumption is required.
- Building event-driven microservices.

---

# When NOT to Use

Avoid the Inbox Pattern when:

- Duplicate processing has no business impact.
- Messaging is not used.
- The system already guarantees exactly-once processing for your use case.

---

# Comparison

| Feature | Normal Consumer | Inbox Pattern |
|---|---|---|
| Duplicate Protection | No | Yes |
| Idempotency | Application-specific | Built-in with Inbox table |
| Reliability | Moderate | High |
| Database Lookup | No | Yes |
| Complexity | Low | Higher |

---

# Interview Questions

## 1. What problem does the Inbox Pattern solve?

It prevents duplicate processing when the same event is delivered multiple times.

---

## 2. Why do duplicate events occur?

Because most messaging systems provide **at-least-once delivery**, meaning retries can result in duplicate messages.

---

## 3. What is stored in the Inbox table?

Typically:

- Event ID.
- Processing status.
- Timestamp.
- Metadata.

---

## 4. How is the Inbox Pattern related to the Outbox Pattern?

- Outbox ensures reliable **event publishing**.
- Inbox ensures reliable **event consumption**.

Together, they provide end-to-end reliable messaging.

---

## 5. Where is the Inbox Pattern commonly used?

- Financial systems.
- E-commerce platforms.
- Event-driven microservices.
- Payment processing systems.

---

# Key Takeaways

- The Inbox Pattern prevents duplicate event processing.
- It records processed events in an Inbox table.
- It enables idempotent consumers.
- It complements the Outbox Pattern.
- It is widely used in reliable event-driven architectures.

---

## Previous & Next

← Previous: [Outbox Pattern](11-Outbox-Pattern.md)

→ Next: [Saga Orchestration](13-Saga-Orchestration.md)