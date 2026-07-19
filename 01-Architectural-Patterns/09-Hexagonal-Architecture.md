# Hexagonal Architecture

## Introduction

Hexagonal Architecture, also known as **Ports and Adapters Architecture**, is an architectural style that separates the core business logic of an application from external systems.

The main idea is:

> The business logic should not depend on external technologies such as databases, APIs, frameworks, or user interfaces.

Instead, external systems interact with the application through well-defined interfaces called **ports** and their implementations called **adapters**.

This architecture improves testability, flexibility, and maintainability.

---

## Why was it Introduced?

Traditional application architectures often make business logic tightly coupled with external dependencies.

Example:

```text
Controller

   |
   ▼

Business Logic

   |
   ▼

Database Code
```

Problems:

- Business logic depends on database implementation.
- Changing frameworks becomes difficult.
- Testing requires external systems.
- Core logic becomes difficult to reuse.

Hexagonal Architecture was introduced to isolate the business rules from external concerns.

---

## Architecture Diagram

```text
                 External Systems

        UI        API       Database
         |         |           |
         ▼         ▼           ▼

      Adapter   Adapter    Adapter

             \     |     /

              Ports (Interfaces)

                    |

                    ▼

            Application Core

          (Business Logic)

                    |

              Domain Rules
```

The core application remains independent of external technologies.

---

## How It Works

The architecture is divided into three main parts:

```text
External World

      |
      ▼

Adapters

      |
      ▼

Ports

      |
      ▼

Application Core
```

### Example: Order System

A customer places an order.

```text
HTTP Request

      |

API Adapter

      |

Order Service Port

      |

Business Logic

      |

Database Adapter
```

The business logic does not know whether data comes from:

- REST API.
- Database.
- Message queue.
- File system.

It only interacts through interfaces.

---

## Core Characteristics

### 1. Application Core

The center of the system.

Contains:

- Business rules.
- Domain logic.
- Application workflows.

It should have no dependency on external systems.

---

### 2. Ports

Ports define how the application communicates with the outside world.

Examples:

```text
CreateOrder Interface

Payment Interface

UserRepository Interface
```

They define contracts without implementation details.

---

### 3. Adapters

Adapters implement ports and connect external systems.

Examples:

- REST Controller Adapter.
- Database Adapter.
- Kafka Adapter.
- External API Adapter.

---

### 4. Dependency Inversion

Dependencies point inward.

```text
External Systems

        ↓

Adapters

        ↓

Application Core
```

The core does not depend on infrastructure.

---

### 5. Technology Independence

The business logic can work with different technologies.

Example:

Replace:

```text
MySQL

with

MongoDB
```

without changing business rules.

---

## Advantages

### 1. Highly Testable

Business logic can be tested without:

- Databases.
- APIs.
- External services.

---

### 2. Easy Technology Replacement

External dependencies can be replaced easily.

Examples:

- Database migration.
- Framework changes.
- API changes.

---

### 3. Better Maintainability

Business logic remains clean and independent.

---

### 4. Improved Flexibility

Multiple interfaces can interact with the same application core.

Example:

```text
Web API

Mobile App

CLI Tool

Message Consumer

        |

        ▼

Application Core
```

---

### 5. Clear Separation of Concerns

Each component has a well-defined responsibility.

---

## Disadvantages

### 1. Additional Complexity

More interfaces and abstractions increase the number of components.

---

### 2. Overengineering for Small Applications

Simple applications may not need this level of separation.

---

### 3. More Initial Development Time

Creating ports and adapters requires additional design effort.

---

### 4. Learning Curve

Developers need to understand dependency inversion and domain-driven design concepts.

---

## Real-World Examples

### Banking Applications

Used for separating:

- Account rules.
- Payment logic.
- External banking integrations.

---

### E-Commerce Systems

Example:

```text
Order Core

Connected With:

- Web API
- Payment Gateway
- Inventory System
- Database
```

---

### Enterprise Applications

Useful where business rules must remain stable while technologies change frequently.

---

## When to Use

Use Hexagonal Architecture when:

- Business logic is complex.
- Long-term maintainability is important.
- External integrations change frequently.
- Multiple interfaces access the same business logic.
- High testability is required.

---

## When NOT to Use

Avoid it when:

- Building a simple CRUD application.
- The application has minimal business logic.
- The project is a small prototype.
- Additional abstraction is unnecessary.

---

## Comparison

| Feature | Traditional Architecture | Hexagonal Architecture |
|---|---|---|
| Business Logic | Coupled with infrastructure | Independent |
| Testing | Requires dependencies | Easy unit testing |
| Database Change | Difficult | Easier |
| Framework Dependency | High | Low |
| Complexity | Lower | Higher |

---

## Interview Questions

### 1. What is Hexagonal Architecture?

Hexagonal Architecture is a design approach that isolates business logic from external systems using ports and adapters.

---

### 2. Why is it called Ports and Adapters?

Because communication happens through:

- Ports → Interfaces/contracts.
- Adapters → Implementations connecting external systems.

---

### 3. What is the main benefit of Hexagonal Architecture?

The main benefit is keeping business logic independent from infrastructure and external technologies.

---

### 4. How does Hexagonal Architecture improve testing?

Business logic can be tested using mock adapters instead of real databases or external services.

---

### 5. What principle does Hexagonal Architecture follow?

It follows the Dependency Inversion Principle where high-level business rules do not depend on low-level infrastructure details.

---

## Key Takeaways

- Hexagonal Architecture separates business logic from external dependencies.
- The application core contains business rules.
- Ports define communication contracts.
- Adapters connect external systems.
- It improves testability and maintainability.
- It is useful for complex, long-lived applications.
- It may be unnecessary for simple applications.

---

## Previous & Next

← Previous: [Pipe and Filter Architecture](08-Pipe-and-Filter.md)

→ Next: [Clean Architecture](10-Clean-Architecture.md)