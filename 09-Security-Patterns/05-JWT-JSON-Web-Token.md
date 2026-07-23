# JWT (JSON Web Token)

## Introduction

JWT (JSON Web Token) is a security pattern that **allows a client to securely carry authentication and authorization information inside a digitally signed token**.

Unlike Session-Based Authentication, where the server stores user session data, JWT stores user claims inside the token itself, making authentication **stateless**.

It answers the question:

> **"Can the server trust the information presented in this token?"**

The main goals of JWT are:

- Enable stateless authentication.
- Reduce server-side session storage.
- Support scalable APIs and microservices.
- Securely transmit user claims.

---

## Why was it Introduced?

Consider a REST API running on multiple servers.

With session-based authentication:

```text
Client

↓

Server A

↓

Session Stored
```

If the next request reaches another server:

```text
Client

↓

Server B

↓

Session Missing
```

The servers need shared session storage such as Redis.

JWT eliminates this dependency.

```text
Client

↓

JWT Token

↓

Any Server

↓

Token Verified
```

Every server can validate the token independently.

---

## Architecture Diagram

```text
              User

                |

         Login Request

                |

                ▼

      Authentication Server

                |

      Validate Credentials

                |

         Generate JWT

                |

                ▼

             Client

                |

      API Request + JWT

                |

                ▼

          API Server

                |

        Verify Signature

                |

      Allow / Reject Access
```

The server verifies the JWT signature instead of looking up a server-side session.

---

## How It Works

The authentication flow:

```text
1. User logs in.

2. Server validates credentials.

3. Server generates a signed JWT.

4. Client stores the JWT.

5. Client includes the JWT in future requests.

6. Server verifies the token signature.

7. Access is granted if the token is valid.
```

Example:

```http
Authorization: Bearer eyJhbGciOiJIUzI1Ni...
```

---

# JWT Structure

A JWT consists of three parts:

```text
Header

.

Payload

.

Signature
```

Example:

```text
xxxxx.yyyyy.zzzzz
```

---

## 1. Header

Contains metadata about the token.

Example:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

---

## 2. Payload

Contains claims about the user.

Example:

```json
{
  "sub": "12345",
  "name": "Alice",
  "role": "Admin",
  "exp": 1750000000
}
```

Common claims:

- `sub` – Subject (user ID)
- `iss` – Issuer
- `aud` – Audience
- `iat` – Issued At
- `exp` – Expiration Time

---

## 3. Signature

Protects the integrity of the token.

The server verifies the signature before trusting the payload.

---

# Core Characteristics

## 1. Stateless

The server does not store authentication sessions.

---

## 2. Self-Contained

The token carries identity and claim information.

---

## 3. Digitally Signed

The signature detects tampering.

---

## 4. Portable

The same token can be used across multiple services.

---

## 5. Expiration Support

JWTs usually contain an expiration time.

---

# Advantages

## 1. Highly Scalable

No centralized session storage is required.

---

## 2. Excellent for APIs

Ideal for REST APIs and microservices.

---

## 3. Reduced Server Load

Authentication does not require database lookups for every request.

---

## 4. Cross-Service Authentication

Multiple services can verify the same token.

---

## 5. Standardized Format

JWT is defined by RFC 7519 and widely supported.

---

# Disadvantages

## 1. Difficult Token Revocation

A valid JWT typically remains usable until it expires unless additional revocation mechanisms are implemented.

---

## 2. Larger Request Size

JWTs are larger than simple session identifiers.

---

## 3. Sensitive Payload

The payload is Base64URL encoded, **not encrypted**, so sensitive information should not be stored inside it.

---

## 4. Expiration Management

Choosing appropriate token lifetimes requires balancing usability and security.

---

## 5. Signature Management

Signing keys must be protected and rotated securely.

---

# Best Practices

- Always use HTTPS.
- Keep JWT expiration times short.
- Never store passwords or sensitive data in the payload.
- Store signing keys securely.
- Use refresh tokens for long-lived sessions.
- Validate signature, issuer, audience, and expiration on every request.

---

# Real-World Examples

## REST APIs

Authenticate users without server-side sessions.

---

## Microservices

Share authentication across multiple services.

---

## Mobile Applications

Carry authentication state between API requests.

---

## Single Page Applications (SPAs)

Use JWTs for stateless authentication with backend APIs.

---

# When to Use

Use JWT when:

- Building REST APIs.
- Designing microservices.
- Supporting mobile applications.
- Scaling horizontally without shared session storage.
- Implementing stateless authentication.

---

# When NOT to Use

Avoid JWT when:

- Immediate session revocation is required.
- Building traditional server-rendered web applications where sessions are sufficient.
- Sensitive information would need to be stored inside the token.

---

# Comparison

| Feature | Session-Based Authentication | JWT Authentication |
|---|---|---|
| Server State | Required | Not Required |
| Session Storage | Server | Client |
| Scalability | Moderate | High |
| Logout | Immediate | Token Expiration or Revocation Required |
| Typical Use Case | Web Applications | APIs and Microservices |

---

# Interview Questions

## 1. What is a JWT?

A digitally signed token that securely carries authentication and authorization claims between a client and a server.

---

## 2. What are the three parts of a JWT?

- Header
- Payload
- Signature

---

## 3. Why is JWT considered stateless?

Because the server does not store authentication session data; the token contains the necessary claims.

---

## 4. Is the JWT payload encrypted?

No. It is Base64URL encoded, not encrypted.

---

## 5. Why is JWT commonly used in microservices?

Because any service with the signing key (or public key, depending on the signing algorithm) can verify the token without accessing centralized session storage.

---

# Key Takeaways

- JWT enables stateless authentication.
- Tokens contain claims and are digitally signed.
- The server verifies the signature instead of maintaining sessions.
- JWT is ideal for APIs, mobile applications, and microservices.
- Short-lived access tokens combined with refresh tokens provide a common balance between scalability and security.

---

## Previous & Next

← Previous: [Session-Based Authentication](04-Session-Based-Authentication.md)

→ Next: [OAuth 2.0](06-OAuth-2.0.md)