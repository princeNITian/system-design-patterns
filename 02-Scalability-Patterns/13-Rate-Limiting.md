# Rate Limiting

## Introduction

Rate Limiting is a scalability and protection pattern that controls the number of requests a client can send to a system within a specific time period.

It prevents systems from being overwhelmed by:

- Excessive traffic.
- Accidental request spikes.
- Malicious attacks.
- Misbehaving clients.

The main goals of rate limiting are:

- Protect backend services.
- Maintain system availability.
- Ensure fair resource usage.
- Prevent abuse.

---

## Why was it Introduced?

Without rate limiting, any client can send unlimited requests.

Example:

```text
              Client

                |

                ▼

          Application Server

                |

                ▼

             Database
```

A single client can generate:

```text
Client A

100,000 requests/sec
```

Problems:

- Servers become overloaded.
- Database receives excessive traffic.
- Legitimate users experience slow responses.
- System may crash.

Rate limiting controls request flow.

---

## Architecture Diagram

```text
                 Clients

          ┌────────┼────────┐

          ▼        ▼        ▼


              Rate Limiter

                   |

                   ▼

             Application Server

                   |

                   ▼

              Database
```

Requests pass through the rate limiter before reaching backend services.

---

## How It Works

The request flow:

```text
1. Client sends request.

2. Request reaches rate limiter.

3. Rate limiter checks request count.

4. If limit is available:

        Allow request


5. If limit exceeded:

        Reject request
```

Example:

```text
API Limit:

100 requests / minute


Client Request:

Request Count = 101


Result:

HTTP 429 Too Many Requests
```

---

# Rate Limiting Algorithms

## 1. Fixed Window Counter

Requests are counted within fixed time intervals.

Example:

```text
Limit:

100 requests / minute


Window:

10:00 - 10:01

Count = 100
```

Advantages:

- Simple.
- Easy to implement.

Disadvantages:

- Traffic spikes at window boundaries.

Example:

```text
10:00:59

100 requests


10:01:00

100 more requests
```

---

## 2. Sliding Window Log

Stores timestamps of individual requests.

Example:

```text
Request Times:

10:00:10

10:00:20

10:00:45
```

The system checks requests in the latest time window.

Advantages:

- More accurate.

Disadvantages:

- Higher memory usage.

---

## 3. Sliding Window Counter

Combination of fixed window and sliding calculation.

Advantages:

- Better accuracy.
- Lower memory usage.

---

## 4. Token Bucket

A bucket contains tokens.

Each request consumes one token.

Example:

```text
Bucket:

100 Tokens


Request

   |

Consume 1 Token
```

When tokens are exhausted:

```text
Reject Request
```

Advantages:

- Allows short bursts.
- Commonly used.

---

## 5. Leaky Bucket

Requests enter a queue and are processed at a fixed rate.

Example:

```text
Requests

   |

   ▼

Queue

   |

Fixed Processing Rate
```

Advantages:

- Smooth traffic flow.

Disadvantages:

- Does not handle bursts well.

---

# Rate Limiting Scope

## 1. User-Based Rate Limiting

Limits requests per user.

Example:

```text
User ID:

100 requests/minute
```

---

## 2. IP-Based Rate Limiting

Limits requests based on client IP.

Example:

```text
IP:

192.168.1.10

Limit:

1000 requests/hour
```

---

## 3. API-Based Rate Limiting

Different APIs have different limits.

Example:

```text
GET /products

1000 requests/min


POST /orders

100 requests/min
```

---

## 4. Global Rate Limiting

Controls total system traffic.

Example:

```text
Entire API

1 Million requests/minute
```

---

# Core Characteristics

## 1. Request Control

Controls incoming traffic.

---

## 2. Fair Usage

Prevents one user from consuming all resources.

---

## 3. Protection Layer

Acts as a defense against overload.

---

## 4. Distributed Support

Rate limits can be shared across multiple servers.

Example:

```text
Server 1

      \

       Redis

      /

Server 2
```

---

## 5. Configurable Policies

Different users and APIs can have different limits.

---

# Advantages

## 1. Prevents System Overload

Protects backend services from excessive traffic.

---

## 2. Improves Availability

Ensures resources remain available.

---

## 3. Prevents Abuse

Blocks:

- Bots.
- Scrapers.
- Malicious clients.

---

## 4. Fair Resource Distribution

All users get reasonable access.

---

## 5. Controls Infrastructure Cost

Prevents unexpected resource consumption.

---

# Disadvantages

## 1. Legitimate Users May Be Blocked

Incorrect limits can affect real users.

---

## 2. Additional Complexity

Requires managing:

- Rules.
- Storage.
- Distributed counters.

---

## 3. Configuration Challenges

Choosing correct limits is difficult.

---

## 4. Distributed Synchronization

Multiple servers need shared rate limit state.

---

# Rate Limiting vs Throttling

| Feature | Rate Limiting | Throttling |
|---|---|---|
| Purpose | Restrict requests | Slow down requests |
| Action | Reject excess requests | Delay processing |
| Response | Usually HTTP 429 | Slower response |
| Goal | Protection | Traffic control |

---

# Real-World Examples

## Social Media APIs

Limit:

- Posts.
- Likes.
- Comments.

Example:

```text
100 posts/hour
```

---

## Payment Systems

Protect transaction APIs.

Example:

```text
10 payments/minute
```

---

## Cloud APIs

Cloud providers limit API usage.

Example:

```text
1000 API calls/sec
```

---

## Login Systems

Prevent brute-force attacks.

Example:

```text
5 login attempts/minute
```

---

# When to Use

Use rate limiting when:

- APIs are public.
- System handles large traffic.
- Abuse protection is required.
- Expensive operations need protection.
- Fair usage is important.

---

# When NOT to Use

Avoid aggressive rate limiting when:

- Internal systems have controlled traffic.
- Requests are mission critical.
- Limits may negatively impact user experience.

---

# Comparison

| Feature | Without Rate Limiting | With Rate Limiting |
|---|---|---|
| Traffic Control | None | Controlled |
| Abuse Protection | Low | High |
| Availability | Lower | Higher |
| Resource Usage | Unpredictable | Managed |
| Complexity | Low | Higher |

---

# Interview Questions

## 1. What is rate limiting?

Rate limiting controls how many requests a client can send within a specific time period.

---

## 2. Why do we need rate limiting?

To protect systems from overload, abuse, and unfair resource consumption.

---

## 3. What happens when rate limit exceeds?

The system usually returns:

```text
HTTP 429 Too Many Requests
```

---

## 4. Which rate limiting algorithm is commonly used?

Common algorithms:

- Token Bucket.
- Leaky Bucket.
- Sliding Window Counter.

---

## 5. Where should rate limiting be implemented?

Common locations:

- API Gateway.
- Load Balancer.
- Application Layer.
- Dedicated Rate Limiting Service.

---

# Key Takeaways

- Rate limiting controls incoming request traffic.
- It protects systems from overload and abuse.
- Token Bucket is widely used for APIs.
- Distributed rate limiting often uses shared storage like Redis.
- Proper limits balance protection and user experience.
- Rate limiting is essential for scalable public-facing systems.

---

## Previous & Next

← Previous: [Geo Replication](12-Geo-Replication.md)

→ Next Module: [03-Communication-and-Integration-Patterns](../03-Communication-and-Integration-Patterns/README.md)