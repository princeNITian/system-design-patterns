# OpenID Connect (OIDC)

## Introduction

OpenID Connect (OIDC) is an **authentication protocol built on top of OAuth 2.0** that enables applications to verify the identity of a user.

While OAuth 2.0 answers:

> **"Can this application access the user's resources?"**

OpenID Connect answers:

> **"Who is the user?"**

OIDC introduces an **ID Token**, which securely carries information about the authenticated user.

The main goals of OpenID Connect are:

- Authenticate users.
- Enable Single Sign-On (SSO).
- Standardize user identity.
- Build on the OAuth 2.0 framework.

---

## Why was it Introduced?

OAuth 2.0 provides authorization but does not define how applications verify user identity.

For example:

```text
User

↓

Google Login

↓

Access Token
```

The application receives an access token but cannot reliably determine:

- Who the user is.
- Whether the login succeeded.
- Basic user identity information.

OpenID Connect solves this by issuing an **ID Token**.

```text
User

↓

Google Login

↓

ID Token

↓

Application Knows User Identity
```

---

## Architecture Diagram

```text
                User

                  |

             Login Request

                  |

                  ▼

        OpenID Provider (OP)

                  |

       Authenticate User

                  |

    ID Token + Access Token

                  |

                  ▼

      Client Application

                  |

        Verify ID Token

                  |

      Authenticated User
```

The client verifies the ID Token before trusting the user's identity.

---

## OIDC Components

### 1. End User

The person logging into the application.

---

### 2. Client

The application requesting authentication.

---

### 3. OpenID Provider (OP)

Authenticates users and issues tokens.

Examples:

- Google
- Microsoft Entra ID
- Auth0
- Okta

---

### 4. Resource Server

Hosts APIs that are accessed using the access token.

---

## How It Works

The authentication flow:

```text
1. User clicks Login.

2. Client redirects user to the OpenID Provider.

3. User authenticates.

4. Provider issues:
      - ID Token
      - Access Token

5. Client validates the ID Token.

6. User is authenticated.

7. Access Token is used to call APIs.
```

---

# Tokens in OpenID Connect

## 1. ID Token

Used to authenticate the user.

Contains claims such as:

```text
User ID

Name

Email

Issuer

Expiration Time
```

Usually implemented as a signed JWT.

---

## 2. Access Token

Used to access protected APIs.

---

## 3. Refresh Token

Obtains new access tokens without requiring the user to log in again.

---

# Common OIDC Claims

Example ID Token payload:

```json
{
  "sub": "12345",
  "name": "Alice",
  "email": "alice@example.com",
  "iss": "https://accounts.example.com",
  "aud": "client-id",
  "exp": 1750000000
}
```

Common claims:

- `sub` – Subject (user identifier)
- `name` – User's name
- `email` – Email address
- `iss` – Issuer
- `aud` – Audience
- `exp` – Expiration time

---

# Core Characteristics

## 1. Authentication Protocol

Verifies user identity.

---

## 2. Built on OAuth 2.0

Uses the OAuth 2.0 framework for authorization.

---

## 3. ID Token

Introduces the ID Token for authentication.

---

## 4. Standardized Identity

Provides a common identity format across providers.

---

## 5. Single Sign-On (SSO)

Supports logging into multiple applications with one identity.

---

# Advantages

## 1. Secure Authentication

Provides a standardized way to verify user identity.

---

## 2. Single Sign-On

Users authenticate once and access multiple applications.

---

## 3. Industry Standard

Supported by most modern identity providers.

---

## 4. Rich User Information

Applications receive standardized user claims.

---

## 5. Works with OAuth 2.0

Combines authentication and authorization in a standardized ecosystem.

---

# Disadvantages

## 1. More Complex than Basic Login

Requires understanding OAuth 2.0 and token validation.

---

## 2. Token Management

Applications must securely validate and manage tokens.

---

## 3. External Dependency

Applications rely on an identity provider.

---

## 4. Configuration Overhead

Redirect URIs, client IDs, scopes, and issuer settings must be configured correctly.

---

## 5. Learning Curve

Developers must understand the distinction between authentication and authorization.

---

# Real-World Examples

## Sign in with Google

Authenticate users using their Google accounts.

---

## Sign in with Microsoft

Authenticate users through Microsoft Entra ID.

---

## GitHub Enterprise

Authenticate enterprise users through external identity providers.

---

## Auth0

Provides OpenID Connect authentication services for applications.

---

# When to Use

Use OpenID Connect when:

- Implementing user login.
- Building Single Sign-On (SSO).
- Integrating with external identity providers.
- Supporting social login.
- Authenticating users in web or mobile applications.

---

# When NOT to Use

Avoid OpenID Connect when:

- Only delegated authorization is required (OAuth 2.0 alone may be sufficient).
- Authentication is handled entirely within a simple internal system without external identity providers.

---

# Comparison

| Feature | OAuth 2.0 | OpenID Connect |
|---|---|---|
| Primary Purpose | Authorization | Authentication |
| User Identity | No | Yes |
| Access Token | Yes | Yes |
| ID Token | No | Yes |
| Built on OAuth 2.0 | — | Yes |

---

# Interview Questions

## 1. What is OpenID Connect?

An authentication protocol built on top of OAuth 2.0 that verifies user identity.

---

## 2. What is the difference between OAuth 2.0 and OpenID Connect?

OAuth 2.0 authorizes applications to access resources, while OpenID Connect authenticates users and provides identity information.

---

## 3. What is an ID Token?

A signed token, typically a JWT, that contains authenticated user identity claims.

---

## 4. Why is OpenID Connect used for Single Sign-On?

Because it provides standardized user authentication across multiple applications.

---

## 5. Which companies commonly support OpenID Connect?

- Google
- Microsoft
- Okta
- Auth0
- Keycloak

---

# Key Takeaways

- OpenID Connect adds authentication to OAuth 2.0.
- It introduces the ID Token for verifying user identity.
- OIDC is widely used for Single Sign-On and social login.
- OAuth 2.0 handles authorization, while OIDC handles authentication.
- Modern identity providers commonly support OpenID Connect.

---

## Previous & Next

← Previous: [OAuth 2.0](06-OAuth-2.0.md)

→ Next: [Role-Based Access Control (RBAC)](08-Role-Based-Access-Control-RBAC.md)