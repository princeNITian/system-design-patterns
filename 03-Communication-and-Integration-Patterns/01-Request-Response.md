# Request-Response Pattern

## Introduction

The Request-Response Pattern is a communication pattern where one system sends a request to another system and waits for a response before continuing.

It is the most common communication pattern used in distributed systems and forms the foundation of:

- REST APIs
- GraphQL APIs
- gRPC
- Database queries
- Remote Procedure Calls (RPC)

The main goals of the Request-Response pattern are:

- Enable direct communication.
- Provide immediate feedback.
- Keep interactions simple.
- Support synchronous processing.

---

## Why was it Introduced?

Applications often need information or actions from another service.

Example:

- A mobile app requests user details.
- A payment service verifies a transaction.
- An e-commerce application retrieves product information.

Without a standard communication pattern, systems would struggle to exchange data consistently.

Request-Response provides a simple and predictable way for services to communicate.

---

## Architecture Diagram

```text
          Client

             |

     Request (HTTP/gRPC)

             |

             ▼

          Server

             |

      Process Request

             |

             ▼

         Response

             |

             ▼

          Client
```

The client waits until the server returns a response.

---

## How It Works

The communication flow:

```text
1. Client sends a request.

2. Server receives the request.

3. Server processes the request.

4. Server sends a response.

5. Client continues execution.
```

Example:

```text
GET /products/101

        |

        ▼

Product Service

        |

Returns Product Details
```

---

# Common Protocols

## HTTP / REST

Most web applications use HTTP.

Example:

```http
GET /users/10
```

Response:

```json
{
  "id": 10,
  "name": "John"
}
```

---

## GraphQL

Clients request only the required data.

Example:

```graphql
query {
  user(id: 10) {
    name
    email
  }
}
```

---

## gRPC

Uses Protocol Buffers for efficient communication.

Suitable for high-performance microservices.

---

# Core Characteristics

## 1. Synchronous Communication

The client waits until the response arrives.

---

## 2. Direct Interaction

The client communicates directly with the server.

---

## 3. Immediate Result

The client immediately knows whether the request succeeded or failed.

---

## 4. Tight Time Dependency

Both client and server must be available at the same time.

---

## 5. Stateless Communication

Each request is usually independent of previous requests.

---

# Advantages

## 1. Simple to Implement

Easy to understand and widely supported.

---

## 2. Immediate Feedback

Clients receive instant success or failure information.

---

## 3. Easy Debugging

Request and response can be traced easily.

---

## 4. Widely Supported

Supported by almost every programming language and framework.

---

## 5. Standardized

Protocols like HTTP make interoperability straightforward.

---

# Disadvantages

## 1. Blocking Communication

The client waits until processing finishes.

---

## 2. Increased Latency

Slow servers directly impact client response time.

---

## 3. Tight Coupling

Both systems must be available simultaneously.

---

## 4. Limited Scalability

Large numbers of synchronous requests can overwhelm services.

---

## 5. Cascading Failures

If one service becomes unavailable, dependent services may also fail.

---

# Real-World Examples

## E-Commerce

- Product Details API
- Order Details API
- Inventory Lookup

---

## Banking

- Account Balance
- Transaction History
- Payment Verification

---

## Social Media

- User Profile
- Post Details
- Friend List

---

# When to Use

Use the Request-Response pattern when:

- Immediate results are required.
- The operation is short-lived.
- Clients need instant confirmation.
- User-facing APIs are involved.

---

# When NOT to Use

Avoid Request-Response when:

- Processing takes a long time.
- Millions of events must be handled.
- Services should remain loosely coupled.
- Asynchronous communication is preferred.

---

# Comparison

| Feature | Request-Response | Event-Driven |
|---|---|---|
| Communication | Synchronous | Asynchronous |
| Client Waits | Yes | No |
| Coupling | Higher | Lower |
| Immediate Response | Yes | Usually No |
| Scalability | Moderate | High |

---

# Interview Questions

## 1. What is the Request-Response pattern?

A communication pattern where a client sends a request and waits for a response from the server.

---

## 2. Why is it called synchronous?

Because the client blocks until the server finishes processing and returns a response.

---

## 3. What are common protocols used?

- HTTP
- REST
- GraphQL
- gRPC

---

## 4. What are the drawbacks of Request-Response?

- Blocking communication.
- Higher latency.
- Tight coupling.
- Limited scalability.

---

## 5. When should you choose Request-Response over messaging?

When users need an immediate response and the operation completes quickly.

---

# Key Takeaways

- Request-Response is the foundation of modern APIs.
- It enables direct and synchronous communication.
- It is simple, predictable, and widely supported.
- It works best for short-lived operations requiring immediate feedback.
- Large distributed systems often combine Request-Response with asynchronous messaging patterns.

---

## Previous & Next

← Previous: [Scalability Patterns](../02-Scalability-Patterns/README.md)

→ Next: [Publish-Subscribe](02-Publish-Subscribe.md)