# Timeout

## Introduction

The Timeout Pattern is a resilience pattern that **limits how long an application waits for an operation to complete**.

If an operation does not finish within the configured time, it is terminated and treated as a failure, allowing the application to recover instead of waiting indefinitely.

The main goals of the Timeout pattern are:

- Prevent indefinite waiting.
- Improve application responsiveness.
- Free system resources.
- Detect slow or unresponsive services.

---

## Why was it Introduced?

In distributed systems, requests may become slow because of:

- Network latency.
- Slow databases.
- Overloaded services.
- External API delays.

Without a timeout, requests may wait indefinitely.

```text
Client

      |

      ▼

Waiting...

Waiting...

Waiting...
```

Timeouts stop waiting after a defined period.

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

         /         \

   Response      No Response

      |               |

      ▼               ▼

Return Result     Timeout
```

If the response is not received within the timeout period, the operation fails.

---

## How It Works

The communication flow:

```text
1. Client sends a request.

2. Start a timeout timer.

3. Wait for the response.

4. If the response arrives before the timeout:
      Return the result.

5. Otherwise:
      Stop waiting.

6. Return a timeout error or execute recovery logic.
```

Example:

```text
Request Sent

      |

5 Second Timeout

      |

No Response

      |

Timeout Error
```

---

# Core Components

## 1. Request

The operation being executed.

---

## 2. Timeout Duration

Maximum time allowed for the operation.

---

## 3. Timer

Tracks the elapsed waiting time.

---

## 4. Recovery Logic

Handles timeout failures using patterns such as:

- Retry
- Circuit Breaker
- Fallback

---

# Core Characteristics

## 1. Maximum Waiting Time

Operations cannot wait forever.

---

## 2. Faster Failure Detection

Slow services are detected quickly.

---

## 3. Resource Protection

Threads and connections are released after timeout.

---

## 4. Improved Responsiveness

Applications remain responsive during failures.

---

## 5. Works with Other Patterns

Often combined with Retry and Circuit Breaker.

---

# Advantages

## 1. Prevents Hanging Requests

Applications avoid waiting indefinitely.

---

## 2. Better User Experience

Users receive faster responses, even when failures occur.

---

## 3. Protects Resources

Connections, threads, and memory are freed promptly.

---

## 4. Improves Stability

Slow dependencies cannot block the entire application.

---

## 5. Enables Faster Recovery

Failures are detected early so recovery mechanisms can begin.

---

# Disadvantages

## 1. Configuration Challenges

Timeout values that are too short may reject valid requests.

---

## 2. False Timeouts

Temporary network delays can trigger unnecessary failures.

---

## 3. Increased Failure Rate

Aggressive timeout settings may increase failed requests.

---

## 4. Additional Retry Traffic

Timeouts combined with retries may increase system load.

---

## 5. Requires Monitoring

Timeout values should be tuned using production metrics.

---

# Real-World Examples

## API Calls

Stop waiting for an external API after a configured time.

---

## Database Queries

Cancel slow-running database operations.

---

## Payment Gateways

Fail requests that exceed acceptable response times.

---

## Microservices

Prevent one slow service from blocking others.

---

# When to Use

Use the Timeout pattern when:

- Calling external services.
- Accessing databases.
- Performing network operations.
- Building distributed systems.

---

# When NOT to Use

Avoid the Timeout pattern when:

- Operations are guaranteed to complete quickly.
- Long-running background jobs are expected.
- Interrupting the operation could cause data inconsistency.

---

# Comparison

| Feature | No Timeout | Timeout Pattern |
|---|---|---|
| Maximum Wait Time | Unlimited | Configurable |
| Resource Usage | Higher | Controlled |
| Failure Detection | Slow | Fast |
| Responsiveness | Lower | Higher |
| Suitable for Distributed Systems | Limited | Yes |

---

# Interview Questions

## 1. What is the Timeout pattern?

A resilience pattern that limits how long an application waits for an operation before treating it as a failure.

---

## 2. Why are timeouts important?

They prevent applications from waiting indefinitely for slow or unavailable dependencies.

---

## 3. What happens after a timeout?

The operation fails, and the application may trigger retries, fallbacks, or circuit breakers.

---

## 4. Can a timeout value be too short?

Yes.

An aggressive timeout may cause valid requests to fail unnecessarily.

---

## 5. Which patterns are commonly used with Timeout?

- Retry
- Circuit Breaker
- Fallback

---

# Key Takeaways

- The Timeout pattern limits waiting time for operations.
- It prevents hanging requests and improves responsiveness.
- It helps free system resources during failures.
- Timeout values should be carefully configured and monitored.
- It is a fundamental resilience pattern in distributed systems.

---

## Previous & Next

← Previous: [Circuit Breaker](02-Circuit-Breaker.md)

→ Next: [Fallback](04-Fallback.md)