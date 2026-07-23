# API Keys

## Introduction

API Keys are a security pattern that **identify and authenticate applications or clients when accessing an API**.

An API key is a unique secret value issued by an API provider. Clients include the key in each request, allowing the server to identify the calling application.

API Keys primarily answer the question:

> **"Which application is making this request?"**

Unlike user authentication mechanisms such as passwords or OAuth, API Keys typically identify **applications**, not individual users.

The main goals of API Keys are:

- Identify API clients.
- Control API access.
- Track API usage.
- Enforce rate limits and quotas.

---

## Why were they Introduced?

Imagine a public weather API.

Without API Keys:

```text
Internet

↓

Weather API
```

Anyone could send unlimited requests, leading to:

- Abuse
- Excessive traffic
- Increased costs
- Denial-of-Service risks

API Keys allow the provider to identify each client and enforce usage policies.

---

## Architecture Diagram

```text
         Client Application

                 |

        API Request + API Key

                 |

                 ▼

            API Gateway

                 |

         Validate API Key

                 |

          Allow / Reject

                 |

                 ▼

              REST API
```

The API Gateway validates the API key before forwarding the request.

---

## How It Works

The authentication flow:

```text
1. Client registers with the API provider.

2. Provider generates an API key.

3. Client stores the key securely.

4. Every API request includes the key.

5. Server validates the key.

6. Request is accepted or rejected.
```

Example:

```http
GET /products HTTP/1.1
Host: api.example.com
X-API-Key: 7fa29b...
```

---

# Where API Keys are Sent

API Keys are commonly transmitted using:

## 1. HTTP Header (Recommended)

```http
X-API-Key: abc123
```

---

## 2. Authorization Header

```http
Authorization: ApiKey abc123
```

---

## 3. Query Parameter (Not Recommended)

```text
GET /products?apiKey=abc123
```

Query parameters may be logged by browsers, proxies, or servers, exposing the key.

---

# Core Characteristics

## 1. Client Identification

API Keys identify the calling application.

---

## 2. Simple Authentication

Validation requires only checking the provided key.

---

## 3. Rate Limiting

Providers can apply request limits per API key.

---

## 4. Usage Monitoring

Requests can be tracked and analyzed for each client.

---

## 5. Key Rotation

API providers can revoke or replace compromised keys.

---

# Advantages

## 1. Easy to Implement

API Keys require minimal infrastructure.

---

## 2. Lightweight

No complex authentication protocol is needed.

---

## 3. Usage Tracking

Each client can be monitored independently.

---

## 4. Supports Quotas

Providers can enforce request limits per client.

---

## 5. Widely Supported

Most API gateways and cloud platforms support API key validation.

---

# Disadvantages

## 1. Limited Security

API Keys identify applications but usually do not authenticate individual users.

---

## 2. Key Leakage

Exposed keys can be misused if stored or transmitted insecurely.

---

## 3. No Fine-Grained Authorization

API Keys generally provide access to an application rather than user-specific permissions.

---

## 4. Static Credentials

Long-lived keys require secure storage and periodic rotation.

---

## 5. Not Suitable for Sensitive User Authentication

OAuth 2.0 or OpenID Connect is typically preferred for user-facing applications.

---

# Best Practices

- Transmit API Keys only over HTTPS.
- Store keys securely using a secrets manager.
- Never hardcode keys in source code.
- Rotate keys periodically.
- Apply rate limits and usage quotas.
- Revoke compromised keys immediately.

---

# Real-World Examples

## Google Maps API

Applications authenticate using API Keys to access mapping services.

---

## OpenAI API

Applications include API Keys to authenticate requests.

---

## Stripe

API Keys identify applications interacting with payment APIs.

---

## AWS API Gateway

Supports API Key validation and usage plans for controlling API access.

---

# When to Use

Use API Keys when:

- Identifying applications consuming an API.
- Applying rate limits.
- Tracking API usage.
- Protecting public developer APIs.
- Enabling third-party integrations.

---

# When NOT to Use

Avoid using API Keys when:

- Authenticating end users.
- Fine-grained authorization is required.
- Sensitive user data is involved.
- Delegated access between systems is needed.

---

# Comparison

| Feature | API Keys | OAuth 2.0 |
|---|---|---|
| Identifies | Application | User or Application |
| User Authentication | No | Yes (with OIDC) |
| Authorization | Limited | Fine-Grained |
| Complexity | Low | High |
| Typical Use Case | Public APIs | User Authorization |

---

# Interview Questions

## 1. What is an API Key?

A unique secret issued by an API provider that identifies an application making API requests.

---

## 2. Are API Keys used for user authentication?

Generally, no. They identify applications rather than individual users.

---

## 3. Where should API Keys be sent?

Preferably in an HTTP header, such as `X-API-Key`.

---

## 4. Why should API Keys not be passed as query parameters?

Because query parameters may be logged or cached, increasing the risk of key exposure.

---

## 5. What are common uses of API Keys?

- Client identification
- API access control
- Usage monitoring
- Rate limiting
- Quota enforcement

---

# Key Takeaways

- API Keys identify applications accessing an API.
- They are simple, lightweight, and widely supported.
- API Keys should always be transmitted over HTTPS and stored securely.
- They are best suited for application-level authentication rather than user authentication.
- API gateways commonly use API Keys for rate limiting and usage tracking.

---

## Previous & Next

← Previous: [Authorization](02-Authorization.md)

→ Next: [Session-Based Authentication](04-Session-Based-Authentication.md)