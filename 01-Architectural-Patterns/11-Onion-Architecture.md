# Onion Architecture

## Introduction

Onion Architecture is an architectural style that organizes an application around its **core business logic** and ensures that dependencies flow toward the center of the application.

It was introduced by Jeffrey Palermo in 2008 as an approach to create applications that are:

- Independent of frameworks.
- Independent of databases.
- Easy to test.
- Focused on domain logic.

The central idea is:

> The application core should not depend on external technologies.

---

## Why was it Introduced?

Traditional architectures often place business logic together with infrastructure concerns.

Example:

```text
Controller

    |
    ▼

Service Logic

    |
    ▼

Database

    |
    ▼

Framework
```

Problems:

- Business rules become tightly coupled with databases.
- Testing requires external dependencies.
- Changing infrastructure becomes difficult.
- Domain logic becomes harder to maintain.

Onion Architecture was introduced to keep the domain model at the center and move external dependencies outward.

---

## Architecture Diagram

```text
                 External Layer

        UI / API / Database / Frameworks

                    |

                    ▼

              Infrastructure Layer

        External Services / Persistence

                    |

                    ▼

            Application Services Layer

          Use Cases and Workflows

                    |

                    ▼

                 Domain Layer

          Entities and Business Rules
```

The domain layer is the core of the application.

Dependencies always point inward.

---

## How It Works

The application is divided into concentric layers.

Example:

```text
User Request

      |

      ▼

API Controller

      |

      ▼

Application Service

      |

      ▼

Domain Model

      |

      ▼

Business Rules
```

The inner layers do not know anything about outer layers.

Example:

The Domain layer does not know:

- Which database is used.
- Which API framework is used.
- How data is stored.

---

## Core Characteristics

### 1. Domain-Centric Design

The domain model is the most important part of the application.

It contains:

- Business rules.
- Entities.
- Domain behavior.

---

### 2. Dependency Inversion

Dependencies move toward the center.

Example:

```text
Infrastructure

      ↓

Application

      ↓

Domain
```

The domain does not depend on infrastructure.

---

### 3. Layer Independence

Each layer has a specific responsibility.

---

### 4. Interface-Based Communication

Outer layers communicate with inner layers using abstractions.

Example:

```text
Repository Interface

        |

Database Implementation
```

---

### 5. Separation of Concerns

Business logic and technical details remain separate.

---

## Architecture Layers

### 1. Domain Layer

The innermost layer.

Contains:

- Entities.
- Value objects.
- Business rules.

Example:

```text
Customer

Order

Payment
```

---

### 2. Application Layer

Contains application workflows.

Responsible for:

- Coordinating business operations.
- Executing use cases.

Example:

```text
Create Order

Process Payment
```

---

### 3. Infrastructure Layer

Contains technical implementations.

Examples:

- Database access.
- External APIs.
- Message queues.

---

### 4. Presentation Layer

Handles interaction with users or external systems.

Examples:

- REST APIs.
- Web interfaces.
- Controllers.

---

## Advantages

### 1. Business Logic Independence

Core business rules remain isolated from technical changes.

---

### 2. Easy Testing

Domain logic can be tested without databases or external systems.

---

### 3. Flexible Technology Choices

Infrastructure can change without affecting business logic.

Example:

```text
PostgreSQL

can be replaced with

MongoDB
```

---

### 4. Better Maintainability

Clear boundaries make large applications easier to evolve.

---

### 5. Supports Domain-Driven Design

Works well with DDD principles.

---

## Disadvantages

### 1. Additional Complexity

Requires more layers and abstractions.

---

### 2. More Initial Development Effort

Creating interfaces and boundaries takes additional time.

---

### 3. Overengineering Risk

Small applications may not benefit from this structure.

---

### 4. Requires Strong Design Understanding

Incorrect boundaries can reduce effectiveness.

---

## Real-World Examples

### Enterprise Applications

Common in:

- Banking systems.
- Insurance platforms.
- Healthcare systems.

---

### E-Commerce Systems

Example:

```text
Domain:

Order Rules

Application:

Checkout Workflow

Infrastructure:

Payment Gateway

Presentation:

REST API
```

---

### Large Business Applications

Useful where business rules change frequently but infrastructure evolves independently.

---

## When to Use

Use Onion Architecture when:

- Domain logic is complex.
- Business rules are critical.
- Applications have a long lifespan.
- Multiple infrastructure changes are expected.
- High testability is required.

---

## When NOT to Use

Avoid it when:

- Building simple CRUD applications.
- Developing small applications.
- Business logic is minimal.
- Additional abstraction is unnecessary.

---

## Comparison

| Feature | Clean Architecture | Onion Architecture |
|---|---|---|
| Main Focus | Separation of concerns | Domain-centric design |
| Core | Entities and use cases | Domain model |
| Dependency Rule | Inward | Inward |
| Framework Independence | Yes | Yes |
| Complexity | Higher | Moderate to High |

---

## Interview Questions

### 1. What is Onion Architecture?

Onion Architecture is a design pattern where the application is organized around the domain model with dependencies pointing inward.

---

### 2. What is the core principle of Onion Architecture?

The domain layer should be independent of external systems and contain the most important business logic.

---

### 3. What are the layers of Onion Architecture?

Common layers include:

- Domain Layer
- Application Layer
- Infrastructure Layer
- Presentation Layer

---

### 4. How does Onion Architecture improve testing?

The domain logic can be tested independently without requiring databases or external services.

---

### 5. How is Onion Architecture different from traditional layered architecture?

Traditional layered architecture often allows business logic to depend on infrastructure, while Onion Architecture prevents this by enforcing inward dependencies.

---

## Key Takeaways

- Onion Architecture puts domain logic at the center.
- External dependencies are moved to outer layers.
- Dependencies always point inward.
- Business rules remain independent of infrastructure.
- It improves maintainability and testability.
- It is useful for complex domain-driven applications.

---

## Previous & Next

← Previous: [Clean Architecture](10-Clean-Architecture.md)

→ Next: [Space-Based Architecture](12-Space-Based-Architecture.md)