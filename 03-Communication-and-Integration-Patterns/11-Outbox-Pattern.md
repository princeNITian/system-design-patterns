# Outbox Pattern

## Introduction

The Outbox Pattern is a reliability pattern used to ensure that **database updates and event publishing happen reliably together**.

Instead of directly publishing an event after updating the database, the application first stores the event in an **Outbox table** within the same database transaction. A separate process then publishes the event to a message broker.

The main goals of the Outbox Pattern are:

- Prevent data loss.
- Ensure reliable event publishing.
- Maintain consistency between the database and message broker.
- Eliminate dual-write problems.

---

## Why was it Introduced?

Consider an Order Service.

After creating an order, it should publish an **Order Created** event.

```text
Create Order

      |

      ▼

Save to Database

      |

      ▼

Publish Event
```

Problem:

What if the database update succeeds, but event publishing fails?

```text
Database Updated ✅

Event Published ❌
```

Other services never receive the event, leading to inconsistent systems.

The Outbox Pattern solves this by storing both operations in the same database transaction.

---

## Architecture Diagram

```text
              Application

                   |

                   ▼

        Database Transaction

       ┌────────────┴────────────┐

       ▼                         ▼

 Orders Table            Outbox Table

                                   |

                                   ▼

                         Outbox Processor

                                   |

                                   ▼

                           Message Broker

                                   |

                                   ▼

                              Consumers
```

---

## How It Works

The communication flow:

```text
1. Client sends a request.

2. Application updates business data.

3. Application inserts an event into the Outbox table.

4. Database transaction commits.

5. Outbox processor reads pending events.

6. Event is published to the message broker.

7. Event is marked as processed.
```

Example:

```text
Create Order

      |

Orders Table Updated

      |

Outbox Table Updated

      |

Transaction Commit

      |

Background Publisher

      |

Kafka
```

---

# Core Components

## 1. Business Table

Stores application data.

Example:

```text
Orders
```

---

## 2. Outbox Table

Stores events waiting to be published.

Example:

```text
OrderCreated
PaymentCompleted
OrderCancelled
```

---

## 3. Outbox Processor

Reads unpublished events and publishes them.

---

## 4. Message Broker

Delivers events to downstream services.

Examples:

- Apache Kafka
- RabbitMQ
- Amazon SQS

---

# Core Characteristics

## 1. Single Database Transaction

Business data and event records are saved together.

---

## 2. Reliable Event Publishing

Events cannot be lost after a successful transaction.

---

## 3. Asynchronous Delivery

Events are published after the database transaction commits.

---

## 4. Retry Support

Failed publications can be retried safely.

---

## 5. Event Persistence

Events remain in the Outbox table until successfully published.

---

# Advantages

## 1. Prevents Data Loss

Events are never lost after successful database updates.

---

## 2. Eliminates Dual-Write Problem

Database update and event creation occur atomically.

---

## 3. Improves Reliability

Temporary broker failures do not lose events.

---

## 4. Supports Retries

Failed events remain available for later processing.

---

## 5. Works Well with Microservices

Ensures consistent communication between services.

---

# Disadvantages

## 1. Additional Storage

Requires maintaining an Outbox table.

---

## 2. Increased Complexity

A background publisher must be implemented.

---

## 3. Eventual Consistency

Consumers receive events after the transaction commits.

---

## 4. Duplicate Publishing

Publishers may retry sending events.

Consumers should therefore be idempotent.

---

## 5. Cleanup Required

Processed Outbox records should be archived or deleted.

---

# Real-World Examples

## E-Commerce

After an order is created:

- Save the order.
- Store an Order Created event.
- Publish the event later.

---

## Banking

After a money transfer:

- Update account balances.
- Store a Transaction Completed event.
- Publish the event reliably.

---

## Inventory Systems

After inventory changes:

- Update stock.
- Publish inventory events.

---

# When to Use

Use the Outbox Pattern when:

- Database updates must trigger events.
- Message delivery must be reliable.
- Microservices communicate through events.
- Losing events is unacceptable.

---

# When NOT to Use

Avoid the Outbox Pattern when:

- Applications are monolithic with no messaging.
- Event publishing is not required.
- Occasional event loss is acceptable.

---

# Comparison

| Feature | Direct Event Publishing | Outbox Pattern |
|---|---|---|
| Reliability | Lower | High |
| Data Loss Risk | Possible | Very Low |
| Retry Support | Limited | Built-in |
| Complexity | Low | Higher |
| Event Consistency | Not Guaranteed | Guaranteed after transaction |

---

# Interview Questions

## 1. What problem does the Outbox Pattern solve?

It prevents inconsistencies caused by successful database updates but failed event publishing.

---

## 2. What is the dual-write problem?

The challenge of updating two separate systems (database and message broker) where one operation succeeds and the other fails.

---

## 3. Why is the Outbox table stored in the same database?

To ensure both the business data and the event are committed atomically in a single transaction.

---

## 4. Can duplicate events occur?

Yes. The publisher may retry failed deliveries, so consumers should be idempotent.

---

## 5. Where is the Outbox Pattern commonly used?

- Microservices.
- Event-driven architectures.
- Financial systems.
- E-commerce platforms.

---

# Key Takeaways

- The Outbox Pattern guarantees reliable event publishing.
- Business data and events are stored in the same transaction.
- A background process publishes events to the message broker.
- It eliminates the dual-write problem.
- It is one of the most common reliability patterns in modern microservices.

---

## Previous & Next

← Previous: [Webhook](10-Webhook.md)

→ Next: [Inbox Pattern](12-Inbox-Pattern.md)