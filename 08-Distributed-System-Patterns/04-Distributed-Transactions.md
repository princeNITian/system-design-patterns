# Distributed Transactions

## Introduction

Distributed Transactions are a distributed system pattern that **ensure a single logical transaction maintains data consistency across multiple independent services or databases**.

Unlike a traditional database transaction, where all operations occur within a single database, a distributed transaction spans multiple systems that may fail independently.

The main goals of Distributed Transactions are:

- Maintain data consistency across services.
- Coordinate multiple operations.
- Handle partial failures safely.
- Ensure all participating systems reach a consistent outcome.

---

## Why were they Introduced?

Consider an e-commerce application.

Creating an order involves multiple services:

```text
Order Service

Inventory Service

Payment Service

Shipping Service
```

Suppose the following occurs:

```text
Order Created ✓

Inventory Reserved ✓

Payment Failed ✗

Shipment Not Created
```

Without coordination:

- The order exists.
- Inventory remains reserved.
- Payment failed.
- System state becomes inconsistent.

Distributed Transactions ensure all participating services either complete successfully or recover to a consistent state.

---

## Architecture Diagram

```text
                 Client

                    |

                    ▼

         Transaction Coordinator

     /         |          |         \

    ▼          ▼          ▼          ▼

Order     Inventory   Payment   Shipping

 Service    Service    Service    Service
```

The coordinator manages the transaction across all participating services.

---

## How It Works

The general flow:

```text
1. Client starts a transaction.

2. Coordinator contacts participating services.

3. Each service performs its operation.

4. Coordinator determines success or failure.

5. Commit or recovery actions are executed.

6. All services reach a consistent final state.
```

Example:

```text
Create Order

↓

Reserve Inventory

↓

Process Payment

↓

Create Shipment

↓

Complete Transaction
```

If a failure occurs:

```text
Create Order

↓

Reserve Inventory

↓

Payment Failed

↓

Recover Previous Operations
```

---

# Core Characteristics

## 1. Multiple Participants

Several independent services or databases participate in the same transaction.

---

## 2. Coordinated Execution

A coordinator or orchestration mechanism manages transaction progress.

---

## 3. Failure Handling

Partial failures are detected and handled appropriately.

---

## 4. Consistent Outcome

All participants eventually reach a consistent state.

---

## 5. Atomic Business Process

The overall business operation behaves as one logical transaction.

---

# Common Approaches

## 1. Two-Phase Commit (2PC)

Provides atomic commit through a prepare and commit protocol.

---

## 2. Three-Phase Commit (3PC)

Extends 2PC by reducing blocking during failures.

---

## 3. Saga Pattern

Coordinates long-running transactions using local transactions and compensating actions.

---

## 4. Event-Driven Coordination

Services communicate through events while maintaining eventual consistency.

---

# Advantages

## 1. Business Consistency

Related operations complete in a coordinated manner.

---

## 2. Reliable Failure Recovery

The system can recover from partial failures.

---

## 3. Supports Distributed Architectures

Enables complex workflows across multiple services.

---

## 4. Data Integrity

Prevents inconsistent business state.

---

## 5. Flexible Implementation

Supports both strong consistency and eventual consistency approaches.

---

# Disadvantages

## 1. Higher Complexity

Distributed coordination is significantly more complex than local transactions.

---

## 2. Increased Latency

Multiple services must participate before completion.

---

## 3. Failure Handling

Network failures complicate transaction management.

---

## 4. Scalability Challenges

Strong coordination can reduce throughput.

---

## 5. Operational Overhead

Monitoring and debugging distributed transactions require additional tooling.

---

# Real-World Examples

## E-Commerce

Order, inventory, payment, and shipping services participate in a single business workflow.

---

## Banking

Funds are transferred across multiple accounts or banking systems.

---

## Airline Booking

Seat reservation, payment, and ticket generation occur as one logical transaction.

---

## Travel Booking

Hotel, flight, and car rental services coordinate a complete booking.

---

# When to Use

Use Distributed Transactions when:

- Multiple services participate in one business operation.
- Data consistency is important.
- Partial failures must be handled safely.
- Business workflows span several databases or microservices.

---

# When NOT to Use

Avoid Distributed Transactions when:

- Operations are independent.
- Eventual consistency is sufficient.
- High throughput is more important than strict coordination.

---

# Comparison

| Feature | Local Transaction | Distributed Transaction |
|---|---|---|
| Scope | Single Database | Multiple Services or Databases |
| Coordinator | Database | External Coordinator or Workflow |
| Complexity | Low | High |
| Latency | Lower | Higher |
| Failure Handling | Simpler | More Complex |

---

# Interview Questions

## 1. What is a Distributed Transaction?

A transaction that coordinates operations across multiple services or databases while maintaining overall consistency.

---

## 2. Why are Distributed Transactions needed?

Because modern distributed applications frequently execute business operations across multiple independent systems.

---

## 3. What are common implementations of Distributed Transactions?

- Two-Phase Commit (2PC)
- Three-Phase Commit (3PC)
- Saga Pattern
- Event-Driven Coordination

---

## 4. Why are Distributed Transactions more difficult than local transactions?

Because multiple systems can fail independently and communicate over unreliable networks.

---

## 5. Where are Distributed Transactions commonly used?

- E-commerce
- Banking
- Airline booking
- Travel reservation
- Enterprise workflow systems

---

# Key Takeaways

- Distributed Transactions coordinate operations across multiple services.
- They ensure business consistency despite partial failures.
- Several implementation strategies exist, including 2PC, 3PC, and Saga.
- They introduce additional coordination, latency, and operational complexity.
- Choosing the right approach depends on consistency requirements and system design.

---

## Previous & Next

← Previous: [Quorum](03-Quorum.md)

→ Next: [Two-Phase Commit (2PC)](05-Two-Phase-Commit-2PC.md)