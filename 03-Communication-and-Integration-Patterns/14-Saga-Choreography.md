# Saga Choreography

## Introduction

Saga Choreography is a communication pattern used to manage **distributed transactions** where **each service reacts to events independently**, without a central coordinator.

Instead of a single orchestrator controlling the workflow, every participating service listens for events, performs its own business logic, and publishes the next event.

The main goals of Saga Choreography are:

- Coordinate distributed transactions using events.
- Eliminate a central orchestrator.
- Increase service autonomy.
- Build loosely coupled microservices.

---

## Why was it Introduced?

Saga Orchestration introduces a central coordinator.

```text
          Saga Orchestrator

               |

      Order → Payment → Inventory
```

Although effective, the orchestrator becomes another component to manage.

Saga Choreography removes this coordinator.

Instead, services communicate through events.

```text
Order Created

      |

      ▼

Payment Service

      |

Payment Completed

      |

      ▼

Inventory Service

      |

Inventory Reserved
```

Each service decides what to do when it receives an event.

---

## Architecture Diagram

```text
          Order Service

                |

      Order Created Event

                |

                ▼

        Message Broker

                |

                ▼

       Payment Service

                |

   Payment Completed Event

                |

                ▼

        Message Broker

                |

                ▼

      Inventory Service

                |

 Inventory Reserved Event

                |

                ▼

      Shipping Service
```

No central coordinator exists.

---

## How It Works

The communication flow:

```text
1. Order Service creates an order.

2. Order Service publishes Order Created.

3. Payment Service receives the event.

4. Payment Service processes payment.

5. Payment Service publishes Payment Completed.

6. Inventory Service receives the event.

7. Inventory Service reserves stock.

8. Inventory Service publishes Inventory Reserved.

9. Shipping Service creates shipment.
```

If payment fails:

```text
Payment Failed

        |

Publish Payment Failed Event

        |

Order Service

        |

Cancel Order
```

Compensating actions are also driven by events.

---

# Core Components

## 1. Participant Services

Each service performs one business operation.

Examples:

- Order Service
- Payment Service
- Inventory Service
- Shipping Service

---

## 2. Events

Services communicate by publishing business events.

Examples:

```text
Order Created

Payment Completed

Inventory Reserved
```

---

## 3. Message Broker

Delivers events between services.

Examples:

- Apache Kafka
- RabbitMQ
- Amazon SNS/SQS

---

## 4. Compensating Transactions

Services publish failure events that trigger compensating actions in other services.

---

# Core Characteristics

## 1. No Central Coordinator

Each service controls its own behavior.

---

## 2. Event-Driven Communication

Services communicate only through events.

---

## 3. Loose Coupling

Services know only about events, not about each other.

---

## 4. Distributed Workflow

Business logic is distributed across multiple services.

---

## 5. Eventual Consistency

Consistency is achieved after all events have been processed.

---

# Advantages

## 1. No Single Point of Control

Removing the orchestrator eliminates a central dependency.

---

## 2. High Service Autonomy

Each service owns its business logic.

---

## 3. Loose Coupling

Services evolve independently.

---

## 4. High Scalability

New services can subscribe to events without modifying existing services.

---

## 5. Natural Fit for Event-Driven Architecture

Works well with messaging platforms such as Kafka.

---

# Disadvantages

## 1. Difficult to Understand

Business workflows are spread across multiple services.

---

## 2. Harder Debugging

Tracing a transaction requires following multiple events.

---

## 3. Complex Failure Handling

Compensation logic is distributed across services.

---

## 4. Event Dependency

Changes to business events may affect multiple consumers.

---

## 5. Monitoring Complexity

Distributed tracing is essential to understand transaction flow.

---

# Real-World Examples

## E-Commerce

Workflow:

- Order Created.
- Payment Completed.
- Inventory Reserved.
- Shipment Created.

Each service reacts independently.

---

## Banking

Money transfer events trigger:

- Debit Account.
- Credit Account.
- Notification.

---

## Travel Booking

Booking events trigger:

- Flight Reservation.
- Hotel Reservation.
- Car Rental.

Compensation events cancel previous reservations if needed.

---

# When to Use

Use Saga Choreography when:

- Services are event-driven.
- Loose coupling is important.
- There is no need for a central coordinator.
- Teams own independent microservices.

---

# When NOT to Use

Avoid Saga Choreography when:

- Business workflows are highly complex.
- A central view of the transaction is required.
- Teams struggle with distributed debugging.
- Tight workflow control is necessary.

---

# Comparison

| Feature | Saga Orchestration | Saga Choreography |
|---|---|---|
| Coordinator | Central Orchestrator | No Coordinator |
| Communication | Commands | Events |
| Coupling | Moderate | Low |
| Workflow Visibility | Easier | More Difficult |
| Scalability | High | Very High |

---

# Interview Questions

## 1. What is Saga Choreography?

A distributed transaction pattern where services communicate through events without a central coordinator.

---

## 2. How is Saga Choreography different from Saga Orchestration?

Saga Orchestration uses a central orchestrator.

Saga Choreography allows each service to react independently to events.

---

## 3. What happens when a step fails?

A failure event is published, triggering compensating actions in other services.

---

## 4. Which messaging systems are commonly used?

- Apache Kafka
- RabbitMQ
- Amazon SNS/SQS
- Apache Pulsar

---

## 5. When should you choose Saga Choreography?

When building highly event-driven microservices that benefit from loose coupling and decentralized coordination.

---

# Key Takeaways

- Saga Choreography manages distributed transactions using events.
- There is no central orchestrator.
- Services react independently to business events.
- Compensating actions are triggered through failure events.
- It is a powerful pattern for large-scale event-driven microservice architectures.

---

## Previous & Next

← Previous: [Saga Orchestration](13-Saga-Orchestration.md)

→ Next Module: [04-Data-Management-Patterns](../04-Data-Management-Patterns/README.md)