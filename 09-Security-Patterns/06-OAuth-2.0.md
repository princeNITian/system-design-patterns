# OAuth 2.0

## Introduction

OAuth 2.0 is an authorization framework that **allows an application to obtain limited access to a user's resources without requiring the user's password**.

Instead of sharing credentials with third-party applications, users authorize access through an authorization server, which issues access tokens.

OAuth 2.0 answers the question:

> **"Can this application access the user's resources?"**

**Important:** OAuth 2.0 is an **authorization** framework, **not an authentication protocol**. Authentication is commonly provided by **OpenID Connect (OIDC)**, which is built on top of OAuth 2.0.

The main goals of OAuth 2.0 are:

- Delegate authorization.
- Protect user credentials.
- Enable secure third-party integrations.
- Provide limited, revocable access.

---

## Why was it Introduced?

Imagine a calendar application that wants to access a user's Google Drive.

Without OAuth 2.0:

```text
User

↓

Shares Google Password

↓

Calendar App
```

The application now has full access to the user's account.

With OAuth 2.0:

```text
User

↓

Approves Access

↓

Access Token

↓

Calendar App
```

The application receives only the permissions that the user approves.

---

## Architecture Diagram

```text
                User

                  |

      Authorize Application

                  |

                  ▼

       Authorization Server

                  |

        Access Token Issued

                  |

                  ▼

     Client Application

                  |

      API Request + Token

                  |

                  ▼

        Resource Server

                  |

        Validate Token

                  |

        Protected Resource
```

The client never receives the user's password.

---

## OAuth 2.0 Roles

### 1. Resource Owner

The user who owns the protected resources.

---

### 2. Client

The application requesting access.

Example:

```text
Spotify

Slack

GitHub App
```

---

### 3. Authorization Server

Authenticates the user and issues access tokens.

Example:

```text
Google Accounts

Microsoft Entra ID

Auth0
```

---

### 4. Resource Server

Hosts the protected APIs or resources.

Example:

```text
Google Drive API

GitHub API

Microsoft Graph API
```

---

## How It Works

The high-level flow:

```text
1. Client requests authorization.

2. User logs in and grants permission.

3. Authorization server issues an authorization code.

4. Client exchanges the code for an access token.

5. Client calls the protected API.

6. Resource server validates the access token.

7. Protected resource is returned.
```

---

## OAuth 2.0 Grant Types

### 1. Authorization Code Grant

The most common and recommended flow for web and mobile applications.

---

### 2. Client Credentials Grant

Used for machine-to-machine communication where no user is involved.

Example:

```text
Service A

↓

Service B
```

---

### 3. Device Authorization Grant

Designed for devices with limited input capabilities, such as smart TVs.

---

### 4. Refresh Token Flow

Allows a client to obtain a new access token without requiring the user to log in again.

---

## Access Token vs Refresh Token

| Feature | Access Token | Refresh Token |
|---|---|---|
| Purpose | Access APIs | Obtain New Access Tokens |
| Lifetime | Short | Long |
| Sent to APIs | Yes | No |
| Exposure Risk | Higher | Lower (should be securely stored) |

---

# Core Characteristics

## 1. Delegated Authorization

Users authorize applications without sharing passwords.

---

## 2. Token-Based Access

Applications use access tokens instead of credentials.

---

## 3. Limited Permissions

Applications receive only the approved scopes.

---

## 4. Revocable Access

Users or providers can revoke granted permissions.

---

## 5. Widely Adopted Standard

OAuth 2.0 is supported by most major identity providers.

---

# Advantages

## 1. Password Protection

Third-party applications never receive user passwords.

---

## 2. Fine-Grained Permissions

Applications receive only the requested scopes.

---

## 3. Revocable Access

Permissions can be revoked without changing the user's password.

---

## 4. Secure Third-Party Integrations

Enables trusted application ecosystems.

---

## 5. Industry Standard

Supported by Google, Microsoft, GitHub, Facebook, and many others.

---

# Disadvantages

## 1. Protocol Complexity

OAuth 2.0 includes multiple flows and token types.

---

## 2. Incorrect Implementation Risks

Misconfigured redirect URIs, missing PKCE, or improper token validation can introduce security vulnerabilities.

---

## 3. Token Management

Applications must securely store and refresh tokens.

---

## 4. Multiple Components

Requires an authorization server and resource server.

---

## 5. Authorization Only

OAuth 2.0 alone does not authenticate users.

---

# Real-World Examples

## Sign in with Google

Applications request permission to access Google APIs.

---

## GitHub OAuth Apps

Third-party applications access repositories after user approval.

---

## Microsoft 365

Applications access Outlook, OneDrive, and Microsoft Graph APIs.

---

## Slack Integrations

Third-party apps access Slack workspaces using OAuth.

---

# When to Use

Use OAuth 2.0 when:

- Building third-party integrations.
- Allowing delegated API access.
- Accessing cloud provider APIs.
- Connecting external applications securely.
- Implementing machine-to-machine authorization.

---

# When NOT to Use

Avoid OAuth 2.0 when:

- A simple internal authentication system is sufficient.
- No delegated authorization is required.
- User identity alone is needed (consider OpenID Connect).

---

# Comparison

| Feature | API Keys | OAuth 2.0 |
|---|---|---|
| User Approval | No | Yes |
| Delegated Access | No | Yes |
| Fine-Grained Permissions | Limited | Yes |
| Password Sharing | Possible | No |
| Typical Use Case | Simple API Access | Third-Party Authorization |

---

# Interview Questions

## 1. What is OAuth 2.0?

An authorization framework that allows applications to access user resources without obtaining the user's password.

---

## 2. Is OAuth 2.0 an authentication protocol?

No. OAuth 2.0 provides authorization. Authentication is commonly implemented using OpenID Connect (OIDC).

---

## 3. What are the four OAuth 2.0 roles?

- Resource Owner
- Client
- Authorization Server
- Resource Server

---

## 4. What is the difference between an access token and a refresh token?

An access token is used to call APIs, while a refresh token is used to obtain new access tokens.

---

## 5. Which OAuth 2.0 flow is recommended for modern web applications?

The Authorization Code Grant with PKCE (Proof Key for Code Exchange).

---

# Key Takeaways

- OAuth 2.0 enables delegated authorization without sharing passwords.
- Applications receive access tokens instead of user credentials.
- OAuth 2.0 is an authorization framework, not an authentication protocol.
- Authorization Code Grant with PKCE is the recommended flow for most modern clients.
- OAuth 2.0 powers secure integrations across cloud platforms and third-party applications.

---

## Previous & Next

← Previous: [JWT (JSON Web Token)](05-JWT-JSON-Web-Token.md)

→ Next: [OpenID Connect (OIDC)](07-OpenID-Connect-OIDC.md)