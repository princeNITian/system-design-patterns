# Rate Limiting

## Introduction

Rate Limiting is an API design pattern that **controls the number of requests a client can make within a specified time period**.

It protects APIs from abuse, prevents resource exhaustion, and ensures fair usage among clients.

The main goals of Rate Limiting are:

- Protect backend services.
- Prevent abuse and denial-of-service attacks.
- Ensure fair resource allocation.
- Improve system stability.

---

## Why was it Introduced?

Consider a public API.

```text
          API

           ▲

     Millions of Requests

           ▲

      Single Client
```

Without restrictions, a single client could overwhelm the server, causing slower responses or outages for everyone.

Rate Limiting ensures each client can only make a limited number of requests within a defined time window.

---

## Architecture Diagram

```text
             Client

                |

                ▼

          API Gateway

                |

        Rate Limiter Check

          /            \

         ▼              ▼

  Within Limit     Limit Exceeded

         |              |

         ▼              ▼

     Process      HTTP 429

                  Too Many Requests
```

---

## How It Works

The communication flow:

```text
1. Client sends a request.

2. Rate limiter identifies the client.

3. Request count is checked.

4. If within the allowed limit:
      Process the request.

5. If the limit is exceeded:
      Reject the request with HTTP 429.
```

Example:

```text
Limit:

100 requests/minute

Client:

101st Request

↓

HTTP 429 Too Many Requests
```

---

# Common Rate Limiting Algorithms

## 1. Fixed Window Counter

Counts requests within a fixed time window.

Example:

```text
100 requests

Every Minute
```

Simple but can allow traffic spikes at window boundaries.

---

## 2. Sliding Window Log

Stores timestamps for each request and counts only requests within the current window.

Provides more accurate limiting but requires additional memory.

---

## 3. Sliding Window Counter

Combines the current and previous windows to smooth request limits.

Balances accuracy and efficiency.

---

## 4. Token Bucket

Tokens are added to a bucket at a constant rate.

Each request consumes one token.

If no tokens remain, requests are rejected.

Allows short bursts while maintaining an average request rate.

---

## 5. Leaky Bucket

Requests enter a queue and leave at a constant rate.

Smooths burst traffic by processing requests steadily.

---

# Core Characteristics

## 1. Request Control

Limits the number of requests over time.

---

## 2. Fair Usage

Prevents one client from monopolizing resources.

---

## 3. Client Identification

Limits can be applied using:

- API Key
- User ID
- IP Address
- Access Token

---

## 4. Configurable Policies

Different clients or plans can have different limits.

---

## 5. Automatic Enforcement

Limits are applied without manual intervention.

---

# Advantages

## 1. Prevents Abuse

Protects APIs from excessive requests.

---

## 2. Improves Stability

Reduces resource exhaustion during traffic spikes.

---

## 3. Fair Resource Allocation

Ensures all clients receive reasonable access.

---

## 4. Supports Multi-Tenant Systems

Different usage limits can be assigned to different customers.

---

## 5. Enhances Security

Helps mitigate brute-force attacks and certain denial-of-service scenarios.

---

# Disadvantages

## 1. Additional Infrastructure

Rate limiting requires counters, storage, or distributed coordination.

---

## 2. Configuration Complexity

Selecting appropriate limits requires careful planning.

---

## 3. Potential False Positives

Legitimate users may occasionally exceed configured limits.

---

## 4. Distributed Synchronization

Maintaining accurate counters across multiple servers can be challenging.

---

## 5. User Friction

Clients must handle `HTTP 429 Too Many Requests` responses appropriately.

---

# Real-World Examples

## Public APIs

Limit requests per API key to prevent abuse.

---

## Login APIs

Restrict repeated login attempts to reduce brute-force attacks.

---

## Payment APIs

Control transaction request rates for stability.

---

## AI APIs

Limit requests or tokens per user based on subscription plans.

---

# When to Use

Use Rate Limiting when:

- Exposing public APIs.
- Preventing abuse.
- Protecting backend resources.
- Supporting multiple customers with different usage plans.

---

# When NOT to Use

Avoid strict Rate Limiting when:

- APIs are used only internally in controlled environments.
- Very low traffic makes request limiting unnecessary.
- Other forms of traffic control already satisfy the requirements.

---

# Comparison

| Feature | Without Rate Limiting | With Rate Limiting |
|---|---|---|
| Abuse Protection | Low | High |
| Resource Control | Limited | Strong |
| Fair Usage | No | Yes |
| System Stability | Lower | Higher |
| Implementation Complexity | Lower | Higher |

---

# Interview Questions

## 1. What is Rate Limiting?

A technique that restricts the number of requests a client can make within a given time period.

---

## 2. Why is Rate Limiting important?

It protects APIs from abuse, ensures fair usage, and improves system stability.

---

## 3. What HTTP status code is returned when the limit is exceeded?

**HTTP 429 – Too Many Requests**

---

## 4. What are the common Rate Limiting algorithms?

- Fixed Window Counter
- Sliding Window Log
- Sliding Window Counter
- Token Bucket
- Leaky Bucket

---

## 5. Which algorithm is commonly preferred for production systems?

Token Bucket is widely used because it supports burst traffic while maintaining a controlled average request rate.

---

# Key Takeaways

- Rate Limiting controls request frequency.
- It protects APIs from abuse and resource exhaustion.
- Multiple algorithms exist with different trade-offs.
- HTTP 429 indicates that a client has exceeded its limit.
- Rate Limiting is a fundamental component of modern API security and scalability.

---

## Previous & Next

← Previous: [Idempotency](05-Idempotency.md)

→ Next: [API Gateway](07-API-Gateway.md)