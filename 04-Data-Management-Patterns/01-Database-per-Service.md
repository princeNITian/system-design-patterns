# Database per Service

## Introduction

The Database per Service Pattern is a data management pattern where **each microservice owns and manages its own database**.

No other service is allowed to directly access that database. Services communicate with each other through APIs or events instead of sharing data stores.

The main goals of the Database per Service pattern are:

- Ensure data ownership.
- Reduce coupling between services.
- Enable independent deployments.
- Allow each service to choose the most suitable database.

---

## Why was it Introduced?

In a monolithic application, all modules usually share one database.

```text
Application

      |

      ▼

 Shared Database
```

As applications evolve into microservices, a shared database introduces problems:

- Tight coupling.
- Schema conflicts.
- Difficult deployments.
- Limited scalability.

Giving each service its own database solves these issues.

---

## Architecture Diagram

```text
            Client

               |

               ▼

        API Gateway

               |

     -----------------------

     |         |          |

     ▼         ▼          ▼

 Order     Payment   Inventory

 Service    Service    Service

     |         |          |

     ▼         ▼          ▼

 Order DB  Payment DB Inventory DB
```

Each service owns its database.

---

## How It Works

The communication flow:

```text
1. Client sends a request.

2. Request reaches the appropriate service.

3. Service updates only its own database.

4. Other services access data through APIs or events.

5. No service directly queries another service's database.
```

Example:

```text
Order Service

      |

Order Database

      |

Publish Order Created Event

      |

Inventory Service Updates Inventory
```

---

# Core Characteristics

## 1. Independent Database

Every service owns its own data store.

---

## 2. Data Ownership

Only the owning service can modify its database.

---

## 3. Loose Coupling

Services communicate through APIs or events.

---

## 4. Polyglot Persistence

Different services may use different database technologies.

---

## 5. Independent Scaling

Each database can scale according to its workload.

---

# Advantages

## 1. Loose Coupling

Database changes do not affect other services.

---

## 2. Independent Deployment

Services can be deployed without coordinating database changes across teams.

---

## 3. Better Scalability

Each database can be scaled independently.

---

## 4. Technology Flexibility

Each service can choose the most appropriate database.

Examples:

- PostgreSQL
- MySQL
- MongoDB
- DynamoDB

---

## 5. Improved Fault Isolation

Database failures affect only the owning service.

---

# Disadvantages

## 1. Data Duplication

Some data may exist in multiple services.

---

## 2. Distributed Transactions

Transactions across services require patterns like Saga.

---

## 3. Increased Operational Complexity

Managing multiple databases is more challenging.

---

## 4. Data Consistency Challenges

Keeping related data synchronized requires messaging or APIs.

---

## 5. Reporting Complexity

Generating reports across multiple databases is more difficult.

---

# Real-World Examples

## E-Commerce

- Order Service → Order Database
- Payment Service → Payment Database
- Inventory Service → Inventory Database
- User Service → User Database

---

## Banking

Separate databases for:

- Accounts
- Payments
- Loans
- Customer Profiles

---

## Ride Sharing

Separate databases for:

- Riders
- Drivers
- Trips
- Payments

---

# When to Use

Use the Database per Service pattern when:

- Building microservices.
- Services require independent deployments.
- Different services have different data requirements.
- Teams own individual services.

---

# When NOT to Use

Avoid the Database per Service pattern when:

- Building a small monolithic application.
- Cross-service transactions are frequent and complex.
- Operational simplicity is more important than service independence.

---

# Comparison

| Feature | Shared Database | Database per Service |
|---|---|---|
| Database Ownership | Shared | One per service |
| Coupling | High | Low |
| Independent Deployment | Difficult | Easy |
| Scalability | Limited | High |
| Technology Choice | Single database | Polyglot persistence |

---

# Interview Questions

## 1. What is the Database per Service pattern?

A pattern where each microservice owns and manages its own database.

---

## 2. Why should services avoid accessing another service's database?

To maintain service autonomy, loose coupling, and clear data ownership.

---

## 3. Can different services use different databases?

Yes. This is known as **Polyglot Persistence**.

---

## 4. How do services share data?

Through APIs, events, or messaging—not by directly accessing another service's database.

---

## 5. What challenge does this pattern introduce?

Distributed transactions, which are commonly handled using Saga patterns.

---

# Key Takeaways

- Each microservice owns its own database.
- Services communicate through APIs or events.
- The pattern improves scalability and service independence.
- Polyglot persistence allows technology flexibility.
- It is the preferred database pattern for modern microservice architectures.

---

## Previous & Next

← Previous Module: [03-Communication-and-Integration-Patterns](../03-Communication-and-Integration-Patterns/README.md)

→ Next: [Shared Database](02-Shared-Database.md)