# CQRS (Command Query Responsibility Segregation)

## Introduction

CQRS (Command Query Responsibility Segregation) is a data management pattern that **separates write operations (Commands) from read operations (Queries)**.

Instead of using the same model for both reading and writing data, CQRS uses independent models optimized for each purpose.

The main goals of CQRS are:

- Optimize read and write performance.
- Scale reads and writes independently.
- Simplify complex business logic.
- Support high-performance distributed systems.

---

## Why was it Introduced?

Traditional applications use a single model for both reading and writing.

```text
Application

      |

      ▼

 Database
```

As applications grow:

- Reads become much more frequent than writes.
- Read queries become complex.
- Write operations contain extensive business rules.

Using one model for both creates unnecessary complexity.

CQRS separates these responsibilities.

---

## Architecture Diagram

```text
                Client

            /           \

           ▼             ▼

     Command API     Query API

           |             |

           ▼             ▼

     Write Model    Read Model

           |             |

           ▼             ▼

      Write DB       Read DB
```

The write and read sides are independent.

---

## How It Works

The communication flow:

```text
1. Client sends a command.

2. Command updates the Write Model.

3. Data is stored in the Write Database.

4. Changes are propagated to the Read Model.

5. Client sends queries to the Read Model.

6. Read Database returns optimized results.
```

Example:

```text
Create Order

      |

Write Database

      |

Update Read Model

      |

Customer Dashboard
```

---

# Core Components

## 1. Command

Performs write operations.

Examples:

- Create Order
- Update Payment
- Cancel Booking

---

## 2. Write Model

Handles business logic and data modifications.

---

## 3. Query

Retrieves data without modifying it.

Examples:

- Get Orders
- Search Products
- View Dashboard

---

## 4. Read Model

Optimized for fast data retrieval.

---

## 5. Synchronization

Updates from the Write Model are propagated to the Read Model, often using events.

---

# Core Characteristics

## 1. Separate Read and Write Models

Commands and queries use different models.

---

## 2. Independent Scaling

Read and write workloads can scale independently.

---

## 3. Optimized Data Models

Each model is designed for its specific purpose.

---

## 4. Eventual Consistency

The Read Model may lag behind the Write Model.

---

## 5. Event-Driven Synchronization

Events commonly synchronize the read and write sides.

---

# Advantages

## 1. Better Performance

Read and write operations are independently optimized.

---

## 2. Independent Scalability

Read-heavy systems can scale the Read Model without affecting writes.

---

## 3. Simpler Business Logic

Complex write validation remains isolated from query logic.

---

## 4. Flexible Read Models

Different read models can support different application views.

---

## 5. Improved Maintainability

Read and write concerns are clearly separated.

---

# Disadvantages

## 1. Increased Complexity

Maintaining two models requires additional development effort.

---

## 2. Eventual Consistency

Read data may not immediately reflect recent writes.

---

## 3. Synchronization Overhead

Keeping the Read Model updated introduces additional infrastructure.

---

## 4. Higher Storage Requirements

Separate databases or models may duplicate data.

---

## 5. More Operational Components

Applications often require messaging systems and background processors.

---

# Real-World Examples

## E-Commerce

Write Model:

- Create Order
- Cancel Order

Read Model:

- Order History
- Customer Dashboard
- Sales Reports

---

## Banking

Write:

- Transfer Money
- Deposit Funds

Read:

- Account Balance
- Transaction History

---

## Social Media

Write:

- Create Post
- Like Post

Read:

- News Feed
- User Profile
- Trending Posts

---

# When to Use

Use CQRS when:

- Read traffic greatly exceeds write traffic.
- Read and write workloads have different scalability needs.
- Business logic is complex.
- High-performance queries are required.

---

# When NOT to Use

Avoid CQRS when:

- Applications are small and simple.
- Read and write workloads are balanced.
- Strong immediate consistency is required.
- Additional architectural complexity is not justified.

---

# Comparison

| Feature | Traditional CRUD | CQRS |
|---|---|---|
| Read Model | Same as write | Separate |
| Write Model | Same as read | Separate |
| Scalability | Shared | Independent |
| Complexity | Lower | Higher |
| Consistency | Immediate | Usually Eventual |

---

# Interview Questions

## 1. What is CQRS?

A pattern that separates command (write) operations from query (read) operations using independent models.

---

## 2. Why is CQRS useful?

It allows reads and writes to be optimized and scaled independently.

---

## 3. Does CQRS require two databases?

No.

CQRS separates logical models. These models may use separate databases, separate schemas, or even the same database depending on the implementation.

---

## 4. Why is eventual consistency common in CQRS?

Because the Read Model is usually updated asynchronously after changes are made to the Write Model.

---

## 5. Where is CQRS commonly used?

- E-commerce platforms.
- Banking systems.
- Event-driven architectures.
- High-traffic enterprise applications.

---

# Key Takeaways

- CQRS separates read and write responsibilities.
- Read and write models can be optimized independently.
- The Read Model is often synchronized using events.
- CQRS improves scalability for read-heavy systems.
- It is commonly combined with Event Sourcing in distributed systems.

---

## Previous & Next

← Previous: [Shared Database](02-Shared-Database.md)

→ Next: [Event Sourcing](04-Event-Sourcing.md)