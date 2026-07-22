# GraphQL

## Introduction

GraphQL is an API design pattern that **allows clients to request exactly the data they need through a single endpoint**.

Unlike traditional REST APIs, where the server determines the response structure, GraphQL enables clients to specify the fields they want in each request.

The main goals of GraphQL are:

- Eliminate over-fetching and under-fetching.
- Reduce network requests.
- Provide flexible data retrieval.
- Improve client performance.

---

## Why was it Introduced?

Consider a REST API for an e-commerce application.

To display an order page, a client may need data from multiple endpoints.

```text
GET /users/101

GET /orders/500

GET /products/20
```

This results in multiple network requests.

GraphQL allows the client to retrieve all required data with a single request.

---

## Architecture Diagram

```text
              Client

                 |

                 ▼

        GraphQL Endpoint

           /        \

          ▼          ▼

 GraphQL Resolver  GraphQL Resolver

          \          /

           ▼        ▼

        Backend Services

      /      |      |      \

     ▼       ▼      ▼       ▼

 User   Order  Product  Payment
Service Service Service  Service
```

A single GraphQL endpoint coordinates requests across multiple backend services.

---

## How It Works

The communication flow:

```text
1. Client sends a GraphQL query.

2. GraphQL parses the query.

3. Resolvers fetch the required data.

4. Data from multiple services is combined.

5. The requested fields are returned to the client.
```

Example query:

```graphql
query {
  user(id: 101) {
    name
    orders {
      id
      total
    }
  }
}
```

Only the requested fields are returned.

---

# Core Components

## 1. Schema

Defines the available types, queries, and mutations.

---

## 2. Query

Retrieves data.

Example:

```graphql
query {
  products {
    id
    name
  }
}
```

---

## 3. Mutation

Creates, updates, or deletes data.

Example:

```graphql
mutation {
  createOrder(...)
}
```

---

## 4. Resolver

Fetches data for each field in a query.

---

## 5. Single Endpoint

GraphQL typically exposes one endpoint.

Example:

```text
/graphql
```

---

# Core Characteristics

## 1. Client-Driven Queries

Clients request only the fields they need.

---

## 2. Single Endpoint

All operations use a single API endpoint.

---

## 3. Strongly Typed Schema

Every query is validated against a predefined schema.

---

## 4. Flexible Responses

Different clients can request different response structures.

---

## 5. Data Aggregation

A single query can retrieve data from multiple backend services.

---

# Advantages

## 1. Eliminates Over-Fetching

Only requested fields are returned.

---

## 2. Eliminates Under-Fetching

Related data can be retrieved in one request.

---

## 3. Fewer Network Requests

Multiple REST calls are replaced by a single GraphQL query.

---

## 4. Better Client Flexibility

Each client controls its own response structure.

---

## 5. Strong Type Safety

The schema provides validation and documentation.

---

# Disadvantages

## 1. Increased Complexity

GraphQL servers are more complex than basic REST APIs.

---

## 2. Query Optimization Challenges

Poorly designed queries can become expensive to execute.

---

## 3. Caching Complexity

HTTP caching is less straightforward than with REST.

---

## 4. Learning Curve

Developers must understand schemas, resolvers, and query language.

---

## 5. Security Considerations

Complex queries may require depth limits, complexity analysis, and rate limiting.

---

# Real-World Examples

## GitHub

Provides a GraphQL API for flexible repository and user queries.

---

## Shopify

Uses GraphQL extensively for storefront and administrative APIs.

---

## E-Commerce

Retrieve products, inventory, and reviews in a single query.

---

## Social Media

Fetch users, posts, comments, and reactions together.

---

# When to Use

Use GraphQL when:

- Multiple clients require different data.
- APIs aggregate data from multiple services.
- Over-fetching and under-fetching are common.
- Client flexibility is a priority.

---

# When NOT to Use

Avoid GraphQL when:

- APIs are simple CRUD services.
- HTTP caching is a primary requirement.
- Teams prefer straightforward REST endpoints.
- The added flexibility is unnecessary.

---

# Comparison

| Feature | REST | GraphQL |
|---|---|---|
| Endpoints | Multiple | Single |
| Response Structure | Server Defined | Client Defined |
| Over-Fetching | Possible | Eliminated |
| Under-Fetching | Possible | Eliminated |
| Caching | Simpler | More Complex |

---

# Interview Questions

## 1. What is GraphQL?

A query language and API pattern that allows clients to request exactly the data they need.

---

## 2. How is GraphQL different from REST?

REST exposes multiple resource-based endpoints, while GraphQL typically exposes a single endpoint with client-defined queries.

---

## 3. What is a GraphQL Resolver?

A function responsible for fetching the data for a specific field in a GraphQL query.

---

## 4. What are the main advantages of GraphQL?

- Eliminates over-fetching.
- Eliminates under-fetching.
- Reduces network requests.
- Provides flexible queries.

---

## 5. What are the disadvantages of GraphQL?

- Increased implementation complexity.
- More difficult caching.
- Query optimization and security challenges.

---

# Key Takeaways

- GraphQL allows clients to request exactly the data they need.
- A single endpoint serves all queries and mutations.
- It reduces unnecessary network requests.
- GraphQL is well suited for applications with diverse client requirements.
- It complements REST and is widely adopted in modern API ecosystems.

---

## Previous & Next

← Previous: [Backend for Frontend (BFF)](08-Backend-for-Frontend-BFF.md)

→ Next Module: [07-Deployment-Patterns](../07-Deployment-Patterns/README.md)