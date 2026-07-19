# Monolithic Architecture

## Overview

A Monolithic Architecture is a software architecture where the entire application is built, developed, and deployed as a **single unit**.

All business functionalities—such as user management, authentication, products, orders, payments, notifications, and reporting—are part of the same codebase and are packaged into one deployable application.

Although modern systems often use Microservices, most successful products—including Amazon, Netflix, and Facebook—started as monolithic applications before evolving as their scale and business requirements grew.

---

## Why Do We Need It?

When building a new application, simplicity is often more important than scalability.

Instead of managing multiple services, databases, deployments, and network communication, a monolithic architecture keeps everything in one place.

This allows teams to:

- Develop features quickly
- Deploy a single application
- Debug more easily
- Keep operational complexity low

For startups and small teams, this significantly reduces development time.

---

## Components

A monolithic application typically contains multiple modules within the same application.

Example:

- Authentication
- User Management
- Product Management
- Order Management
- Payment Processing
- Notification Service
- Reporting

Although these modules are logically separated, they are compiled and deployed together.

---

## Architecture

```text
                    Users
                      │
                      ▼
              Load Balancer
                      │
                      ▼
        +---------------------------+
        |      Monolithic App       |
        |---------------------------|
        | Authentication            |
        | Users                     |
        | Products                  |
        | Orders                    |
        | Payments                  |
        | Notifications             |
        +---------------------------+
                      │
                      ▼
                 Database
```

---

## How It Works

1. A client sends a request.
2. The request reaches the monolithic application.
3. The appropriate module processes the request.
4. Business logic is executed.
5. The application interacts with the database.
6. The response is returned to the client.

Since all modules run within the same process, communication between them happens through direct method or function calls instead of network calls.

---

## Example

Consider an e-commerce application.

When a customer places an order:

```text
Place Order

      │

Monolithic Application

      │

Order Module
      │
Payment Module
      │
Inventory Module
      │
Notification Module

      │

Database

      │

Response
```

All modules execute inside the same application.

---

## Advantages

- Simple architecture
- Easy to develop
- Single deployment
- Easy debugging
- Easier testing
- High performance due to in-process communication
- Simpler transactions across modules
- Lower infrastructure cost

---

## Disadvantages

- Large codebase becomes difficult to maintain
- Entire application must be deployed for small changes
- Difficult to scale individual modules
- Technology stack is tightly coupled
- Large teams may face merge conflicts
- A failure in one module can affect the entire application

---

## When to Use

Monolithic Architecture is a good choice when:

- Building an MVP
- Developing a startup product
- Small or medium-sized applications
- Small engineering teams
- Business requirements are evolving rapidly
- Operational simplicity is preferred

Examples:

- Internal business applications
- Admin dashboards
- Learning projects
- Early-stage SaaS products

---

## When NOT to Use

Consider other architectures if:

- Different modules need independent scaling.
- Multiple teams work independently.
- The application has grown into millions of users.
- Different services require different technologies.
- Independent deployments are essential.

---

## Real-World Examples

Many successful companies started with monoliths before migrating to distributed architectures.

Examples include:

- Amazon (early years)
- Netflix (before cloud migration)
- Facebook (early PHP application)
- Shopify
- GitHub
- Basecamp

Starting with a monolith is often a deliberate engineering decision rather than a limitation.

---

## Monolith vs Client-Server

A common misconception is that Monolithic Architecture and Client-Server Architecture are the same.

They describe different aspects of a system.

| Client-Server | Monolithic |
|--------------|------------|
| Communication architecture | Application architecture |
| Defines how clients communicate with servers | Defines how the server application is organized |
| Client and server are separate | Entire backend is one deployable unit |
| Still used by Microservices | One implementation of the server |

A monolithic application commonly follows the Client-Server model.

---

## Evolution

As applications grow, monoliths often evolve into more modular architectures.

```text
Client-Server
       │
       ▼
Monolithic
       │
       ▼
Layered Architecture
       │
       ▼
SOA
       │
       ▼
Microservices
```

Not every application needs to evolve beyond a monolith. Many successful products continue to use monolithic architectures because they best fit their business needs.

---

## Interview Questions

- What is Monolithic Architecture?
- What are the advantages of a Monolith?
- What are its disadvantages?
- Why do startups usually begin with a Monolith?
- Is Monolithic Architecture outdated?
- How is Monolithic Architecture different from Microservices?
- How is Monolithic Architecture different from Client-Server Architecture?

---

## Key Takeaways

- A monolith is a single deployable application containing all business modules.
- It is the simplest architecture to build, test, and deploy.
- Communication between modules is fast because it happens within the same process.
- Monoliths are an excellent choice for startups, MVPs, and small teams.
- Microservices are not a replacement for Monoliths—they are an evolution driven by scale and organizational needs.

---

## Previous

⬅️ 01-Client-Server-Architecture.md

## Next

➡️ 03-Layered-N-Tier-Architecture.md