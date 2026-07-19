# Layered (N-Tier) Architecture

## Overview

Layered Architecture, also known as **N-Tier Architecture**, is one of the most widely used software architecture patterns for organizing application code.

Instead of placing all business logic in a single place, the application is divided into multiple **layers**, where each layer has a specific responsibility.

Each layer communicates only with the layer directly below it, making the application easier to understand, maintain, test, and extend.

Unlike Monolithic Architecture, which describes **how an application is deployed**, Layered Architecture describes **how the application's code is organized**.

---

## Why Do We Need It?

As applications grow, mixing UI logic, business logic, and database code quickly becomes difficult to manage.

For example, imagine a login API where:

- HTTP request handling
- Business validation
- SQL queries
- Response formatting

are all written in one function.

This makes the code difficult to:

- Read
- Test
- Debug
- Reuse
- Maintain

Layered Architecture separates these responsibilities into dedicated layers.

---

## Common Layers

Although applications can have any number of layers, a typical backend consists of:

### Presentation Layer

Responsible for:

- Receiving requests
- Validating input
- Returning responses

Examples:

- Controllers
- Routes
- REST APIs

---

### Business Layer

Responsible for:

- Business rules
- Application logic
- Workflows
- Calculations

Examples:

- Order validation
- Discount calculation
- Inventory verification

---

### Data Access Layer

Responsible for:

- Reading data
- Writing data
- Database communication

Examples:

- Repository
- DAO (Data Access Object)

---

### Database Layer

Stores application data.

Examples:

- MySQL
- PostgreSQL
- MongoDB
- DynamoDB

---

## Architecture

```text
                Client
                  │
                  ▼
        +------------------+
        | Presentation     |
        | (Controller/API) |
        +------------------+
                  │
                  ▼
        +------------------+
        | Business Layer   |
        | (Service)        |
        +------------------+
                  │
                  ▼
        +------------------+
        | Data Layer       |
        | (Repository)     |
        +------------------+
                  │
                  ▼
            +------------+
            | Database   |
            +------------+
```

---

## How It Works

Suppose a user places an order.

1. Client sends a request.
2. Controller receives the request.
3. Controller calls the Service.
4. Service validates business rules.
5. Service calls the Repository.
6. Repository queries the database.
7. Data is returned to the Service.
8. Service prepares the response.
9. Controller returns the response to the client.

Each layer has a single responsibility.

---

## Example

Node.js project structure:

```text
src/

controllers/
    OrderController.js

services/
    OrderService.js

repositories/
    OrderRepository.js

models/
    Order.js

database/
```

Request flow:

```text
POST /orders

      │

OrderController

      │

OrderService

      │

OrderRepository

      │

MySQL

      │

Response
```

---

## Advantages

- Clear separation of responsibilities
- Easier maintenance
- Better code organization
- Improved readability
- Easier testing
- Better code reuse
- Teams can work independently on different layers

---

## Disadvantages

- Additional boilerplate code
- Requests pass through multiple layers
- Can become overly complex for small applications
- Poor layer design may lead to unnecessary dependencies

---

## When to Use

Layered Architecture is a great choice when:

- Building enterprise applications
- Developing REST APIs
- Creating CRUD applications
- Business logic is complex
- Maintainability is important

Examples:

- Banking applications
- E-commerce systems
- Hospital management systems
- ERP software
- CRM platforms

---

## When NOT to Use

Avoid Layered Architecture when:

- Building very small utilities
- Creating simple scripts
- Performance is more important than abstraction
- The application has very limited business logic

---

## Real-World Examples

Most backend frameworks encourage Layered Architecture.

Examples:

- Spring Boot
- ASP.NET Core
- NestJS
- Express.js
- Django
- Laravel

Almost every enterprise backend follows some variation of Layered Architecture.

---

## Layered vs Monolithic

This is one of the most common interview questions.

| Monolithic Architecture | Layered Architecture |
|--------------------------|----------------------|
| Defines deployment style | Defines code organization |
| Single deployable application | Code divided into layers |
| Focuses on packaging | Focuses on responsibilities |
| Can use Layered Architecture | Can exist inside a Monolith or a Microservice |

A monolithic application is often implemented using Layered Architecture.

Likewise, each individual microservice can also follow Layered Architecture internally.

---

## Evolution

As applications become larger, teams often look for better ways to isolate business logic from frameworks.

This leads to architectures such as:

```text
Layered
      │
      ▼
Hexagonal
      │
      ▼
Clean
      │
      ▼
Onion
```

These architectures improve testability and reduce framework dependency while preserving the idea of separating responsibilities.

---

## Interview Questions

- What is Layered Architecture?
- What is N-Tier Architecture?
- What are the common layers?
- Why is Layered Architecture popular?
- Can Microservices use Layered Architecture?
- What is the difference between Layered and Monolithic Architecture?
- What are the disadvantages of Layered Architecture?

---

## Key Takeaways

- Layered Architecture organizes code into separate responsibilities.
- Each layer has a well-defined purpose.
- It improves maintainability, readability, and testability.
- Layered Architecture is independent of deployment style.
- Both Monolithic and Microservices commonly use Layered Architecture internally.

---

## Previous

⬅️ 02-Monolithic-Architecture.md

## Next

➡️ 04-Service-Oriented-Architecture-SOA.md