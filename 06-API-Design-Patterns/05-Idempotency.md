# Idempotency

## Introduction

Idempotency is an API design pattern that **ensures performing the same operation multiple times produces the same result as performing it once**.

It is especially important for operations that may be retried due to network failures, client timeouts, or temporary service disruptions.

The main goals of Idempotency are:

- Prevent duplicate operations.
- Support safe retries.
- Improve reliability.
- Maintain data consistency.

---

## Why was it Introduced?

Consider an online payment API.

```text
Client

      |

POST /payments
```

The payment succeeds, but the network connection is lost before the client receives the response.

The client retries the request.

Without idempotency:

```text
Payment Processed

      |

Retry

      |

Payment Processed Again ❌
```

The customer is charged twice.

Idempotency prevents duplicate processing.

---

## Architecture Diagram

```text
            Client

               |

               ▼

 POST /payments

Idempotency-Key: abc123

               |

               ▼

            REST API

               |

      Check Idempotency Key

        /              \

   Already Exists    New Request

        |                |

        ▼                ▼

Return Previous    Process Request

Response                |

                          ▼

                 Store Key & Response
```

---

## How It Works

The communication flow:

```text
1. Client generates an Idempotency Key.

2. Request is sent with the key.

3. Server checks whether the key already exists.

4. If the key is new:
      Process the request.
      Store the key and response.

5. If the key already exists:
      Return the previously stored response.
```

Example:

```text
POST /payments

Idempotency-Key: payment-123
```

Retrying with the same key returns the original result instead of creating another payment.

---

# HTTP Methods and Idempotency

## Naturally Idempotent

These HTTP methods are inherently idempotent:

- GET
- PUT
- DELETE
- HEAD
- OPTIONS

Executing them multiple times results in the same final state.

---

## Not Naturally Idempotent

```text
POST
```

POST typically creates new resources and therefore requires additional logic, such as idempotency keys, to become idempotent.

---

# Core Characteristics

## 1. Safe Retries

Repeated requests do not create duplicate operations.

---

## 2. Duplicate Detection

Previously processed requests are identified using an idempotency key.

---

## 3. Consistent Responses

Duplicate requests receive the same response as the original request.

---

## 4. Improved Reliability

Clients can safely retry requests after failures.

---

## 5. Data Consistency

Duplicate writes are prevented.

---

# Advantages

## 1. Prevents Duplicate Transactions

Avoids duplicate payments, orders, or reservations.

---

## 2. Supports Automatic Retries

Clients can retry requests without fear of creating duplicate data.

---

## 3. Improves User Experience

Users are protected from accidental repeated submissions.

---

## 4. Better Fault Tolerance

Temporary network failures are easier to recover from.

---

## 5. Widely Used in Financial Systems

Essential for payment processing and other critical operations.

---

# Disadvantages

## 1. Additional Storage

Servers must store idempotency keys and previous responses.

---

## 2. Expiration Management

Stored keys require cleanup after an appropriate retention period.

---

## 3. Increased Complexity

Applications must implement duplicate detection logic.

---

## 4. Not Suitable for Every Operation

Some operations are intentionally non-idempotent.

---

## 5. Key Management

Clients must generate unique and reusable idempotency keys for retries.

---

# Real-World Examples

## Payment Processing

Prevent duplicate charges when payment requests are retried.

---

## E-Commerce

Avoid duplicate order creation after client retries.

---

## Ticket Booking

Ensure only one reservation is created for the same booking request.

---

## Banking

Prevent duplicate money transfers caused by network failures.

---

# When to Use

Use Idempotency when:

- Processing payments.
- Creating orders.
- Booking reservations.
- Performing any operation that may be retried safely.

---

# When NOT to Use

Avoid implementing idempotency when:

- Operations are intentionally repeatable.
- Each request is expected to create a new resource.
- Duplicate execution is acceptable.

---

# Comparison

| Feature | Without Idempotency | With Idempotency |
|---|---|---|
| Duplicate Requests | Possible | Prevented |
| Safe Retries | No | Yes |
| Data Consistency | Lower | Higher |
| Fault Recovery | Limited | Better |
| Implementation Complexity | Lower | Higher |

---

# Interview Questions

## 1. What is Idempotency?

A property where performing the same operation multiple times produces the same result as performing it once.

---

## 2. Why is Idempotency important?

It prevents duplicate operations when clients retry requests.

---

## 3. Which HTTP methods are naturally idempotent?

- GET
- PUT
- DELETE
- HEAD
- OPTIONS

---

## 4. Why is POST usually not idempotent?

Because each POST request typically creates a new resource.

---

## 5. How is idempotency commonly implemented for POST requests?

By using an Idempotency Key that uniquely identifies a client request.

---

# Key Takeaways

- Idempotency enables safe retries without duplicate processing.
- It is critical for payments, bookings, and financial systems.
- POST requests commonly use idempotency keys.
- Idempotent APIs improve reliability and consistency.
- It is a fundamental pattern in modern API design.

---

## Previous & Next

← Previous: [Filtering & Sorting](04-Filtering-and-Sorting.md)

→ Next: [Rate Limiting](06-Rate-Limiting.md)