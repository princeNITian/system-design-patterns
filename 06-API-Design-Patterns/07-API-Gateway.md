# API Gateway

## Introduction

The API Gateway pattern is an API design pattern that **provides a single entry point for clients to access multiple backend services**.

Instead of clients communicating directly with individual services, all requests pass through the API Gateway, which handles routing, authentication, rate limiting, request transformation, and other cross-cutting concerns.

The main goals of the API Gateway pattern are:

- Simplify client communication.
- Centralize common functionality.
- Improve security.
- Reduce client complexity.

---

## Why was it Introduced?

In a microservices architecture, a client may need to communicate with multiple services.

```text
Client

 | \
 |  \
 ▼   ▼
User Service

      ▼
Order Service

      ▼
Payment Service

      ▼
Inventory Service
```

Problems:

- Multiple network calls.
- Complex client logic.
- Duplicate authentication.
- Difficult API management.

The API Gateway provides a single entry point.

---

## Architecture Diagram

```text
              Client

                 |

                 ▼

           API Gateway

      /       |       \

     ▼        ▼        ▼

 User      Order    Payment
Service    Service   Service

                 |

                 ▼

          Other Services
```

Clients communicate only with the gateway.

---

## How It Works

The communication flow:

```text
1. Client sends a request.

2. API Gateway authenticates the request.

3. Gateway applies policies.

4. Gateway routes the request.

5. Backend service processes the request.

6. Gateway returns the response to the client.
```

Example:

```text
Client

     |

GET /orders/123

     |

API Gateway

     |

Order Service

     |

Response
```

---

# Core Responsibilities

## 1. Request Routing

Routes requests to the appropriate backend service.

---

## 2. Authentication & Authorization

Validates users before forwarding requests.

---

## 3. Rate Limiting

Protects backend services from excessive traffic.

---

## 4. Load Balancing

Distributes requests across multiple service instances.

---

## 5. Request & Response Transformation

Modifies requests or responses when necessary.

---

## 6. API Aggregation

Combines responses from multiple services into a single response.

---

## 7. Logging & Monitoring

Captures metrics, logs, and request traces.

---

# Core Characteristics

## 1. Single Entry Point

Clients interact with one endpoint instead of many services.

---

## 2. Centralized Cross-Cutting Concerns

Common functionality is implemented once.

---

## 3. Backend Abstraction

Internal service structure is hidden from clients.

---

## 4. Improved Security

Backend services are not directly exposed.

---

## 5. Client Simplification

Clients require fewer network calls and less routing logic.

---

# Advantages

## 1. Simplified Client Development

Clients communicate with a single endpoint.

---

## 2. Improved Security

Authentication and authorization are centralized.

---

## 3. Reduced Network Calls

Aggregation minimizes round trips.

---

## 4. Easier Monitoring

Traffic flows through a single control point.

---

## 5. Better Scalability

Gateway policies can be managed independently from backend services.

---

# Disadvantages

## 1. Additional Hop

Every request passes through the gateway, adding some latency.

---

## 2. Potential Bottleneck

A poorly scaled gateway can become a performance bottleneck.

---

## 3. Increased Complexity

Gateway configuration grows as the system evolves.

---

## 4. Single Point of Failure

If not deployed redundantly, gateway failures can affect all services.

---

## 5. Operational Overhead

Monitoring, scaling, and maintaining the gateway require additional effort.

---

# Real-World Examples

## Amazon API Gateway

Provides authentication, throttling, routing, and monitoring for backend services.

---

## Kong Gateway

Manages APIs with plugins for security, logging, and traffic control.

---

## NGINX

Acts as a reverse proxy and API Gateway for many web applications.

---

## Netflix

Uses API gateways to expose microservices to various client applications.

---

# When to Use

Use the API Gateway pattern when:

- Building microservices.
- Multiple backend services exist.
- Authentication should be centralized.
- Clients require a single entry point.

---

# When NOT to Use

Avoid the API Gateway pattern when:

- Building a simple monolithic application.
- Only one backend service exists.
- Gateway functionality provides little value.

---

# Comparison

| Feature | Direct Service Access | API Gateway |
|---|---|---|
| Client Complexity | Higher | Lower |
| Authentication | Distributed | Centralized |
| Routing | Client Managed | Gateway Managed |
| API Aggregation | No | Yes |
| Operational Complexity | Lower | Higher |

---

# Interview Questions

## 1. What is an API Gateway?

A single entry point that routes client requests to backend services while handling common concerns such as authentication and rate limiting.

---

## 2. Why is an API Gateway important in microservices?

It hides internal services, simplifies clients, and centralizes cross-cutting functionality.

---

## 3. What responsibilities are commonly handled by an API Gateway?

- Routing.
- Authentication.
- Authorization.
- Rate Limiting.
- Load Balancing.
- Request Transformation.
- API Aggregation.

---

## 4. Can an API Gateway become a bottleneck?

Yes.

If it is not scaled properly, it can become a performance bottleneck or single point of failure.

---

## 5. What are some popular API Gateway solutions?

- Amazon API Gateway
- Kong
- NGINX
- Apigee
- Azure API Management

---

# Key Takeaways

- API Gateway provides a single entry point for backend services.
- It centralizes authentication, routing, and other common concerns.
- It simplifies clients and improves security.
- API aggregation reduces client network calls.
- It is a core building block of modern microservices architectures.

---

## Previous & Next

← Previous: [Rate Limiting](06-Rate-Limiting.md)

→ Next: [Backend for Frontend (BFF)](08-Backend-for-Frontend-BFF.md)