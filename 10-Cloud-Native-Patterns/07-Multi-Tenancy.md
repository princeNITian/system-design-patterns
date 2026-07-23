# Multi-Tenancy

## Introduction

Multi-Tenancy is a cloud-native architectural pattern where **a single application instance serves multiple customers (tenants) while keeping each tenant's data and configuration logically isolated**.

A **tenant** is an individual customer, organization, or business using the application.

Instead of deploying a separate application for every customer, multiple tenants share the same infrastructure.

Multi-Tenancy answers the question:

> **"How can one application securely serve multiple customers?"**

The main goals of Multi-Tenancy are:

- Maximize infrastructure utilization.
- Reduce operational costs.
- Simplify deployments.
- Scale efficiently.
- Maintain tenant isolation.

---

# Why was it Introduced?

Imagine a SaaS company with 10,000 customers.

Without Multi-Tenancy:

```text
Customer A

↓

Dedicated Server

----------------

Customer B

↓

Dedicated Server

----------------

Customer C

↓

Dedicated Server
```

This requires thousands of application deployments.

With Multi-Tenancy:

```text
Customers

↓

Shared Application

↓

Tenant Isolation

↓

Shared Infrastructure
```

A single deployment serves all customers while keeping their data isolated.

---

# Architecture Diagram

```text
          Tenant A

               |

          Tenant B

               |

          Tenant C

               |

               ▼

      Shared Application

               |

      Tenant Identification

               |

               ▼

        Shared Database

      (Tenant Isolation)
```

Each request is associated with a tenant, and access is restricted to that tenant's data.

---

# How It Works

The workflow:

```text
1. Tenant authenticates.

2. Application identifies the tenant.

3. Tenant context is attached to the request.

4. Data access is filtered by tenant.

5. Only tenant-specific data is returned.
```

---

# Multi-Tenancy Models

## 1. Shared Database, Shared Schema

All tenants share the same tables.

Example:

```text
Orders

------------------------

tenant_id

order_id

amount
```

Each row belongs to a tenant.

### Advantages

- Lowest infrastructure cost.
- Easy to scale.
- Simple deployment.

### Disadvantages

- Strong isolation must be enforced in application logic.
- Noisy neighbors can affect performance.

---

## 2. Shared Database, Separate Schemas

Each tenant has its own database schema.

```text
Database

↓

Tenant_A Schema

Tenant_B Schema

Tenant_C Schema
```

### Advantages

- Better isolation.
- Easier tenant-specific customization.

### Disadvantages

- Schema management becomes more complex.

---

## 3. Separate Databases

Each tenant receives a dedicated database.

```text
Tenant A

↓

Database A

----------------

Tenant B

↓

Database B
```

### Advantages

- Strong isolation.
- Easier compliance.
- Independent backups and restores.

### Disadvantages

- Higher infrastructure cost.
- More operational overhead.

---

# Tenant Isolation

Isolation ensures that tenants cannot access each other's data.

Common techniques include:

- Tenant IDs
- Row-level security
- Separate schemas
- Separate databases
- Access control policies

---

# Core Characteristics

## 1. Shared Infrastructure

Multiple tenants share compute and networking resources.

---

## 2. Logical Isolation

Each tenant's data remains isolated.

---

## 3. Resource Efficiency

Infrastructure is utilized more effectively than single-tenant deployments.

---

## 4. Scalable

Supports thousands or even millions of tenants.

---

## 5. Configurable

Applications can support tenant-specific branding, settings, or features.

---

# Advantages

## 1. Lower Costs

Infrastructure is shared across many customers.

---

## 2. Easier Maintenance

A single deployment can serve all tenants.

---

## 3. Simplified Upgrades

Application updates benefit every tenant simultaneously.

---

## 4. Better Resource Utilization

Compute and storage resources are used more efficiently.

---

## 5. Cloud-Native Friendly

Well suited for SaaS platforms and modern cloud architectures.

---

# Disadvantages

## 1. Tenant Isolation Complexity

Incorrect implementation can expose one tenant's data to another.

---

## 2. Noisy Neighbor Problem

One tenant's heavy workload may affect others.

---

## 3. Customization Challenges

Supporting tenant-specific features increases complexity.

---

## 4. Security Risks

Strong authentication and authorization are essential.

---

## 5. Migration Complexity

Moving tenants between isolation models can be challenging.

---

# Real-World Examples

## Salesforce

Serves many organizations from a shared platform with logical tenant isolation.

---

## Microsoft 365

Hosts multiple organizations on shared infrastructure.

---

## Shopify

Supports millions of online stores using a multi-tenant architecture.

---

## Slack

Multiple organizations use the same platform while maintaining isolated workspaces.

---

## GitHub

Hosts repositories for millions of users and organizations on shared infrastructure.

---

# When to Use

Use Multi-Tenancy when:

- Building SaaS platforms.
- Serving many customers from a shared application.
- Optimizing infrastructure costs.
- Supporting rapid customer onboarding.
- Managing centralized application deployments.

---

# When NOT to Use

Avoid Multi-Tenancy when:

- Regulatory or contractual requirements demand complete physical isolation.
- Every customer requires extensive infrastructure customization.
- Strong isolation is more important than operational efficiency.

---

# Comparison

| Feature | Single-Tenant | Multi-Tenant |
|---|---|---|
| Infrastructure | Dedicated | Shared |
| Cost | Higher | Lower |
| Isolation | Strong | Logical (or Physical, depending on model) |
| Maintenance | Per Customer | Centralized |
| Scalability | Limited | High |

---

# Interview Questions

## 1. What is Multi-Tenancy?

An architectural pattern where one application instance serves multiple customers while keeping their data logically isolated.

---

## 2. What is a tenant?

A customer, organization, or business that uses a shared application.

---

## 3. What are the three common Multi-Tenancy models?

- Shared Database, Shared Schema
- Shared Database, Separate Schemas
- Separate Databases

---

## 4. What is the noisy neighbor problem?

A situation where one tenant's heavy resource usage negatively impacts the performance of other tenants sharing the same infrastructure.

---

## 5. Why is tenant isolation important?

It ensures that one tenant cannot access or modify another tenant's data or resources.

---

# Key Takeaways

- Multi-Tenancy enables a single application to serve multiple customers efficiently.
- Tenant isolation is the foundation of secure multi-tenant architectures.
- Different isolation models offer different trade-offs between cost, scalability, and security.
- Multi-Tenancy is widely used in SaaS platforms.
- Proper authentication, authorization, and data isolation are critical for secure implementations.

---

## Previous & Next

← Previous: [Autoscaling](06-Autoscaling.md)

→ Next: [Serverless Pattern](08-Serverless-Pattern.md)