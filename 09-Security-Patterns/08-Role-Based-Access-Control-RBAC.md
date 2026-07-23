# Role-Based Access Control (RBAC)

## Introduction

Role-Based Access Control (RBAC) is an authorization pattern that **grants permissions to users based on the roles assigned to them rather than assigning permissions directly to individual users**.

Instead of managing permissions for every user separately, permissions are grouped into roles, and users are assigned one or more roles.

RBAC answers the question:

> **"What actions are allowed for users with this role?"**

The main goals of RBAC are:

- Simplify permission management.
- Enforce the principle of least privilege.
- Improve security.
- Scale authorization for large organizations.

---

## Why was it Introduced?

Imagine a company with 5,000 employees.

Without RBAC:

```text
Alice

↓

Read Reports

Write Reports

Delete Reports

View Dashboard

Approve Expenses

...
```

Every user requires individual permission management.

Now multiply this by thousands of users.

Instead, RBAC groups permissions into roles.

```text
Manager

↓

Read Reports

Approve Expenses
```

```text
Employee

↓

Read Reports

View Dashboard
```

Users simply receive the appropriate role.

---

## Architecture Diagram

```text
          Users

            |

      Assigned Roles

            |

            ▼

         Role

            |

      Permissions

            |

            ▼

      Protected Resource
```

Permissions are associated with roles, not directly with users.

---

## How It Works

The authorization flow:

```text
1. User authenticates.

2. User's assigned roles are loaded.

3. User requests a resource.

4. System checks whether the role contains the required permission.

5. Access is granted or denied.
```

Example:

```text
Alice

↓

Role = Admin

↓

Permission = Delete User

↓

Access Granted
```

---

# RBAC Components

## 1. User

The person or service requesting access.

---

## 2. Role

A collection of permissions.

Examples:

```text
Admin

Manager

Developer

Customer
```

---

## 3. Permission

An allowed action.

Examples:

```text
Read

Write

Delete

Update
```

---

## 4. Resource

The object being accessed.

Examples:

```text
Users

Orders

Products

Reports
```

---

# Example

```text
Role: Admin

↓

Create Users

Delete Users

View Reports

Manage Roles
```

---

```text
Role: Customer

↓

View Products

Create Orders

View Orders
```

---

# Core Characteristics

## 1. Role-Centric

Permissions are assigned to roles.

---

## 2. Reusable Roles

Multiple users can share the same role.

---

## 3. Centralized Permission Management

Permissions are managed once per role.

---

## 4. Least Privilege

Users receive only the permissions associated with their assigned roles.

---

## 5. Easy Administration

Adding or removing users does not require redefining permissions.

---

# Advantages

## 1. Simple Administration

Permission management becomes significantly easier.

---

## 2. Scalable

Supports organizations with thousands of users.

---

## 3. Consistent Permissions

Users with the same role receive the same access.

---

## 4. Improved Security

Reduces accidental permission assignments.

---

## 5. Widely Supported

Most enterprise systems and cloud platforms support RBAC.

---

# Disadvantages

## 1. Role Explosion

Large organizations may create hundreds of specialized roles.

---

## 2. Limited Flexibility

Complex business rules may not fit predefined roles.

---

## 3. Static Permissions

Roles may not adapt well to changing contexts such as location or time.

---

## 4. Maintenance

Roles require periodic review and updates.

---

## 5. Cross-Department Complexity

Users with responsibilities spanning multiple departments may require multiple roles.

---

# Real-World Examples

## AWS IAM

Permissions are assigned to IAM roles and attached to users or services.

---

## Kubernetes RBAC

Controls access to Kubernetes resources using roles and role bindings.

---

## GitHub Organizations

Users receive Owner, Maintainer, or Member roles.

---

## Enterprise Applications

Employees receive HR, Finance, or Administrator roles.

---

# When to Use

Use RBAC when:

- Managing many users.
- Permissions are role-based.
- Organizational responsibilities are well defined.
- Building enterprise applications.
- Securing cloud infrastructure.

---

# When NOT to Use

Avoid RBAC when:

- Access depends heavily on dynamic conditions such as time, location, device, or resource attributes.
- Highly granular, context-aware authorization is required.

---

# Comparison

| Feature | RBAC | ABAC |
|---|---|---|
| Access Based On | Roles | Attributes and Policies |
| Flexibility | Moderate | High |
| Administration | Simple | More Complex |
| Dynamic Decisions | Limited | Excellent |
| Enterprise Adoption | Very High | Growing |

---

# Interview Questions

## 1. What is RBAC?

An authorization model where permissions are assigned to roles, and users receive permissions through their assigned roles.

---

## 2. Why is RBAC widely used?

Because it simplifies permission management and scales well for organizations with many users.

---

## 3. What are the core RBAC components?

- User
- Role
- Permission
- Resource

---

## 4. What is Role Explosion?

The situation where an organization creates too many specialized roles, making RBAC difficult to manage.

---

## 5. Which systems commonly use RBAC?

- AWS IAM
- Kubernetes
- GitHub
- Enterprise identity management systems

---

# Key Takeaways

- RBAC assigns permissions to roles instead of individual users.
- Users inherit permissions from their assigned roles.
- RBAC simplifies administration and supports least privilege.
- It is one of the most widely adopted authorization models.
- For context-aware authorization, ABAC may be a better choice.

---

## Previous & Next

← Previous: [OpenID Connect (OIDC)](07-OpenID-Connect-OIDC.md)

→ Next: [Attribute-Based Access Control (ABAC)](09-Attribute-Based-Access-Control-ABAC.md)