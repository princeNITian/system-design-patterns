# Circuit Breaker

## Introduction

The Circuit Breaker Pattern is a resilience pattern that **prevents an application from repeatedly calling a failing service**.

Instead of continuously sending requests to an unavailable dependency, the circuit breaker temporarily blocks requests, allowing the failing service time to recover.

The main goals of the Circuit Breaker pattern are:

- Prevent cascading failures.
- Protect failing services.
- Improve system stability.
- Recover gracefully from outages.

---

## Why was it Introduced?

Consider an application calling a Payment Service.

```text
Application

      |

      ▼

Payment Service
```

If the Payment Service becomes unavailable and the application continues sending requests:

- Resources are wasted.
- Response times increase.
- Threads become blocked.
- Other services may also fail.

The Circuit Breaker stops sending requests after repeated failures.

---

## Architecture Diagram

```text
             Client

                |

                ▼

        Circuit Breaker

          /         \

     Closed      Open

        |           |

        ▼           ▼

   Target Service  Fail Fast

          |

     Half-Open

          |

     Recovery Check
```

---

## How It Works

The communication flow:

```text
1. Client sends a request.

2. Circuit Breaker forwards the request.

3. If the request succeeds:
      Keep the circuit closed.

4. If failures exceed a threshold:
      Open the circuit.

5. While open:
      Reject requests immediately.

6. After a timeout:
      Enter Half-Open state.

7. Allow a few test requests.

8. If successful:
      Close the circuit.

9. Otherwise:
      Reopen the circuit.
```

---

# Circuit Breaker States

## 1. Closed State

```text
Client

  |

  ▼

Service
```

All requests are forwarded normally.

---

## 2. Open State

```text
Client

  |

  ▼

Circuit Breaker

  |

Fail Fast
```

Requests are rejected immediately without contacting the service.

---

## 3. Half-Open State

```text
Client

  |

  ▼

Test Request

  |

Service
```

A limited number of requests determine whether the service has recovered.

---

# Core Components

## 1. Failure Counter

Tracks consecutive failures.

---

## 2. Failure Threshold

The number of failures required to open the circuit.

---

## 3. Recovery Timeout

The waiting period before entering the Half-Open state.

---

## 4. Circuit States

- Closed
- Open
- Half-Open

---

# Core Characteristics

## 1. Fast Failure Detection

Repeated failures quickly trigger protection.

---

## 2. Automatic Recovery

The circuit periodically checks if the service has recovered.

---

## 3. Resource Protection

Avoids wasting threads and network resources.

---

## 4. Improved Availability

Healthy services continue operating even if one dependency fails.

---

## 5. Often Combined with Retry

Retries usually occur only while the circuit is closed.

---

# Advantages

## 1. Prevents Cascading Failures

Stops failures from spreading across services.

---

## 2. Reduces Load

Protects an already failing service from additional requests.

---

## 3. Faster Responses

Clients fail immediately instead of waiting for long timeouts.

---

## 4. Automatic Recovery

The Half-Open state allows the system to recover without manual intervention.

---

## 5. Improves System Stability

Keeps healthy components responsive during dependency failures.

---

# Disadvantages

## 1. Increased Complexity

Requires monitoring failures and managing circuit states.

---

## 2. Configuration Challenges

Thresholds and timeouts must be tuned carefully.

---

## 3. Temporary Request Rejection

Some requests may fail even after the service has recovered until the circuit closes.

---

## 4. Additional Monitoring

Metrics are needed to understand circuit behavior.

---

## 5. Not a Replacement for Reliable Services

The pattern manages failures but does not eliminate their root causes.

---

# Real-World Examples

## Payment Systems

Stop calling an unavailable payment gateway after repeated failures.

---

## Microservices

Protect downstream services from excessive traffic during outages.

---

## Cloud APIs

Prevent repeated calls to unavailable third-party APIs.

---

## Databases

Temporarily stop sending requests to an overloaded database.

---

# When to Use

Use the Circuit Breaker pattern when:

- Calling external services.
- Building microservices.
- Network failures are possible.
- Cascading failures must be prevented.

---

# When NOT to Use

Avoid the Circuit Breaker pattern when:

- Operations are entirely local.
- The dependency is extremely reliable and inexpensive to call.
- Failure handling adds unnecessary complexity.

---

# Comparison

| Feature | Retry Pattern | Circuit Breaker |
|---|---|---|
| Purpose | Recover from transient failures | Prevent repeated failures |
| Failed Requests | Retried | Blocked after threshold |
| Improves Reliability | Yes | Yes |
| Protects Dependencies | Limited | Strong |
| Automatic Recovery | Retry-based | State-based |

---

# Interview Questions

## 1. What is the Circuit Breaker pattern?

A resilience pattern that temporarily stops sending requests to a failing service after repeated failures.

---

## 2. What are the three Circuit Breaker states?

- Closed
- Open
- Half-Open

---

## 3. What happens in the Open state?

Requests fail immediately without contacting the target service.

---

## 4. Why is the Half-Open state important?

It allows a small number of requests to verify whether the service has recovered before fully reopening traffic.

---

## 5. Which patterns are commonly used with Circuit Breaker?

- Retry
- Timeout
- Fallback

---

# Key Takeaways

- The Circuit Breaker prevents repeated calls to failing services.
- It protects systems from cascading failures.
- It operates using Closed, Open, and Half-Open states.
- It automatically tests service recovery.
- It is one of the most important resilience patterns in distributed systems.

---

## Previous & Next

← Previous: [Retry Pattern](01-Retry-Pattern.md)

→ Next: [Timeout](03-Timeout.md)