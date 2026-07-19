# Architectural Patterns

Architectural Patterns define the **high-level structure** of a software system. They describe **how different components are organized, how they interact, and how responsibilities are distributed** across the application.

Choosing the right architecture is one of the most important decisions in software design because it directly impacts scalability, maintainability, performance, deployment, and future growth.

This module covers the evolution of software architectures—from simple client-server applications to modern cloud-native and distributed architectures.

---

# Why Learn Architectural Patterns?

Understanding architectural patterns helps you answer questions such as:

- How should I structure my application?
- Should I build a Monolith or Microservices?
- When should I choose Event-Driven Architecture?
- Is Serverless suitable for my use case?
- How can I make my application easier to maintain and test?
- Which architecture is used by companies like Amazon, Netflix, and Uber?

Architectural patterns provide the foundation upon which all other system design concepts are built.

---

# Learning Objectives

After completing this module, you will be able to:

- Understand the evolution of software architecture.
- Identify the strengths and weaknesses of each architectural pattern.
- Choose an appropriate architecture based on business and technical requirements.
- Explain architectural trade-offs during system design interviews.
- Recognize where each pattern is commonly used in the industry.

---

# Learning Order

Follow the topics in the order below:

| # | Pattern | Focus |
|---|---------|-------|
| 01 | Client-Server Architecture | Foundation of distributed applications |
| 02 | Monolithic Architecture | Single deployable application |
| 03 | Layered (N-Tier) Architecture | Separation of responsibilities |
| 04 | Service-Oriented Architecture (SOA) | Enterprise service integration |
| 05 | Microservices | Independently deployable services |
| 06 | Event-Driven Architecture | Asynchronous communication using events |
| 07 | Serverless Architecture | Managed infrastructure and Functions-as-a-Service |
| 08 | Pipe and Filter | Data processing through independent stages |
| 09 | Hexagonal Architecture | Decoupling business logic from external systems |
| 10 | Clean Architecture | Dependency inversion and maintainability |
| 11 | Onion Architecture | Domain-centric application design |
| 12 | Space-Based Architecture | Eliminating database bottlenecks for extreme scalability |
| 13 | Peer-to-Peer (P2P) Architecture | Decentralized communication between nodes |

---

# Evolution of Software Architecture

```text
Client-Server
       │
       ▼
Monolithic
       │
       ▼
Layered (N-Tier)
       │
       ▼
Service-Oriented Architecture (SOA)
       │
       ▼
Microservices
       │
       ▼
Event-Driven
       │
       ▼
Serverless
```

> Modern systems often combine multiple architectural patterns rather than relying on a single one.

---

# Prerequisites

No prior knowledge is required.

However, having a basic understanding of the following topics is helpful:

- HTTP
- APIs
- Databases
- Basic Networking
- Software Development Fundamentals

---

# After Completing This Module

You will understand:

- How software architectures evolved over time.
- Why different architectural patterns exist.
- The trade-offs between architectural approaches.
- Which architecture fits different business scenarios.
- How architectural choices impact scalability, maintainability, and deployment.

You'll also be well prepared to move on to the next module:

➡️ **Scalability Patterns**, where you'll learn how to scale these architectures to handle millions of users.

---

# Next Module

📁 **02-Scalability-Patterns**

Learn how modern systems achieve high performance using:

- Load Balancing
- Auto Scaling
- Caching
- CDN
- Replication
- Sharding
- Rate Limiting
- Consistent Hashing
- Geo Replication

---

# Related Modules

- **02-Scalability-Patterns**
- **03-Communication-and-Integration-Patterns**
- **04-Data-Management-Patterns**
- **05-Resilience-Patterns**

These modules build directly upon the architectural concepts introduced here.

---

# Summary

Architectural Patterns are the **foundation of System Design**. Before deciding how to scale a system, communicate between services, manage data, or handle failures, you must first decide **how the system itself will be structured**.

Mastering these patterns will help you make informed architectural decisions and provide strong reasoning during real-world software design and system design interviews.