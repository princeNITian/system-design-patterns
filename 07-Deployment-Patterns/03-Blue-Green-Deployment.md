# Blue-Green Deployment

## Introduction

Blue-Green Deployment is a deployment pattern that **maintains two identical production environments and switches traffic from the old version to the new version when the new deployment is ready**.

One environment (Blue) serves live traffic, while the other environment (Green) hosts the new application version. After validation, traffic is switched from Blue to Green with minimal downtime.

The main goals of Blue-Green Deployment are:

- Achieve near zero-downtime deployments.
- Enable fast rollbacks.
- Reduce deployment risk.
- Validate new releases before exposing them to users.

---

## Why was it Introduced?

Rolling Deployment gradually updates servers, meaning old and new versions run simultaneously.

Some applications require:

- Instant deployment.
- Instant rollback.
- Complete environment isolation.

Blue-Green Deployment addresses these requirements by keeping two complete production environments.

---

## Architecture Diagram

### Before Deployment

```text
                 Clients

                    |

                    ▼

             Load Balancer

              /           \

             ▼             ▼

      Blue Environment   Green Environment

        Version 1         Idle
```

Blue serves all production traffic.

---

### During Deployment

```text
                 Clients

                    |

                    ▼

             Load Balancer

              /           \

             ▼             ▼

      Blue Environment   Green Environment

        Version 1         Version 2
```

Green is deployed and tested without serving production traffic.

---

### After Deployment

```text
                 Clients

                    |

                    ▼

             Load Balancer

              /           \

             ▼             ▼

      Blue Environment   Green Environment

          Idle           Version 2
```

Traffic is switched entirely to Green.

---

## How It Works

The deployment flow:

```text
1. Blue serves production traffic.

2. Deploy the new version to Green.

3. Validate Green.

4. Switch the load balancer.

5. Green becomes production.

6. Blue remains available for rollback.
```

Example:

```text
Blue (V1)

↓

Deploy V2 to Green

↓

Test Green

↓

Switch Traffic

↓

Green (V2)
```

---

# Core Characteristics

## 1. Two Production Environments

Blue and Green are identical infrastructure environments.

---

## 2. Traffic Switching

The load balancer directs all traffic to one environment at a time.

---

## 3. Near Zero Downtime

Traffic switches almost instantly after validation.

---

## 4. Fast Rollback

Traffic can be redirected back to the previous environment if necessary.

---

## 5. Environment Isolation

The new version is fully tested before receiving production traffic.

---

# Advantages

## 1. Near Zero Downtime

Users experience little or no service interruption.

---

## 2. Instant Rollback

Switching traffic back to the previous environment is fast.

---

## 3. Safer Deployments

The new version can be validated before release.

---

## 4. Reduced Deployment Risk

Production traffic is exposed only after successful verification.

---

## 5. Simple Rollback Process

No application redeployment is required for rollback.

---

# Disadvantages

## 1. Higher Infrastructure Cost

Two complete production environments must be maintained.

---

## 2. Database Challenges

Database schema changes may require additional migration strategies.

---

## 3. Resource Duplication

Idle infrastructure consumes compute resources.

---

## 4. Operational Complexity

Managing identical environments requires careful synchronization.

---

## 5. Environment Drift

Configuration differences between Blue and Green can cause unexpected behavior.

---

# Real-World Examples

## E-Commerce

Deploy a new shopping application version while customers continue using the current version.

---

## Banking

Release new services with the ability to immediately revert if issues occur.

---

## SaaS Platforms

Deploy updates with minimal disruption to customers.

---

## Kubernetes

Maintain two deployments and switch traffic using Services or Ingress controllers.

---

# When to Use

Use Blue-Green Deployment when:

- Near zero downtime is required.
- Fast rollback is important.
- Infrastructure cost is acceptable.
- Production releases require thorough validation.

---

# When NOT to Use

Avoid Blue-Green Deployment when:

- Infrastructure resources are limited.
- Maintaining duplicate environments is too expensive.
- Small applications do not justify the additional operational overhead.

---

# Comparison

| Feature | Rolling Deployment | Blue-Green Deployment |
|---|---|---|
| Downtime | No (or Minimal) | Near Zero |
| Active Environments | One | Two |
| Rollback Speed | Moderate | Very Fast |
| Infrastructure Cost | Moderate | High |
| Deployment Risk | Low | Very Low |

---

# Interview Questions

## 1. What is Blue-Green Deployment?

A deployment strategy that maintains two production environments and switches traffic between them.

---

## 2. Why is Blue-Green Deployment popular?

It enables near zero-downtime deployments and very fast rollbacks.

---

## 3. Why are two environments required?

One environment serves production traffic while the other hosts and validates the new release.

---

## 4. What is the biggest disadvantage of Blue-Green Deployment?

The cost of maintaining duplicate production infrastructure.

---

## 5. How is rollback performed?

By switching the load balancer back to the previous environment.

---

# Key Takeaways

- Blue-Green Deployment uses two identical production environments.
- Traffic switches instantly after validation.
- Rollbacks are fast and straightforward.
- Infrastructure costs are higher due to duplicate environments.
- It is widely used for high-availability production systems.

---

## Previous & Next

← Previous: [Rolling Deployment](02-Rolling-Deployment.md)

→ Next: [Canary Deployment](04-Canary-Deployment.md)