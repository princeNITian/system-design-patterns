# RESTful API Design

## Introduction

RESTful API Design is an API design pattern that **models application functionality as resources accessed using standard HTTP methods**.

REST (Representational State Transfer) is the most widely adopted architectural style for building web APIs because it is simple, scalable, stateless, and easy to integrate.

The main goals of RESTful API Design are:

- Provide consistent APIs.
- Simplify client-server communication.
- Improve scalability.
- Follow standard HTTP semantics.

---

## Why was it Introduced?

Before REST, many systems used Remote Procedure Call (RPC) style APIs.

Example:

```text
/createUser

/getUser

/updateUser

/deleteUser
```

As APIs grew, these endpoints became inconsistent and difficult to maintain.

REST organizes APIs around resources.

Example:

```text
/users
/users/101
/orders
/products
```

---

## Architecture Diagram

```text
          Client

             |

             ▼

        HTTP Request

             |

             ▼

        REST API Server

             |

             ▼

         Resource

      /      |      \

   Users   Orders  Products

             |

             ▼

         Database
```

---

## How It Works

The communication flow:

```text
1. Client sends an HTTP request.

2. The request targets a resource.

3. The server processes the request.

4. The server returns an HTTP response.

5. The client receives the resource representation.
```

Example:

```text
GET /users/101

        |

HTTP 200 OK

{
  "id":101,
  "name":"Alice"
}
```

---

# HTTP Methods

## GET

Retrieve resources.

Example:

```text
GET /products
```

---

## POST

Create a new resource.

Example:

```text
POST /orders
```

---

## PUT

Replace an existing resource.

Example:

```text
PUT /users/101
```

---

## PATCH

Partially update a resource.

Example:

```text
PATCH /users/101
```

---

## DELETE

Remove a resource.

Example:

```text
DELETE /products/55
```

---

# Core Characteristics

## 1. Resource-Oriented

Everything is treated as a resource.

Examples:

- Users
- Orders
- Products

---

## 2. Stateless

Each request contains all information required for processing.

---

## 3. Uniform Interface

Uses consistent URLs and HTTP methods.

---

## 4. Standard HTTP Status Codes

Examples:

- 200 OK
- 201 Created
- 400 Bad Request
- 404 Not Found
- 500 Internal Server Error

---

## 5. Client-Server Separation

Clients and servers evolve independently.

---

# REST Resource Naming

Good Examples:

```text
/users

/users/101

/orders

/products
```

Avoid:

```text
/getUsers

/createUser

/deleteOrder
```

Resources should be nouns, not verbs.

---

# Advantages

## 1. Simple and Consistent

Easy for developers to understand.

---

## 2. Scalable

Stateless communication supports horizontal scaling.

---

## 3. Widely Supported

Works with browsers, mobile apps, and backend services.

---

## 4. Cache Friendly

GET requests can be cached to improve performance.

---

## 5. Language Independent

Any client capable of making HTTP requests can consume REST APIs.

---

# Disadvantages

## 1. Over-Fetching

Clients may receive more data than needed.

---

## 2. Under-Fetching

Multiple API calls may be required to gather related data.

---

## 3. Multiple Round Trips

Fetching related resources may require several requests.

---

## 4. Fixed Response Structure

Clients cannot choose exactly which fields to retrieve.

---

## 5. Versioning Challenges

APIs require strategies to evolve without breaking existing clients.

---

# Real-World Examples

## E-Commerce

```text
GET /products

POST /orders

GET /orders/123
```

---

## Banking

```text
GET /accounts

POST /transactions
```

---

## Social Media

```text
GET /posts

POST /comments
```

---

## Food Delivery

```text
GET /restaurants

POST /orders
```

---

# When to Use

Use RESTful API Design when:

- Building web APIs.
- Developing mobile backends.
- Exposing public APIs.
- Building CRUD-based applications.

---

# When NOT to Use

Avoid REST when:

- Clients require highly customized responses.
- Multiple related resources must be fetched frequently.
- Real-time communication is the primary requirement.

---

# Comparison

| Feature | RPC APIs | REST APIs |
|---|---|---|
| Design | Operation-Oriented | Resource-Oriented |
| HTTP Methods | Often POST | Standard HTTP Methods |
| Scalability | Moderate | High |
| Cache Support | Limited | Excellent |
| Standardization | Lower | Higher |

---

# Interview Questions

## 1. What is REST?

REST is an architectural style that exposes resources using standard HTTP methods.

---

## 2. Why are REST APIs stateless?

Each request contains all information needed to process it, allowing servers to scale independently.

---

## 3. Why should resource names be nouns?

Resources represent entities, while HTTP methods define the action being performed.

---

## 4. What are the common HTTP methods?

- GET
- POST
- PUT
- PATCH
- DELETE

---

## 5. What are the limitations of REST?

- Over-fetching.
- Under-fetching.
- Multiple network requests.
- Fixed response structure.

---

# Key Takeaways

- REST organizes APIs around resources.
- Standard HTTP methods define operations.
- Stateless communication improves scalability.
- Consistent naming improves maintainability.
- REST remains the most widely used API design style.

---

## Previous & Next

← Previous Module: [05-Resilience-Patterns](../05-Resilience-Patterns/README.md)

→ Next: [API Versioning](02-API-Versioning.md)