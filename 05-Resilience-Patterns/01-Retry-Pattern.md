# Retry Pattern

## Introduction

The Retry Pattern is a resilience pattern that **automatically retries a failed operation before reporting it as a failure**.

Many failures in distributed systems are temporary, such as network glitches, transient service outages, or short-lived resource contention. Retrying the operation after a short delay often succeeds without user intervention.

The main goals of the Retry Pattern are:

- Recover from transient failures.
- Improve application reliability.
- Reduce manual intervention.
- Increase the success rate of operations.

---

## Why was it Introduced?

In distributed systems, requests may fail temporarily because of:

- Network latency.
- Temporary service outages.
- Database connection issues.
- Rate limiting.

Immediately failing the request can reduce system reliability.

Instead, the application retries the operation.

---

## Architecture Diagram

```text
           Client

              |

              ▼

         Send Request

              |

              ▼

        Target Service

         /          \

    Success       Failure

                     |

                     ▼

              Retry Policy

                     |

              Retry Request

                     |

                     ▼

             Target Service
```

---

## How It Works

The communication flow:

```text
1. Client sends a request.

2. Service processes the request.

3. If successful:
      Return the response.

4. If the request fails:
      Wait for a retry interval.

5. Retry the request.

6. Continue until:
      - Success
      - Maximum retries reached
```

Example:

```text
Attempt 1

❌ Failure

      |

Wait 1 Second

      |

Attempt 2

❌ Failure

      |

Wait 2 Seconds

      |

Attempt 3

✅ Success
```

---

# Core Components

## 1. Initial Request

The original operation.

---

## 2. Retry Policy

Defines:

- Maximum retries.
- Retry interval.
- Backoff strategy.

---

## 3. Delay Strategy

Determines how long to wait before retrying.

Examples:

- Fixed Delay.
- Exponential Backoff.
- Exponential Backoff with Jitter.

---

## 4. Target Service

The external dependency being retried.

---

# Core Characteristics

## 1. Automatic Retries

Failed operations are retried without user involvement.

---

## 2. Configurable Limits

Retries are limited to prevent infinite loops.

---

## 3. Delay Between Attempts

Waiting before retries reduces pressure on recovering systems.

---

## 4. Best for Transient Failures

Designed for temporary, not permanent, failures.

---

## 5. Often Combined with Other Patterns

Commonly used with:

- Circuit Breaker.
- Timeout.
- Fallback.

---

# Common Retry Strategies

## 1. Fixed Delay

Wait the same amount of time before every retry.

Example:

```text
1s

1s

1s
```

---

## 2. Exponential Backoff

Increase the delay after each failed attempt.

Example:

```text
1s

2s

4s

8s
```

---

## 3. Exponential Backoff with Jitter

Adds random variation to the delay to prevent many clients from retrying simultaneously.

---

# Advantages

## 1. Improves Reliability

Temporary failures often recover automatically.

---

## 2. Better User Experience

Users experience fewer visible failures.

---

## 3. Easy to Implement

Most frameworks provide built-in retry support.

---

## 4. Reduces Manual Recovery

Applications recover automatically from transient issues.

---

## 5. Works Well in Distributed Systems

Especially useful for network-based communication.

---

# Disadvantages

## 1. Increased Latency

Retries delay the final response.

---

## 2. Additional Load

Repeated requests increase traffic to the target service.

---

## 3. Retry Storms

Many clients retrying simultaneously can overload a recovering service.

---

## 4. Not Suitable for Permanent Failures

Retries cannot fix invalid requests or business logic errors.

---

## 5. Requires Careful Configuration

Poor retry policies may worsen failures.

---

# Real-World Examples

## API Calls

Retry temporary HTTP failures.

---

## Database Connections

Reconnect after transient connection failures.

---

## Message Processing

Retry processing failed messages before moving them to a Dead Letter Queue.

---

## Cloud Services

Retry requests to external services experiencing temporary outages.

---

# When to Use

Use the Retry Pattern when:

- Failures are temporary.
- Network communication is involved.
- External services may recover quickly.
- Operations are idempotent or safe to retry.

---

# When NOT to Use

Avoid the Retry Pattern when:

- Errors are permanent.
- Requests are not safe to repeat.
- Immediate failure is preferable.
- The target service is already overloaded.

---

# Comparison

| Feature | No Retry | Retry Pattern |
|---|---|---|
| Failure Recovery | None | Automatic |
| Reliability | Lower | Higher |
| Latency | Lower | Higher |
| Load on Target | Lower | Higher |
| Best For | Permanent failures | Transient failures |

---

# Interview Questions

## 1. What is the Retry Pattern?

A resilience pattern that automatically retries failed operations before reporting failure.

---

## 2. What is a transient failure?

A temporary failure that is likely to succeed if retried after a short delay.

---

## 3. Why is exponential backoff preferred over fixed delay?

It gradually reduces retry frequency, giving the failing service more time to recover and reducing load.

---

## 4. Why is jitter added to retries?

To prevent many clients from retrying at the same time, which can overwhelm recovering services.

---

## 5. Which patterns are commonly used with Retry?

- Circuit Breaker.
- Timeout.
- Fallback.

---

# Key Takeaways

- The Retry Pattern automatically retries transient failures.
- Retry limits prevent infinite retry loops.
- Exponential backoff with jitter is the preferred retry strategy.
- Retries should be used only for retry-safe operations.
- It is a fundamental resilience pattern in distributed systems.

---

## Previous & Next

← Previous Module: [04-Data-Management-Patterns](../04-Data-Management-Patterns/README.md)

→ Next: [Circuit Breaker](02-Circuit-Breaker.md)