# Authentication

## Introduction

Authentication is a security pattern that **verifies the identity of a user, application, or service before granting access to a system**.

It answers the fundamental question:

> **"Who are you?"**

Authentication is the first step in securing any application. Only after identity has been verified can the system determine what actions the authenticated entity is allowed to perform.

The main goals of Authentication are:

- Verify identity.
- Prevent unauthorized access.
- Protect sensitive resources.
- Establish trust between users and systems.

---

## Why was it Introduced?

Imagine an online banking application.

Without authentication:

```text
User

↓

Bank Application

↓

Account Access
```

Anyone could access any account simply by opening the application.

Authentication ensures that only legitimate users can access protected resources.

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

   Verify Credentials

            |

     Success / Failure

            |

            ▼

      Protected System
```

The authentication server validates the user's identity before access is granted.

---

## How It Works

The authentication flow:

```text
1. User submits credentials.

2. Authentication server verifies credentials.

3. Identity is confirmed.

4. Authentication result is returned.

5. User receives an authenticated session or token.

6. Future requests include proof of authentication.
```

Example:

```text
Username

Password

↓

Authentication Server

↓

Authenticated User
```

---

# Authentication Factors

Authentication can rely on one or more factors.

## 1. Something You Know

Examples:

- Password
- PIN
- Security answer

---

## 2. Something You Have

Examples:

- Mobile phone
- Hardware security key
- Smart card

---

## 3. Something You Are

Examples:

- Fingerprint
- Face recognition
- Iris scan

---

## 4. Multi-Factor Authentication (MFA)

Combines two or more authentication factors.

Example:

```text
Password

+

One-Time Password (OTP)
```

---

# Common Authentication Methods

## 1. Username and Password

The most common authentication mechanism.

---

## 2. One-Time Password (OTP)

Temporary verification code delivered via SMS, email, or authenticator application.

---

## 3. Biometric Authentication

Uses unique physical characteristics.

---

## 4. Token-Based Authentication

Uses access tokens such as JWT after successful login.

---

## 5. Certificate-Based Authentication

Uses digital certificates to verify identity.

---

# Core Characteristics

## 1. Identity Verification

Confirms the identity of the requesting entity.

---

## 2. Credential Validation

Credentials are verified against trusted identity data.

---

## 3. Secure Communication

Authentication should occur over encrypted channels such as HTTPS.

---

## 4. Session or Token Creation

Successful authentication typically results in a session or authentication token.

---

## 5. Foundation for Authorization

Authentication occurs before authorization decisions.

---

# Advantages

## 1. Prevents Unauthorized Access

Only authenticated users can access protected resources.

---

## 2. Improves Security

Identity verification reduces the risk of impersonation.

---

## 3. Supports Auditing

User identity can be associated with actions performed in the system.

---

## 4. Enables Personalized Services

Applications can provide user-specific experiences.

---

## 5. Works with Multiple Security Models

Authentication integrates with RBAC, ABAC, OAuth, JWT, and other authorization mechanisms.

---

# Disadvantages

## 1. Credential Theft

Weak passwords may be compromised.

---

## 2. User Friction

Additional authentication steps may reduce usability.

---

## 3. Password Management

Users often struggle with password creation and storage.

---

## 4. Infrastructure Requirements

Authentication systems require secure identity storage and management.

---

## 5. Attack Surface

Authentication endpoints are common targets for brute-force and phishing attacks.

---

# Real-World Examples

## Online Banking

Users authenticate before accessing account information.

---

## Enterprise Applications

Employees authenticate using corporate identity providers.

---

## Cloud Platforms

AWS, Azure, and Google Cloud require authentication before accessing resources.

---

## Social Media

Users authenticate before interacting with their accounts.

---

# When to Use

Use Authentication when:

- Protecting user accounts.
- Securing APIs.
- Restricting access to applications.
- Identifying services in distributed systems.
- Protecting administrative interfaces.

---

# When NOT to Use

Authentication should be used whenever access control is required. Public resources that require no identity verification may not need authentication.

---

# Comparison

| Feature | Authentication | Authorization |
|---|---|---|
| Purpose | Verify Identity | Grant Permissions |
| Question Answered | Who are you? | What can you do? |
| Performed First | Yes | No |
| Output | Identity Verified | Access Granted or Denied |
| Example | Login | Permission Check |

---

# Interview Questions

## 1. What is Authentication?

The process of verifying the identity of a user, application, or service.

---

## 2. What is the difference between Authentication and Authorization?

Authentication verifies identity, while authorization determines what an authenticated entity is allowed to access.

---

## 3. What are the three primary authentication factors?

- Something you know
- Something you have
- Something you are

---

## 4. What is Multi-Factor Authentication (MFA)?

An authentication approach that combines two or more independent authentication factors.

---

## 5. Why should authentication occur over HTTPS?

To protect credentials from interception during transmission.

---

# Key Takeaways

- Authentication verifies identity before access is granted.
- It answers the question, **"Who are you?"**
- Authentication precedes authorization.
- Multiple authentication factors improve security.
- Secure authentication is the foundation of every modern application.

---

## Previous & Next

← Previous Module: [08-Distributed-System-Patterns](../08-Distributed-System-Patterns/README.md)

→ Next: [Authorization](02-Authorization.md)