# Microservices Architecture

## Introduction

Microservices Architecture is an architectural style where an application is divided into a collection of small, independent services. Each service is responsible for a single business capability, owns its own data, and can be developed, deployed, and scaled independently.

Unlike a Monolithic Architecture, where all modules are packaged into a single application, Microservices split the system into multiple services that communicate through APIs or asynchronous messaging.

This architecture is widely adopted by modern cloud-native applications because it enables independent development, scalability, and faster software delivery.

---

## Why was it Introduced?

As applications and engineering teams grew, Monolithic Architectures started facing several challenges:

- Entire application had to be deployed for even a small change.
- Scaling required scaling the entire application.
- Large codebases became difficult to maintain.
- Teams frequently blocked each other's work.
- A failure in one module could affect the entire application.

Microservices were introduced to solve these problems by breaking the application into independently manageable services.

---

## Architecture Diagram

```text
                    Client
                       │
                       ▼
                API Gateway
                       │
      ┌────────────────┼────────────────┐
      ▼                ▼                ▼

 User Service    Product Service    Order Service
      │                │                │
      ▼                ▼                ▼

 User DB        Product DB        Order DB
```

Each service:

- Owns a single business capability.
- Has its own deployment lifecycle.
- Owns its own database.
- Communicates with other services using APIs or events.

---

## How It Works

A client sends a request to the API Gateway.

The API Gateway routes the request to the appropriate Microservice.

If additional information is required, services communicate with one another using synchronous protocols (such as REST or gRPC) or asynchronous messaging (such as Kafka or RabbitMQ).

Each service processes its own business logic and interacts only with its own database.

Because every service is independent, changes to one service generally do not require redeploying the others.

---

## Core Characteristics

- Single Responsibility (one business capability per service)
- Independent deployment
- Independent scaling
- Database per service
- Loose coupling
- High cohesion
- Decentralized data management
- Technology flexibility
- Fault isolation
- Team ownership

---

## Advantages

- Independent deployment of services
- Independent scaling based on workload
- Better fault isolation
- Faster development by multiple teams
- Easier maintenance due to smaller codebases
- Technology flexibility (Polyglot Programming)
- Better resource utilization
- Well suited for cloud-native applications

---

## Disadvantages

- Increased architectural complexity
- Distributed system challenges
- Network latency between services
- More difficult debugging
- Higher infrastructure and operational costs
- Eventual consistency instead of ACID transactions
- More complex testing and monitoring

---

## Real-World Examples

Many large technology companies use Microservices to build scalable platforms.

Examples include:

- Amazon
- Netflix
- Uber
- Spotify
- Airbnb
- WhatsApp
- LinkedIn

Although their implementations differ, they all organize services around business capabilities and deploy them independently.

---

## When to Use

Microservices are a good choice when:

- Multiple teams work on the application.
- Different services require different scaling characteristics.
- Independent deployments are important.
- The application is expected to grow significantly.
- High availability and fault isolation are required.
- Cloud-native infrastructure is available.

---

## When NOT to Use

Microservices may not be the best choice when:

- Building an MVP or prototype.
- The application is small.
- A single team owns the entire system.
- Traffic is relatively low.
- Operational simplicity is more important than scalability.

In these cases, a well-designed Monolithic Architecture is often the better option.

---

## Comparison

| Feature | Monolith | Microservices |
|----------|----------|---------------|
| Codebase | Single | Multiple |
| Deployment | Entire application | Individual services |
| Scaling | Entire application | Individual services |
| Database | Shared | Database per service |
| Fault Isolation | Low | High |
| Team Ownership | Shared | Independent |
| Complexity | Lower | Higher |
| Technology Choice | Usually one stack | Multiple stacks possible |

---

## Interview Questions

### 1. What are Microservices?

Microservices are an architectural style where an application is divided into small, independently deployable services that each focus on a single business capability.

---

### 2. Why were Microservices introduced?

To overcome the limitations of large monolithic applications, including difficult deployments, poor scalability, and tightly coupled teams.

---

### 3. How do Microservices communicate?

They communicate using synchronous protocols such as REST and gRPC or asynchronous messaging through message brokers.

---

### 4. Why does each Microservice usually have its own database?

Database ownership reduces coupling, allows independent schema evolution, and enables each service to choose the most appropriate database.

---

### 5. What are the biggest challenges of Microservices?

Distributed systems complexity, network latency, debugging, observability, data consistency, and operational overhead.

---

### 6. When should you choose Microservices?

When the application has multiple teams, requires independent deployments, independent scaling, and is expected to grow significantly.

---

## Key Takeaways

- Microservices divide an application into independently deployable services.
- Each service focuses on a single business capability.
- Every service typically owns its own database.
- Services communicate using APIs or asynchronous events.
- Microservices improve scalability, deployment flexibility, and fault isolation.
- They also introduce distributed system complexity and operational overhead.
- Microservices are best suited for large, evolving applications with multiple development teams.

---

## Previous & Next

← Previous: [Service-Oriented Architecture (SOA)](05-Service-Oriented-Architecture-SOA.md)

→ Next: [Event-Driven Architecture](06-Event-Driven-Architecture.md)