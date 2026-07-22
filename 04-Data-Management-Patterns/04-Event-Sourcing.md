# Event Sourcing

## Introduction

Event Sourcing is a data management pattern where **application state is stored as a sequence of events instead of storing only the current state**.

Rather than updating a database record directly, every change is recorded as an immutable event. The current state is reconstructed by replaying these events.

The main goals of Event Sourcing are:

- Preserve a complete history of changes.
- Enable event replay.
- Improve auditability.
- Support event-driven architectures.

---

## Why was it Introduced?

Traditional applications store only the latest state.

Example:

```text
Bank Account

Current Balance = ₹10,000
```

Questions like these become difficult to answer:

- How did the balance reach ₹10,000?
- Who made the last change?
- Can the system reconstruct yesterday's state?

Event Sourcing solves this by storing every change as an event.

---

## Architecture Diagram

```text
             Client

                |

                ▼

         Command Handler

                |

                ▼

          Event Store

                |

      ---------------------

      |         |         |

      ▼         ▼         ▼

 Read Model  Audit Log  Analytics
```

The Event Store becomes the source of truth.

---

## How It Works

The communication flow:

```text
1. Client sends a command.

2. Command is validated.

3. A business event is created.

4. Event is stored in the Event Store.

5. Read Models are updated.

6. Current state is rebuilt by replaying events.
```

Example:

```text
Account Created

↓

Money Deposited

↓

Money Withdrawn

↓

Money Deposited

↓

Current Balance
```

The balance is calculated by replaying all events.

---

# Core Components

## 1. Command

Represents an intention to change data.

Examples:

- Create Order
- Deposit Money
- Cancel Booking

---

## 2. Event

Represents something that has already happened.

Examples:

- Order Created
- Money Deposited
- Payment Completed

Events are immutable.

---

## 3. Event Store

Stores every event in chronological order.

---

## 4. Read Model

Provides optimized query access.

Often implemented using CQRS.

---

## 5. Event Replay

Reconstructs application state by replaying stored events.

---

# Core Characteristics

## 1. Immutable Events

Events are never updated or deleted.

---

## 2. Complete Audit Trail

Every business change is permanently recorded.

---

## 3. Event Replay

Application state can be rebuilt at any time.

---

## 4. Event-Driven Integration

Other services can subscribe to stored events.

---

## 5. Separation of Write and Read

Often used together with CQRS.

---

# Advantages

## 1. Full History

Every state change is preserved.

---

## 2. Excellent Auditability

Ideal for financial and regulated systems.

---

## 3. Easy Recovery

State can be rebuilt from events.

---

## 4. Supports CQRS

Read models can be regenerated at any time.

---

## 5. Enables Event Replay

Historical events can be reprocessed for new business requirements.

---

# Disadvantages

## 1. Increased Complexity

Requires an event store and replay logic.

---

## 2. Event Versioning

Changing event structures over time requires careful management.

---

## 3. Storage Growth

Events accumulate continuously.

---

## 4. Learning Curve

Developers must think in terms of events instead of current state.

---

## 5. Eventual Consistency

Read models are typically updated asynchronously.

---

# Real-World Examples

## Banking

Events:

- Account Created
- Deposit
- Withdrawal
- Transfer

---

## E-Commerce

Events:

- Order Created
- Payment Completed
- Inventory Reserved
- Order Shipped

---

## Trading Platforms

Events:

- Buy Order Placed
- Trade Executed
- Settlement Completed

---

## Audit Systems

Maintain a permanent history of every business operation.

---

# When to Use

Use Event Sourcing when:

- Complete audit history is required.
- Business events are valuable.
- State reconstruction is important.
- Building event-driven systems.
- CQRS is already being used.

---

# When NOT to Use

Avoid Event Sourcing when:

- Applications are simple CRUD systems.
- Historical events have little business value.
- Operational simplicity is preferred.
- Storage costs outweigh the benefits.

---

# Comparison

| Feature | Traditional CRUD | Event Sourcing |
|---|---|---|
| Stored Data | Current state | Sequence of events |
| Audit History | Limited | Complete |
| Replay | No | Yes |
| Recovery | Backup dependent | Replay events |
| Complexity | Lower | Higher |

---

# Interview Questions

## 1. What is Event Sourcing?

A pattern that stores application state as a sequence of immutable events rather than only the latest state.

---

## 2. What is an Event Store?

A database that stores business events in chronological order.

---

## 3. How is current state obtained?

By replaying all relevant events from the Event Store.

---

## 4. Is Event Sourcing usually used with CQRS?

Yes.

CQRS commonly provides optimized read models while Event Sourcing maintains the complete write history.

---

## 5. Where is Event Sourcing commonly used?

- Banking.
- Trading systems.
- E-commerce.
- Audit systems.
- Event-driven architectures.

---

# Key Takeaways

- Event Sourcing stores every business event instead of only the latest state.
- Events are immutable and provide a complete audit trail.
- Current state is rebuilt by replaying events.
- It is commonly combined with CQRS.
- It is ideal for systems requiring traceability and historical reconstruction.

---

## Previous & Next

← Previous: [CQRS](03-CQRS.md)

→ Next: [Materialized View](05-Materialized-View.md)