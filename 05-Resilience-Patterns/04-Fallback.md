# Fallback

## Introduction

The Fallback Pattern is a resilience pattern that **provides an alternative response when the primary operation fails**.

Instead of returning an error immediately, the application responds with a predefined backup response, cached data, default values, or an alternative service.

The main goals of the Fallback pattern are:

- Improve user experience.
- Increase system availability.
- Reduce the impact of failures.
- Provide graceful degradation.

---

## Why was it Introduced?

In distributed systems, dependencies sometimes fail.

Example:

```text
Product Service

      |

      ▼

Recommendation Service

      |

❌ Service Unavailable
```

Without a fallback:

```text
User

      |

Error Page
```

With a fallback:

```text
User

      |

Popular Products
```

Users still receive a useful response.

---

## Architecture Diagram

```text
            Client

               |

               ▼

        Primary Service

         /          \

   Success        Failure

      |              |

      ▼              ▼

 Response      Fallback Logic

                     |

                     ▼

         Cached / Default Response
```

---

## How It Works

The communication flow:

```text
1. Client sends a request.

2. Primary service processes the request.

3. If successful:
      Return the normal response.

4. If the request fails:
      Execute fallback logic.

5. Return an alternative response.
```

Example:

```text
Recommendation Service

        |

❌ Failure

        |

Read Cached Recommendations

        |

Return Response
```

---

# Core Components

## 1. Primary Operation

The main business operation.

---

## 2. Failure Detection

Detects when the primary operation cannot complete successfully.

---

## 3. Fallback Logic

Defines the alternative behavior.

---

## 4. Alternative Response

May return:

- Cached data.
- Default values.
- Static content.
- Response from another service.

---

# Core Characteristics

## 1. Graceful Degradation

The application continues functioning with reduced capabilities.

---

## 2. Improved Availability

Users receive a response even during failures.

---

## 3. Flexible Recovery

Different fallback strategies can be used for different operations.

---

## 4. Reduced User Impact

Failures are hidden whenever possible.

---

## 5. Often Combined with Other Patterns

Commonly used with:

- Retry
- Timeout
- Circuit Breaker

---

# Common Fallback Strategies

## 1. Default Response

Return predefined values.

Example:

```text
"No recommendations available."
```

---

## 2. Cached Data

Return previously retrieved data.

---

## 3. Alternative Service

Use another service that provides similar functionality.

---

## 4. Static Content

Serve predefined content when dynamic data is unavailable.

---

# Advantages

## 1. Better User Experience

Users receive meaningful responses instead of errors.

---

## 2. Improved Availability

Applications remain partially functional during failures.

---

## 3. Reduced Downtime Impact

Temporary outages have less effect on users.

---

## 4. Flexible Implementation

Fallback behavior can vary by use case.

---

## 5. Complements Other Resilience Patterns

Works well after retries, timeouts, or circuit breakers fail.

---

# Disadvantages

## 1. Stale Data

Cached responses may not reflect the latest information.

---

## 2. Limited Functionality

Fallback responses may provide fewer features than the primary service.

---

## 3. Additional Development Effort

Fallback logic must be designed and maintained.

---

## 4. Hidden Failures

Frequent fallback responses may hide underlying system issues if not monitored.

---

## 5. Not Suitable for Critical Operations

Returning default data may be unacceptable for operations such as financial transactions.

---

# Real-World Examples

## E-Commerce

Recommendation service fails.

Fallback:

- Show popular products.

---

## Weather Applications

Weather API fails.

Fallback:

- Display the last cached forecast.

---

## Streaming Platforms

Recommendation engine fails.

Fallback:

- Display trending content.

---

## News Applications

Personalized feed fails.

Fallback:

- Show top headlines.

---

# When to Use

Use the Fallback pattern when:

- Alternative responses are acceptable.
- User experience should be preserved.
- Cached or default data is available.
- Temporary degradation is preferable to complete failure.

---

# When NOT to Use

Avoid the Fallback pattern when:

- Operations require accurate real-time data.
- Incorrect or stale information could cause business problems.
- Critical transactions must either succeed or fail explicitly.

---

# Comparison

| Feature | No Fallback | Fallback Pattern |
|---|---|---|
| Failure Response | Error | Alternative Response |
| User Experience | Poor | Better |
| Availability | Lower | Higher |
| Uses Cached Data | No | Often |
| Graceful Degradation | No | Yes |

---

# Interview Questions

## 1. What is the Fallback pattern?

A resilience pattern that returns an alternative response when the primary operation fails.

---

## 2. What are common fallback responses?

- Cached data.
- Default values.
- Static content.
- Alternative services.

---

## 3. Why is the Fallback pattern useful?

It improves availability and user experience during dependency failures.

---

## 4. Can stale data be returned?

Yes.

Many fallback implementations return cached data that may not contain the latest updates.

---

## 5. Which patterns are commonly used with Fallback?

- Retry
- Timeout
- Circuit Breaker

---

# Key Takeaways

- The Fallback pattern provides alternative responses during failures.
- It enables graceful degradation instead of complete failure.
- Cached data and default responses are common fallback strategies.
- It is often combined with Retry, Timeout, and Circuit Breaker.
- It improves availability while maintaining a better user experience.

---

## Previous & Next

← Previous: [Timeout](03-Timeout.md)

→ Next: [Bulkhead](05-Bulkhead.md)