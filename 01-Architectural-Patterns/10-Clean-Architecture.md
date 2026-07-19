# Clean Architecture

## Introduction

Clean Architecture is an architectural style that focuses on separating business logic from external systems such as databases, frameworks, user interfaces, and external services.

The main principle is:

> Business rules should be independent of external details.

The architecture organizes the application into layers where dependencies always point toward the core business logic.

It was introduced by Robert C. Martin (Uncle Bob) to create systems that are:

- Maintainable
- Testable
- Flexible
- Independent of frameworks and infrastructure

---

## Why was it Introduced?

Traditional applications often mix business logic with external dependencies.

Example:

```text
Controller

   |
   ▼

Business Logic

   |
   ▼

Database

   |
   ▼

Framework
```

This creates problems:

- Business rules become tied to databases.
- Changing frameworks becomes expensive.
- Testing requires external systems.
- Application logic becomes difficult to maintain.

Clean Architecture was introduced to keep the core application independent from technical details.

---

## Architecture Diagram

```text
              External Systems

          UI / Frameworks / Database

                    |
                    ▼

              Interface Adapters

                    |
                    ▼

            Application Business Rules

                    |
                    ▼

              Enterprise Business Rules
```

The inner layers contain the most important business logic.

The outer layers contain implementation details.

---

## How It Works

Clean Architecture follows a dependency rule:

```text
Outer layers

      ↓

Inner layers
```

Dependencies always point inward.

Example:

```text
Database

   ↓

Repository Interface

   ↓

Use Case

   ↓

Business Entity
```

The business entity does not know anything about the database.

---

## Core Characteristics

### 1. Independent Business Rules

Business logic exists independently from:

- Databases.
- Frameworks.
- UI.
- External services.

---

### 2. Dependency Rule

Source code dependencies must only point toward inner layers.

Example:

```text
Database → Use Case → Entity
```

The Entity layer should never depend on the database.

---

### 3. Layer Separation

Clean Architecture commonly contains four layers:

```text
1. Entities

2. Use Cases

3. Interface Adapters

4. Frameworks & Drivers
```

---

## Architecture Layers

### 1. Entities

The innermost layer.

Contains:

- Core business rules.
- Domain objects.
- Enterprise logic.

Example:

```text
User

Order

Payment
```

---

### 2. Use Cases

Contains application-specific business rules.

Responsible for:

- Executing workflows.
- Coordinating entities.
- Implementing application behavior.

Example:

```text
Create Order

Process Payment

Register User
```

---

### 3. Interface Adapters

Converts data between external systems and internal use cases.

Examples:

- Controllers.
- Presenters.
- Gateways.
- Repositories.

---

### 4. Frameworks and Drivers

The outermost layer.

Contains external technologies:

- Databases.
- Web frameworks.
- UI frameworks.
- External APIs.

---

## Advantages

### 1. High Maintainability

Business logic remains clean and isolated.

---

### 2. Easy Testing

Core logic can be tested without external dependencies.

---

### 3. Framework Independence

Frameworks become replaceable implementation details.

Example:

```text
Express.js

can be replaced with

Spring Boot
```

without rewriting business rules.

---

### 4. Database Independence

Business logic does not depend on database technology.

Example:

```text
MySQL

can be replaced with

MongoDB
```

---

### 5. Long-Term Flexibility

The architecture supports continuous evolution.

---

## Disadvantages

### 1. More Code Structure

Requires additional:

- Interfaces.
- Abstractions.
- Layers.

---

### 2. Higher Initial Complexity

Simple applications may feel over-engineered.

---

### 3. Requires Good Design Understanding

Incorrect layer boundaries can reduce the benefits.

---

## Real-World Examples

### Enterprise Applications

Used in systems where business rules are critical:

- Banking platforms.
- Insurance systems.
- Healthcare applications.

---

### E-Commerce Systems

Example:

```text
Order Rules

       |

Payment Rules

       |

Inventory Rules

       |

External Services
```

Business logic remains independent from external integrations.

---

### Large Backend Systems

Useful for applications that evolve over many years with multiple teams.

---

## When to Use

Use Clean Architecture when:

- Business logic is complex.
- The application has a long lifespan.
- Multiple external integrations exist.
- High testability is required.
- Technology changes are expected.

---

## When NOT to Use

Avoid it when:

- Building simple CRUD applications.
- Developing small prototypes.
- Business logic is minimal.
- Additional abstraction provides little value.

---

## Comparison

| Feature | Layered Architecture | Clean Architecture |
|---|---|---|
| Dependency Direction | Often top-down | Always inward |
| Business Logic | May depend on infrastructure | Independent |
| Testing | Moderate | High |
| Framework Dependency | Higher | Lower |
| Complexity | Lower | Higher |

---

## Interview Questions

### 1. What is Clean Architecture?

Clean Architecture is a design approach that separates business logic from external dependencies using layers with inward dependency flow.

---

### 2. What is the Dependency Rule?

Dependencies should always point toward inner layers, meaning business rules should not depend on external details.

---

### 3. What are the four layers of Clean Architecture?

- Entities
- Use Cases
- Interface Adapters
- Frameworks and Drivers

---

### 4. What is the main advantage of Clean Architecture?

It keeps business logic independent, making applications easier to test, maintain, and modify.

---

### 5. How is Clean Architecture different from Layered Architecture?

Layered Architecture separates responsibilities, while Clean Architecture additionally enforces dependency inversion toward business logic.

---

## Key Takeaways

- Clean Architecture protects business logic from external changes.
- Dependencies always point toward the core.
- Entities represent enterprise business rules.
- Use Cases represent application workflows.
- Frameworks and databases remain replaceable details.
- It improves maintainability and testability.
- It is best suited for complex, long-lived applications.

---

## Previous & Next

← Previous: [Hexagonal Architecture](09-Hexagonal-Architecture.md)

→ Next: [Onion Architecture](11-Onion-Architecture.md)