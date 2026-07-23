# Recreate Deployment

## Introduction

Recreate Deployment is the simplest deployment pattern in which **the existing version of an application is completely stopped before the new version is deployed**.

Only one version of the application runs at any given time.

The main goals of Recreate Deployment are:

- Simplify deployments.
- Ensure only one application version is active.
- Minimize deployment complexity.
- Reduce infrastructure requirements.

---

## Why was it Introduced?

In traditional deployments, applications were updated by replacing the existing version.

Example:

```text
Version 1

↓

Stop Application

↓

Deploy Version 2

↓

Start Application
```

This approach is simple but introduces downtime during the deployment process.

---

## Architecture Diagram

### Before Deployment

```text
          Clients

              |

              ▼

        Version 1

              |

              ▼

          Database
```

---

### During Deployment

```text
          Clients

              |

              ▼

        Application

          Stopped

              |

              ▼

          Database
```

Users experience downtime while the application is unavailable.

---

### After Deployment

```text
          Clients

              |

              ▼

        Version 2

              |

              ▼

          Database
```

Only the new version is running.

---

## How It Works

The deployment flow:

```text
1. Stop the current application.

2. Deploy the new version.

3. Start the application.

4. Route all traffic to the new version.
```

Example:

```text
Version 1 Running

        |

Stop Version 1

        |

Deploy Version 2

        |

Start Version 2
```

---

# Core Characteristics

## 1. Single Active Version

Only one version of the application runs at a time.

---

## 2. Downtime

The application is unavailable during deployment.

---

## 3. Simple Deployment Process

No traffic splitting or parallel environments are required.

---

## 4. Minimal Infrastructure

Only one deployment environment is needed.

---

## 5. Easy Rollback

Rollback requires redeploying the previous version.

---

# Advantages

## 1. Simple to Implement

Requires minimal deployment logic.

---

## 2. Low Infrastructure Cost

Only one application environment is maintained.

---

## 3. Easy to Understand

Deployment process is straightforward.

---

## 4. Suitable for Small Applications

Works well for internal tools and low-traffic systems.

---

## 5. Minimal Operational Overhead

No advanced deployment orchestration is required.

---

# Disadvantages

## 1. Downtime

Users cannot access the application during deployment.

---

## 2. Risky Deployments

If the new version fails, the application remains unavailable until rollback.

---

## 3. Slower Recovery

Rollback requires another deployment.

---

## 4. Poor User Experience

Maintenance windows may be required.

---

## 5. Not Ideal for High Availability

Unsuitable for systems requiring continuous uptime.

---

# Real-World Examples

## Internal Business Applications

Applications that can tolerate scheduled maintenance windows.

---

## Development Environments

Simple deployments during development and testing.

---

## Small Business Applications

Systems with low traffic and limited availability requirements.

---

## Legacy Applications

Older systems without support for advanced deployment strategies.

---

# When to Use

Use Recreate Deployment when:

- Downtime is acceptable.
- Infrastructure resources are limited.
- Applications are small or internal.
- Simplicity is the primary goal.

---

# When NOT to Use

Avoid Recreate Deployment when:

- High availability is required.
- Zero-downtime deployments are expected.
- Applications serve critical production workloads.
- Frequent deployments occur.

---

# Comparison

| Feature | Recreate Deployment | Rolling Deployment |
|---|---|---|
| Downtime | Yes | No (or Minimal) |
| Infrastructure Cost | Low | Moderate |
| Deployment Complexity | Low | Moderate |
| Rollback Speed | Slower | Faster |
| High Availability | No | Yes |

---

# Interview Questions

## 1. What is Recreate Deployment?

A deployment strategy where the existing application is stopped before the new version is deployed.

---

## 2. What is the biggest disadvantage of Recreate Deployment?

Application downtime during deployment.

---

## 3. Why is Recreate Deployment simple?

Only one application version exists, eliminating the need for traffic routing or multiple environments.

---

## 4. Is Recreate Deployment suitable for mission-critical applications?

No.

Mission-critical systems typically require deployment strategies with little or no downtime.

---

## 5. When is Recreate Deployment commonly used?

- Development environments.
- Internal tools.
- Small applications.
- Legacy systems.

---

# Key Takeaways

- Recreate Deployment completely replaces the running application.
- Only one version runs at any time.
- It is simple and inexpensive.
- Downtime is its primary drawback.
- It is best suited for applications where temporary unavailability is acceptable.

---

## Previous & Next

← Previous Module: [06-API-Design-Patterns](../06-API-Design-Patterns/README.md)

→ Next: [Rolling Deployment](02-Rolling-Deployment.md)