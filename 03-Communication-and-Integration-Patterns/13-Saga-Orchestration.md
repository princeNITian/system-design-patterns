# Saga Orchestration

## Introduction

Saga Orchestration is a communication pattern used to manage **distributed transactions** across multiple microservices.

Instead of relying on a central database transaction, a dedicated **Saga Orchestrator** coordinates each step of the transaction and decides what should happen next.

If one step fails, the orchestrator executes **compensating transactions** to undo previously completed operations.

The main goals of Saga Orchestration are:

- Maintain data consistency across services.
- Coordinate distributed transactions.
- Handle failures gracefully.
- Eliminate the need for two-phase commit (2PC).

---

## Why was it Introduced?

In a monolithic application, a database transaction ensures that all operations either succeed or fail together.

Example:

```text
BEGIN TRANSACTION

Create Order

Update Inventory

Process Payment

COMMIT
```

In microservices:

- Order Service has its own database.
- Payment Service has its own database.
- Inventory Service has its own database.

A single database transaction is no longer possible.

Saga Orchestration coordinates these services while maintaining consistency.

---

## Architecture Diagram

```text
                 Client

                    |

                    ▼

           Saga Orchestrator

        /         |          \

       ▼          ▼           ▼

 Order Service  Payment   Inventory
                 Service     Service

        \         |          /

         \        |         /

             Compensation
```

The orchestrator manages every step of the workflow.

---

## How It Works

The communication flow:

```text
1. Client starts a transaction.

2. Orchestrator calls Order Service.

3. Order Service succeeds.

4. Orchestrator calls Payment Service.

5. Payment succeeds.

6. Orchestrator calls Inventory Service.

7. Inventory succeeds.

8. Transaction completes.
```

If Inventory fails:

```text
Inventory Failed

        |

Compensate Payment

        |

Compensate Order

        |

Saga Ends
```

---

# Core Components

## 1. Saga Orchestrator

Coordinates the entire transaction.

---

## 2. Participant Services

Each service performs one business operation.

Example:

- Order Service
- Payment Service
- Inventory Service

---

## 3. Compensating Transaction

Reverses a previously completed operation.

Example:

```text
Reserve Inventory

↓

Release Inventory
```

---

## 4. Local Transaction

Each service updates only its own database.

---

# Core Characteristics

## 1. Central Coordination

A single orchestrator controls the workflow.

---

## 2. Distributed Transactions

Business transactions span multiple services.

---

## 3. Compensation

Failures trigger rollback operations through compensating actions.

---

## 4. Service Independence

Each service owns its own data.

---

## 5. Eventual Consistency

The overall system becomes consistent after the saga completes.

---

# Advantages

## 1. Eliminates Distributed Database Transactions

Each service manages its own database.

---

## 2. Centralized Workflow

Business logic is easier to understand.

---

## 3. Easier Error Handling

The orchestrator manages failures consistently.

---

## 4. Better Visibility

The entire transaction can be monitored from one place.

---

## 5. Microservice Friendly

Works well with independent services.

---

# Disadvantages

## 1. Orchestrator Becomes Critical

If the orchestrator fails, transaction progress may stop.

---

## 2. Additional Complexity

Requires orchestration logic and compensation handling.

---

## 3. Compensating Actions

Not every operation can be easily reversed.

---

## 4. Eventual Consistency

Data may be temporarily inconsistent while the saga executes.

---

## 5. Performance Overhead

Multiple service calls increase latency.

---

# Real-World Examples

## E-Commerce

Transaction flow:

- Create Order.
- Process Payment.
- Reserve Inventory.
- Arrange Shipping.

---

## Banking

Transfer money between accounts.

If credit fails:

- Reverse debit.

---

## Travel Booking

Book:

- Flight.
- Hotel.
- Rental Car.

If hotel booking fails:

- Cancel flight.
- Cancel car reservation.

---

# When to Use

Use Saga Orchestration when:

- Multiple microservices participate in one business transaction.
- Each service owns its own database.
- Distributed consistency is required.
- Compensation is possible.

---

# When NOT to Use

Avoid Saga Orchestration when:

- A single database transaction is sufficient.
- Business operations are simple.
- Compensation cannot be implemented.

---

# Comparison

| Feature | Database Transaction | Saga Orchestration |
|---|---|---|
| Scope | Single Database | Multiple Services |
| Coordinator | Database | Saga Orchestrator |
| Rollback | Automatic | Compensation |
| Consistency | Strong | Eventual |
| Scalability | Limited | High |

---

# Interview Questions

## 1. What is Saga Orchestration?

A pattern where a central orchestrator coordinates distributed transactions across multiple microservices.

---

## 2. Why do we need Saga Orchestration?

Because traditional database transactions cannot span multiple independent microservice databases.

---

## 3. What is a compensating transaction?

A business operation that reverses a previously completed action.

---

## 4. Is Saga Orchestration strongly consistent?

No.

It provides **eventual consistency** using compensation instead of database rollbacks.

---

## 5. Where is Saga Orchestration commonly used?

- E-commerce.
- Banking.
- Travel booking.
- Order processing.
- Payment workflows.

---

# Key Takeaways

- Saga Orchestration manages distributed transactions.
- A central orchestrator controls the workflow.
- Each service performs a local transaction.
- Failures are handled using compensating transactions.
- It is one of the most common patterns for maintaining consistency in microservices.

---

## Previous & Next

← Previous: [Inbox Pattern](12-Inbox-Pattern.md)

→ Next: [Saga Choreography](14-Saga-Choreography.md)