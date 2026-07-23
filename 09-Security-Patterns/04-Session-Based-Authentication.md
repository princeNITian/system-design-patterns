# Session-Based Authentication

## Introduction

Session-Based Authentication is a security pattern in which **the server creates and maintains a session for an authenticated user after a successful login**.

Instead of sending credentials with every request, the client sends a **session identifier (Session ID)**, and the server uses it to retrieve the user's session information.

It answers the question:

> **"Has this user already been authenticated?"**

The main goals of Session-Based Authentication are:

- Maintain authenticated user state.
- Improve user experience.
- Protect user credentials.
- Enable secure server-managed sessions.

---

## Why was it Introduced?

Without sessions, users would need to send their username and password with every request.

```text
Request 1

↓

Username + Password
```

```text
Request 2

↓

Username + Password
```

This is inefficient and increases the risk of credential exposure.

Instead:

```text
Login

↓

Session Created

↓

Session ID Returned

↓

Future Requests Use Session ID
```

The server remembers the authenticated user.

---

## Architecture Diagram

```text
             User

               |

      Login Credentials

               |

               ▼

      Authentication Server

               |

      Validate Credentials

               |

      Create Session

               |

       Session ID Cookie

               |

               ▼

           Web Browser

               |

     Future Requests

      + Session Cookie

               |

               ▼

      Application Server

               |

      Retrieve Session

               |

      Process Request
```

The server stores session data, while the client stores only the session identifier.

---

## How It Works

The authentication flow:

```text
1. User submits credentials.

2. Server validates credentials.

3. Server creates a session.

4. Session is stored on the server.

5. Session ID is returned to the client.

6. Client includes the Session ID in future requests.

7. Server retrieves the session and authenticates the user.
```

Example:

```text
Login

↓

Session ID = ABC123

↓

Cookie Stored

↓

Future Requests

↓

Cookie: ABC123
```

---

# Session Storage

Sessions are commonly stored in:

## 1. Application Memory

Simple but not suitable for multiple servers.

---

## 2. Redis

Fast, centralized session storage for distributed applications.

---

## 3. Database

Persistent but generally slower than in-memory storage.

---

## 4. Distributed Cache

Supports horizontally scalable applications.

---

# Session Cookies

The Session ID is typically stored in a secure HTTP cookie.

Example:

```http
Set-Cookie: SESSIONID=abc123;
```

Recommended cookie attributes:

```text
HttpOnly

Secure

SameSite
```

These attributes help reduce common web attacks.

---

# Core Characteristics

## 1. Server-Side State

The server stores authentication information.

---

## 2. Session Identifier

The client stores only the Session ID.

---

## 3. Cookie-Based Communication

Browsers automatically send the session cookie with requests.

---

## 4. Session Expiration

Sessions expire after inactivity or a configured timeout.

---

## 5. Session Invalidation

Users can log out by destroying the server-side session.

---

# Advantages

## 1. Strong Server Control

Sessions can be revoked immediately.

---

## 2. Secure Credential Handling

Passwords are sent only during login.

---

## 3. Easy Logout

Destroying the session immediately ends access.

---

## 4. Mature Technology

Widely supported by web frameworks and browsers.

---

## 5. Rich Session Data

Servers can store user preferences, shopping carts, and other session-specific information.

---

# Disadvantages

## 1. Server Memory Usage

Large numbers of sessions consume server resources.

---

## 2. Horizontal Scaling Challenges

Multiple servers require shared session storage or sticky sessions.

---

## 3. Session Hijacking

Stolen Session IDs can allow unauthorized access if additional protections are not used.

---

## 4. Infrastructure Complexity

Distributed deployments often require Redis or another centralized session store.

---

## 5. Stateful Architecture

Session-based authentication is less suitable for stateless REST APIs.

---

# Best Practices

- Use HTTPS for all authenticated traffic.
- Store Session IDs in **HttpOnly** cookies.
- Enable the **Secure** cookie attribute.
- Use **SameSite** cookies to reduce CSRF risks.
- Regenerate Session IDs after login.
- Expire inactive sessions automatically.
- Destroy sessions immediately during logout.

---

# Real-World Examples

## Traditional Web Applications

Most server-rendered websites use session-based authentication.

---

## Online Banking

Users remain authenticated while interacting with their accounts.

---

## E-Commerce Websites

Shopping carts and user sessions are maintained on the server.

---

## Enterprise Portals

Corporate applications often use centralized session management.

---

# When to Use

Use Session-Based Authentication when:

- Building traditional web applications.
- Browsers are the primary clients.
- Immediate session revocation is important.
- Server-side state is acceptable.

---

# When NOT to Use

Avoid Session-Based Authentication when:

- Building stateless REST APIs.
- Supporting many mobile or third-party clients.
- Designing highly distributed microservices without centralized session storage.

---

# Comparison

| Feature | Session-Based Authentication | JWT Authentication |
|---|---|---|
| Session Storage | Server | Client |
| Server State | Required | Not Required |
| Scalability | Lower | Higher |
| Logout | Immediate | Token Expiration or Revocation Required |
| Typical Use Case | Web Applications | APIs and Microservices |

---

# Interview Questions

## 1. What is Session-Based Authentication?

A server-managed authentication mechanism where the server stores user session data and the client stores only a Session ID.

---

## 2. Where is the Session ID usually stored?

In an HTTP cookie, typically configured with `HttpOnly`, `Secure`, and `SameSite` attributes.

---

## 3. Why is Redis commonly used for session storage?

Because it provides fast, centralized, in-memory storage that supports multiple application servers.

---

## 4. What happens during logout?

The server invalidates or deletes the user's session.

---

## 5. Why is Session-Based Authentication considered stateful?

Because the server maintains session information for every authenticated user.

---

# Key Takeaways

- Session-Based Authentication stores user session data on the server.
- Clients send only a Session ID with each request.
- Secure cookies protect the Session ID.
- Redis is commonly used for scalable session storage.
- Session-based authentication is ideal for traditional web applications but less suitable for stateless APIs.

---

## Previous & Next

← Previous: [API Keys](03-API-Keys.md)

→ Next: [JWT (JSON Web Token)](05-JWT-JSON-Web-Token.md)