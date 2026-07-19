# Webhook

## Introduction

A Webhook is a communication pattern where one application automatically sends an HTTP request to another application when a specific event occurs.

Instead of continuously asking whether something has changed (polling), the receiving application is notified immediately when the event happens.

The main goals of the Webhook pattern are:

- Enable real-time event notifications.
- Reduce unnecessary API calls.
- Decouple systems.
- Improve efficiency.

---

## Why was it Introduced?

Imagine an online payment system.

A merchant needs to know when:

- A payment succeeds.
- A payment fails.
- A refund is processed.

Without webhooks, the merchant would repeatedly call the payment API.

```text
Merchant

     |

Check Status?

     |

Payment Gateway

     |

"No Change"
```

This creates unnecessary network traffic.

Instead, the payment gateway automatically notifies the merchant when the event occurs.

---

## Architecture Diagram

```text
          Event Occurs

                |

                ▼

        Payment Gateway

                |

      HTTP POST Request

                |

                ▼

       Merchant Webhook URL

                |

                ▼

      Merchant Processes Event
```

The sender pushes the event to the receiver.

---

## How It Works

The communication flow:

```text
1. Receiver registers a webhook URL.

2. An event occurs.

3. Sender creates an event payload.

4. Sender sends an HTTP request.

5. Receiver processes the event.

6. Receiver returns an HTTP success response.
```

Example:

```text
Payment Completed

        |

        ▼

POST /webhook

        |

Merchant Server

        |

Update Order Status
```

---

# Core Components

## 1. Event Producer

Generates the event.

Example:

```text
Stripe
```

---

## 2. Webhook Endpoint

An HTTP endpoint that receives webhook requests.

Example:

```text
POST /webhook
```

---

## 3. Event Payload

Contains information about the event.

Example:

```json
{
  "event": "payment.success",
  "orderId": "12345"
}
```

---

## 4. Receiver

Processes the incoming webhook.

Example:

```text
Merchant Application
```

---

# Core Characteristics

## 1. Event-Driven

Requests are sent only when events occur.

---

## 2. Push-Based Communication

The sender pushes data to the receiver.

---

## 3. HTTP-Based

Most webhooks use HTTP POST requests.

---

## 4. Asynchronous Processing

The sender does not require the receiver to immediately complete business processing.

---

## 5. Loose Coupling

Applications communicate without continuous polling.

---

# Advantages

## 1. Real-Time Notifications

Receivers are notified immediately after an event.

---

## 2. Reduced Network Traffic

No repeated polling requests.

---

## 3. Simpler Integrations

External systems can easily react to events.

---

## 4. Better Performance

Resources are used only when events occur.

---

## 5. Widely Supported

Most SaaS platforms expose webhook integrations.

---

# Disadvantages

## 1. Endpoint Availability

The receiving server must be accessible over the internet.

---

## 2. Retry Handling

Failed deliveries require retry mechanisms.

---

## 3. Duplicate Deliveries

The same webhook may be delivered multiple times.

Receivers should implement idempotency.

---

## 4. Security

Webhook requests should be authenticated and verified using signatures or secrets.

---

## 5. Debugging

Webhook failures can be difficult to diagnose without proper logging.

---

# Real-World Examples

## Payment Systems

Events:

- Payment completed.
- Refund processed.
- Subscription renewed.

---

## GitHub

Events:

- Push.
- Pull Request.
- Issue Created.

---

## E-Commerce

Events:

- Order shipped.
- Order cancelled.
- Inventory updated.

---

## CI/CD Systems

Events:

- Build completed.
- Deployment finished.
- Pipeline failed.

---

# When to Use

Use Webhooks when:

- External systems need real-time notifications.
- Polling is inefficient.
- Event-driven integrations are required.
- Third-party applications need updates.

---

# When NOT to Use

Avoid Webhooks when:

- Immediate synchronous responses are required.
- The receiving system cannot expose a public endpoint.
- Guaranteed instant processing is mandatory.

---

# Comparison

| Feature | Polling | Webhook |
|---|---|---|
| Communication | Client requests updates | Server pushes updates |
| Network Usage | Higher | Lower |
| Latency | Depends on polling interval | Near real-time |
| Efficiency | Lower | Higher |
| Best For | Periodic checks | Event notifications |

---

# Interview Questions

## 1. What is a Webhook?

A communication pattern where one application automatically sends an HTTP request to another application when an event occurs.

---

## 2. How is a Webhook different from polling?

Polling repeatedly asks whether something has changed.

A webhook sends data only when an event actually occurs.

---

## 3. Why should webhook handlers be idempotent?

Because webhook providers may retry deliveries, causing duplicate requests.

---

## 4. How are Webhooks secured?

Common approaches include:

- HMAC signatures.
- Shared secrets.
- HTTPS.
- Timestamp validation.

---

## 5. Name some platforms that provide Webhooks.

- Stripe
- GitHub
- Shopify
- Slack
- Twilio

---

# Key Takeaways

- Webhooks provide real-time event notifications.
- They use push-based HTTP communication.
- They reduce unnecessary polling.
- Receivers should verify requests and handle duplicates safely.
- Webhooks are widely used for third-party integrations and SaaS platforms.

---

## Previous & Next

← Previous: [Event Streaming](09-Event-Streaming.md)

→ Next: [Outbox Pattern](11-Outbox-Pattern.md)