# Shared Database

## Introduction

The Shared Database Pattern is a data management pattern where **multiple services or applications access the same database**.

Instead of each service owning its own data store, all services read from and write to a common database.

The main goals of the Shared Database pattern are:

- Simplify data sharing.
- Maintain strong consistency.
- Reduce operational overhead.
- Support centralized data management.

---

## Why was it Introduced?

In many traditional applications, multiple modules need access to the same data.

Instead of maintaining separate databases, all modules share one database.

```text
Order Service

       |

Payment Service

       |

Inventory Service

       |

       ▼

 Shared Database
```

This simplifies data access but increases coupling between services.

---

## Architecture Diagram

```text
          Client

             |

             ▼

     API Gateway

             |

   ---------------------

   |         |         |

   ▼         ▼         ▼

 Order    Payment   Inventory

 Service   Service    Service

      \       |       /

       \      |      /

            ▼

     Shared Database
```

All services access the same database.

---

## How It Works

The communication flow:

```text
1. Client sends a request.

2. Request reaches the appropriate service.

3. Service reads or updates the shared database.

4. Other services access the same database when needed.
```

Example:

```text
Order Service

      |

Insert Order

      |

Shared Database

      |

Inventory Service Reads Order
```

Multiple services directly access the same data.

---

# Core Characteristics

## 1. Single Database

All services use one shared database.

---

## 2. Centralized Data

Business data is stored in one location.

---

## 3. Direct Database Access

Services communicate by reading and writing the same database.

---

## 4. Strong Consistency

Changes are immediately visible to all services.

---

## 5. Simplified Reporting

Reporting across services is easier because all data resides in one database.

---

# Advantages

## 1. Simpler Architecture

Only one database needs to be managed.

---

## 2. Strong Consistency

Services always see the latest committed data.

---

## 3. Easy Data Sharing

No APIs or events are required for sharing data.

---

## 4. Easier Reporting

Cross-service queries can be executed directly.

---

## 5. Lower Operational Overhead

Managing one database is simpler than managing many.

---

# Disadvantages

## 1. Tight Coupling

Schema changes may impact multiple services.

---

## 2. Limited Scalability

The database becomes a shared bottleneck.

---

## 3. Difficult Independent Deployment

Database changes require coordination across teams.

---

## 4. Technology Lock-In

All services must use the same database technology.

---

## 5. Fault Propagation

Database failures affect every service.

---

# Real-World Examples

## Monolithic Applications

All application modules share one relational database.

---

## Enterprise Applications

Departments such as:

- Sales
- Inventory
- Finance

may use a common enterprise database.

---

## Legacy Systems

Older service-oriented applications often rely on a shared database.

---

# When to Use

Use the Shared Database pattern when:

- Building a monolithic application.
- Strong consistency is required.
- Applications are relatively small.
- Operational simplicity is preferred.

---

# When NOT to Use

Avoid the Shared Database pattern when:

- Building independently deployable microservices.
- Teams need service autonomy.
- Independent scaling is required.
- Different services require different database technologies.

---

# Comparison

| Feature | Shared Database | Database per Service |
|---|---|---|
| Database Ownership | Shared | One per service |
| Coupling | High | Low |
| Consistency | Strong | Eventual (across services) |
| Scalability | Limited | High |
| Technology Choice | Single database | Polyglot persistence |

---

# Interview Questions

## 1. What is the Shared Database pattern?

A pattern where multiple services access the same database.

---

## 2. What is the biggest disadvantage of a Shared Database?

Tight coupling between services due to shared schemas and direct database access.

---

## 3. Why is this pattern common in monolithic applications?

Because all modules are deployed together and naturally share the same data store.

---

## 4. Can microservices use a Shared Database?

They can, but it is generally discouraged because it reduces service independence and scalability.

---

## 5. When is a Shared Database a good choice?

For small applications, monoliths, or systems where strong consistency and simplicity are more important than independent service evolution.

---

# Key Takeaways

- Multiple services share a single database.
- It provides strong consistency and simple data sharing.
- It increases coupling between services.
- Independent deployments become more difficult.
- It is well suited for monolithic and many legacy applications but is generally avoided in modern microservice architectures.

---

## Previous & Next

← Previous: [Database per Service](01-Database-per-Service.md)

→ Next: [CQRS](03-CQRS.md)