# Rolling Deployment

## Introduction

Rolling Deployment is a deployment pattern that **gradually replaces instances of the current application with instances of the new version**, allowing the application to remain available throughout the deployment process.

Instead of stopping the entire application, updates are performed incrementally, one instance (or a small batch of instances) at a time.

The main goals of Rolling Deployment are:

- Minimize or eliminate downtime.
- Reduce deployment risk.
- Maintain application availability.
- Support gradual production updates.

---

## Why was it Introduced?

Recreate Deployment causes downtime because all application instances are stopped before deploying the new version.

Rolling Deployment solves this problem by updating instances incrementally.

Instead of:

```text
Stop All Servers

↓

Deploy New Version

↓

Start All Servers
```

Rolling Deployment performs:

```text
Replace Server 1

↓

Replace Server 2

↓

Replace Server 3
```

The application remains available during the entire deployment.

---

## Architecture Diagram

### Before Deployment

```text
             Load Balancer

                   |

      -------------------------

      |           |           |

      ▼           ▼           ▼

    V1 App      V1 App      V1 App
```

---

### During Deployment

```text
             Load Balancer

                   |

      -------------------------

      |           |           |

      ▼           ▼           ▼

    V2 App      V1 App      V1 App
```

Traffic continues to be served while instances are updated.

---

### After Deployment

```text
             Load Balancer

                   |

      -------------------------

      |           |           |

      ▼           ▼           ▼

    V2 App      V2 App      V2 App
```

All instances now run the new version.

---

## How It Works

The deployment flow:

```text
1. Remove one application instance from service.

2. Deploy the new version.

3. Verify the instance is healthy.

4. Return the instance to the load balancer.

5. Repeat until all instances are updated.
```

Example:

```text
V1 V1 V1

↓

V2 V1 V1

↓

V2 V2 V1

↓

V2 V2 V2
```

---

# Core Characteristics

## 1. Incremental Updates

Instances are replaced gradually rather than all at once.

---

## 2. Continuous Availability

The application remains available during deployment.

---

## 3. Load Balancer Integration

Traffic is routed only to healthy instances.

---

## 4. Health Checks

Each updated instance is validated before receiving traffic.

---

## 5. Gradual Rollout

Failures can often be detected before every instance is updated.

---

# Advantages

## 1. Minimal Downtime

Users can continue using the application throughout deployment.

---

## 2. Lower Deployment Risk

Problems may be detected after updating only a subset of instances.

---

## 3. Efficient Resource Usage

No duplicate production environment is required.

---

## 4. Widely Supported

Supported by platforms such as Kubernetes, Amazon ECS, and many cloud providers.

---

## 5. Continuous Delivery Friendly

Enables frequent deployments with reduced operational impact.

---

# Disadvantages

## 1. Multiple Versions Run Simultaneously

Old and new versions coexist during deployment.

---

## 2. Compatibility Requirements

The new version should remain compatible with the old version while both are running.

---

## 3. Slower Deployment

Updating instances sequentially takes longer than replacing everything at once.

---

## 4. Rollback Complexity

Some instances may already be running the new version when a rollback begins.

---

## 5. Session Handling

Applications using local session state may require sticky sessions or shared session storage.

---

# Real-World Examples

## Kubernetes

Rolling updates are the default deployment strategy for Deployments.

---

## Amazon ECS

Tasks are gradually replaced while maintaining the desired number of running tasks.

---

## Web Applications

Application servers behind a load balancer are updated one at a time.

---

## Enterprise Platforms

Business applications are upgraded gradually to maintain availability.

---

# When to Use

Use Rolling Deployment when:

- High availability is required.
- Downtime must be minimized.
- Multiple application instances are available.
- Gradual production updates are acceptable.

---

# When NOT to Use

Avoid Rolling Deployment when:

- The new version is incompatible with the old version.
- Major database changes require all instances to switch simultaneously.
- Complete isolation between versions is required.

---

# Comparison

| Feature | Recreate Deployment | Rolling Deployment |
|---|---|---|
| Downtime | Yes | No (or Minimal) |
| Active Versions | One | Multiple During Deployment |
| Infrastructure Cost | Low | Moderate |
| Deployment Risk | Higher | Lower |
| High Availability | No | Yes |

---

# Interview Questions

## 1. What is Rolling Deployment?

A deployment strategy that gradually replaces old application instances with new ones while keeping the application available.

---

## 2. Why is Rolling Deployment better than Recreate Deployment?

It minimizes downtime and reduces deployment risk by updating instances incrementally.

---

## 3. Why is a Load Balancer important in Rolling Deployment?

It routes traffic only to healthy instances while updates are in progress.

---

## 4. What is one challenge of Rolling Deployment?

Old and new versions run simultaneously, so backward compatibility is often required.

---

## 5. Which platforms commonly support Rolling Deployment?

- Kubernetes
- Amazon ECS
- Azure Kubernetes Service (AKS)
- Google Kubernetes Engine (GKE)

---

# Key Takeaways

- Rolling Deployment updates applications incrementally.
- The application remains available during deployment.
- Load balancers and health checks are essential.
- Multiple versions temporarily coexist.
- It is one of the most common deployment strategies in cloud-native environments.

---

## Previous & Next

← Previous: [Recreate Deployment](01-Recreate-Deployment.md)

→ Next: [Blue-Green Deployment](03-Blue-Green-Deployment.md)