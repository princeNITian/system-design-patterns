# Attribute-Based Access Control (ABAC)

## Introduction

Attribute-Based Access Control (ABAC) is an authorization pattern that **grants or denies access based on attributes associated with the user, resource, action, and environment rather than predefined roles**.

Instead of asking only **"What role does the user have?"**, ABAC evaluates policies using multiple attributes.

ABAC answers the question:

> **"Does this request satisfy the required access policy?"**

The main goals of ABAC are:

- Enable fine-grained access control.
- Support dynamic authorization decisions.
- Reduce role explosion.
- Enforce policy-driven security.

---

## Why was it Introduced?

Imagine a company with employees across multiple countries and departments.

A finance manager should access payroll records only when:

- They belong to the Finance department.
- They are accessing from the corporate network.
- The request occurs during business hours.

Using RBAC alone:

```text
Finance Manager

↓

Access Payroll
```

This grants access regardless of location or time.

With ABAC:

```text
Department = Finance

AND

Location = Corporate Network

AND

Time = Business Hours

↓

Access Granted
```

The decision is based on attributes rather than a static role.

---

## Architecture Diagram

```text
            User

              |

      Authentication

              |

              ▼

     Authorization Engine

              |

      Evaluate Policies

              |

   User Attributes
   Resource Attributes
   Action Attributes
   Environment Attributes

              |

              ▼

      Allow / Deny Access
```

The authorization engine evaluates policies against request attributes.

---

## How It Works

The authorization flow:

```text
1. User authenticates.

2. User requests a resource.

3. System collects request attributes.

4. Authorization engine evaluates policies.

5. Access is granted or denied.
```

Example:

```text
User Department = Finance

AND

Document Classification = Finance

AND

Location = Office

↓

Access Granted
```

---

# Types of Attributes

## 1. User Attributes

Describe the user.

Examples:

- Department
- Job Title
- Clearance Level
- Employment Status

---

## 2. Resource Attributes

Describe the resource.

Examples:

- Owner
- Classification
- Department
- Sensitivity Level

---

## 3. Action Attributes

Describe the requested operation.

Examples:

- Read
- Create
- Update
- Delete

---

## 4. Environment Attributes

Describe the request context.

Examples:

- Time
- Date
- Device
- IP Address
- Geographic Location

---

# Example Policy

```text
IF

User.Department = Finance

AND

Resource.Type = Payroll

AND

Action = Read

AND

Location = Office

THEN

Allow
```

---

# Core Characteristics

## 1. Policy-Based

Access decisions are driven by policies rather than fixed roles.

---

## 2. Dynamic Authorization

Policies are evaluated at request time.

---

## 3. Fine-Grained Access Control

Multiple attributes influence authorization decisions.

---

## 4. Context Awareness

Environmental factors affect access decisions.

---

## 5. Highly Flexible

Supports complex enterprise security requirements.

---

# Advantages

## 1. Very Fine-Grained Control

Supports highly specific authorization policies.

---

## 2. Reduces Role Explosion

Policies replace many specialized roles.

---

## 3. Context-Aware Decisions

Considers location, time, device, and other environmental attributes.

---

## 4. Centralized Policy Management

Policies can be updated without changing application code.

---

## 5. Scalable

Well suited for large organizations with complex access requirements.

---

# Disadvantages

## 1. Higher Complexity

Policies are more complex than simple role assignments.

---

## 2. Performance Overhead

Evaluating many attributes may increase authorization latency.

---

## 3. Difficult Debugging

Understanding why access was granted or denied can be challenging.

---

## 4. Policy Maintenance

Large organizations may accumulate many authorization policies.

---

## 5. Learning Curve

Developers and administrators must understand policy-based authorization.

---

# Real-World Examples

## AWS IAM

Uses policies that evaluate principals, actions, resources, and conditions.

---

## Azure Role and Policy Management

Supports attribute-based access conditions in addition to role assignments.

---

## Google Cloud IAM Conditions

Allows context-aware access using conditional policies.

---

## Enterprise Identity Platforms

Use ABAC to enforce regulatory and organizational access policies.

---

# When to Use

Use ABAC when:

- Access depends on context.
- Policies change frequently.
- Fine-grained authorization is required.
- Large enterprises require flexible security.
- Regulatory compliance requires conditional access.

---

# When NOT to Use

Avoid ABAC when:

- Permission requirements are simple.
- Roles alone adequately represent user responsibilities.
- Minimal authorization complexity is preferred.

---

# Comparison

| Feature | RBAC | ABAC |
|---|---|---|
| Access Based On | Roles | Attributes and Policies |
| Flexibility | Moderate | High |
| Context Awareness | Limited | Excellent |
| Complexity | Lower | Higher |
| Fine-Grained Authorization | Moderate | Excellent |

---

# Interview Questions

## 1. What is ABAC?

An authorization model that grants or denies access based on user, resource, action, and environment attributes.

---

## 2. How is ABAC different from RBAC?

RBAC assigns permissions through roles, while ABAC evaluates policies using multiple attributes.

---

## 3. What are the four major categories of attributes?

- User
- Resource
- Action
- Environment

---

## 4. Why is ABAC considered context-aware?

Because authorization decisions can depend on factors such as location, time, device, or network.

---

## 5. Which cloud platforms support ABAC?

- AWS IAM (policy conditions)
- Microsoft Azure
- Google Cloud IAM Conditions

---

# Key Takeaways

- ABAC uses policies and attributes instead of only roles.
- It supports dynamic, fine-grained authorization.
- Environmental context can influence access decisions.
- ABAC reduces role explosion but introduces greater complexity.
- It is commonly used in large enterprises and cloud platforms.

---

## Previous & Next

← Previous: [Role-Based Access Control (RBAC)](08-Role-Based-Access-Control-RBAC.md)

→ Next: [Encryption at Rest](10-Encryption-at-Rest.md)