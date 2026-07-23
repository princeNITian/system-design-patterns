# Authorization

## Introduction

Authorization is a security pattern that **determines what an authenticated user, application, or service is allowed to access or perform**.

It answers the question:

> **"What are you allowed to do?"**

Authorization occurs **after successful authentication**. Once identity has been verified, the system evaluates permissions, roles, or policies to decide whether access should be granted.

The main goals of Authorization are:

- Enforce access control.
- Protect sensitive resources.
- Apply the principle of least privilege.
- Prevent unauthorized actions.

---

## Why was it Introduced?

Imagine an online banking application.

Both a customer and a bank administrator can successfully authenticate.

```text
Customer

↓

Login Successful
```

```text
Administrator

↓

Login Successful
```

Without authorization, both users could perform every operation.

For example:

```text
Customer

↓

Delete Customer Accounts
```

Clearly, this should not be allowed.

Authorization ensures users only perform actions they have permission to perform.

---

## Architecture Diagram

```text
             User

               |

       Authentication

               |

      Identity Verified

               |

               ▼

      Authorization Service

               |

      Check Permissions

               |

      Allow / Deny Access

               |

               ▼

       Protected Resource
```

The authorization service evaluates permissions before granting access.

---

## How It Works

The authorization flow:

```text
1. User authenticates.

2. Identity is verified.

3. User requests a protected resource.

4. Authorization system evaluates permissions.

5. Access is granted or denied.

6. Resource returns a response.
```

Example:

```text
Authenticated User

↓

Request

DELETE /users

↓

Permission Check

↓

Access Denied
```

---

# Common Authorization Models

## 1. Role-Based Access Control (RBAC)

Permissions are assigned to roles.

Example:

```text
Admin

↓

Create Users

Delete Users

Manage System
```

```text
Customer

↓

View Profile

Transfer Money
```

---

## 2. Attribute-Based Access Control (ABAC)

Access decisions are based on attributes such as:

- User
- Resource
- Environment
- Time
- Location

Example:

```text
Department = Finance

AND

Location = Office

↓

Access Granted
```

---

## 3. Access Control Lists (ACL)

Each resource stores a list of users or groups that may access it.

Example:

```text
Document

↓

Alice

Bob

Charlie
```

---

## 4. Policy-Based Authorization

Permissions are evaluated using centrally managed policies.

Common in cloud platforms.

---

# Core Characteristics

## 1. Identity Dependent

Authorization requires successful authentication.

---

## 2. Permission Evaluation

The system determines whether the requested action is allowed.

---

## 3. Resource Protection

Sensitive operations are protected using access control rules.

---

## 4. Least Privilege

Users receive only the permissions necessary to perform their tasks.

---

## 5. Fine-Grained Control

Different users may receive different permissions for the same resource.

---

# Advantages

## 1. Improved Security

Prevents unauthorized access to protected resources.

---

## 2. Fine-Grained Permissions

Different users receive different levels of access.

---

## 3. Supports Compliance

Helps satisfy security and regulatory requirements.

---

## 4. Reduces Risk

Limits damage if an account is compromised.

---

## 5. Flexible Access Models

Supports RBAC, ABAC, ACL, and policy-based approaches.

---

# Disadvantages

## 1. Configuration Complexity

Managing permissions becomes difficult in large systems.

---

## 2. Administrative Overhead

Roles and policies require ongoing maintenance.

---

## 3. Performance Impact

Permission evaluation introduces additional processing.

---

## 4. Misconfiguration Risk

Incorrect permissions may expose sensitive resources or block legitimate users.

---

## 5. Policy Growth

Authorization rules become increasingly complex as systems evolve.

---

# Real-World Examples

## Banking Applications

Customers can access only their own accounts, while administrators manage the platform.

---

## AWS IAM

Permissions determine which AWS resources a user or role can access.

---

## Google Drive

File owners decide who can view, edit, or share documents.

---

## GitHub

Repository permissions control read, write, and administrative access.

---

# When to Use

Use Authorization when:

- Protecting sensitive resources.
- Restricting administrative operations.
- Enforcing business rules.
- Securing APIs.
- Managing multi-user applications.

---

# When NOT to Use

Authorization should be implemented whenever authenticated users have different access levels or permissions.

---

# Comparison

| Feature | Authentication | Authorization |
|---|---|---|
| Purpose | Verify Identity | Grant Permissions |
| Question Answered | Who are you? | What are you allowed to do? |
| Execution Order | First | Second |
| Output | Authenticated Identity | Allow or Deny |
| Example | Login | Permission Check |

---

# Interview Questions

## 1. What is Authorization?

The process of determining what an authenticated user, application, or service is allowed to access or perform.

---

## 2. What is the difference between Authentication and Authorization?

Authentication verifies identity, while authorization determines permissions.

---

## 3. Name common authorization models.

- Role-Based Access Control (RBAC)
- Attribute-Based Access Control (ABAC)
- Access Control Lists (ACL)
- Policy-Based Authorization

---

## 4. What is the Principle of Least Privilege?

Users should receive only the minimum permissions required to perform their responsibilities.

---

## 5. Why does Authorization depend on Authentication?

Because the system must first know the identity of the requester before evaluating permissions.

---

# Key Takeaways

- Authorization determines what authenticated users are allowed to do.
- It always follows successful authentication.
- Common models include RBAC, ABAC, ACL, and policy-based authorization.
- The principle of least privilege minimizes security risks.
- Effective authorization is essential for protecting applications, APIs, and cloud resources.

---

## Previous & Next

← Previous: [Authentication](01-Authentication.md)

→ Next: [API Keys](03-API-Keys.md)