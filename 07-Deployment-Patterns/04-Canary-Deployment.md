# Canary Deployment

## Introduction

Canary Deployment is a deployment pattern that **gradually releases a new application version to a small percentage of users before making it available to everyone**.

Instead of switching all traffic to the new version at once, traffic is shifted incrementally while monitoring the application's health and performance.

The main goals of Canary Deployment are:

- Reduce deployment risk.
- Detect issues early.
- Minimize user impact.
- Enable controlled production rollouts.

---

## Why was it Introduced?

Even after extensive testing, problems may only appear under real production traffic.

Deploying a new version to every user immediately can lead to:

- Large-scale outages.
- Performance degradation.
- Business impact.
- Difficult rollbacks.

Canary Deployment limits the blast radius by exposing only a small group of users to the new version first.

---

## Architecture Diagram

### Initial State

```text
                 Clients

                    |

                    ▼

             Load Balancer

                    |

        ----------------------

        |                    |

        ▼                    ▼

      V1 (100%)          V2 (0%)
```

---

### First Canary Release

```text
                 Clients

                    |

                    ▼

             Load Balancer

        95%          5%

        ▼             ▼

      V1            V2
```

Only a small percentage of traffic reaches Version 2.

---

### Full Rollout

```text
                 Clients

                    |

                    ▼

             Load Balancer

                    |

        ----------------------

        |                    |

        ▼                    ▼

      V1 (0%)          V2 (100%)
```

All users now use the new version.

---

## How It Works

The deployment flow:

```text
1. Deploy Version 2.

2. Route a small percentage of traffic.

3. Monitor application health.

4. Increase traffic gradually.

5. Continue monitoring.

6. Shift all traffic to Version 2.
```

Example rollout:

```text
5%

↓

10%

↓

25%

↓

50%

↓

100%
```

If problems occur:

```text
Version 2

↓

Rollback

↓

100% Traffic → Version 1
```

---

# Core Characteristics

## 1. Gradual Traffic Shifting

Traffic is increased in controlled stages.

---

## 2. Continuous Monitoring

Metrics are observed throughout the rollout.

---

## 3. Small Blast Radius

Only a subset of users is affected if problems occur.

---

## 4. Incremental Validation

The deployment proceeds only if the application remains healthy.

---

## 5. Fast Rollback

Traffic can quickly return to the previous version.

---

# Advantages

## 1. Lower Deployment Risk

Only a small percentage of users experience potential issues.

---

## 2. Production Validation

The new version is validated using real production traffic.

---

## 3. Better Observability

Performance metrics guide rollout decisions.

---

## 4. Controlled Rollout

Traffic percentages can be adjusted gradually.

---

## 5. Improved Reliability

Problems are detected before affecting all users.

---

# Disadvantages

## 1. More Complex Infrastructure

Traffic management and monitoring are required.

---

## 2. Multiple Versions Run Simultaneously

Old and new versions coexist during deployment.

---

## 3. Additional Monitoring

Comprehensive observability is essential.

---

## 4. Compatibility Requirements

Versions should remain compatible while both are active.

---

## 5. Longer Deployment Time

Incremental rollout takes longer than switching traffic all at once.

---

# Real-World Examples

## Netflix

Gradually releases new application versions to subsets of users.

---

## Google

Rolls out updates to a small percentage of production traffic before global deployment.

---

## Kubernetes

Canary deployments can be implemented using Service Meshes, Ingress controllers, or progressive delivery tools.

---

## E-Commerce

Expose new checkout functionality to a limited number of customers before a full release.

---

# When to Use

Use Canary Deployment when:

- Production stability is critical.
- Real-user validation is required.
- Applications serve large user bases.
- Rollback should be quick and low risk.

---

# When NOT to Use

Avoid Canary Deployment when:

- Applications have very few users.
- Infrastructure cannot support multiple versions.
- Monitoring capabilities are insufficient.

---

# Comparison

| Feature | Blue-Green Deployment | Canary Deployment |
|---|---|---|
| Traffic Shift | Instant | Gradual |
| Rollback | Very Fast | Very Fast |
| Monitoring Importance | Moderate | High |
| Deployment Risk | Very Low | Lowest |
| Infrastructure Complexity | Moderate | High |

---

# Interview Questions

## 1. What is Canary Deployment?

A deployment strategy that gradually routes production traffic to a new application version before full rollout.

---

## 2. Why is Canary Deployment safer than deploying to everyone at once?

Only a small percentage of users are exposed initially, reducing the impact of failures.

---

## 3. What metrics are commonly monitored during a Canary Deployment?

- Error rate
- Latency
- CPU usage
- Memory usage
- Request success rate

---

## 4. How is rollback performed?

Traffic is redirected back to the previous application version.

---

## 5. What is the main difference between Blue-Green and Canary Deployment?

Blue-Green switches all traffic at once, whereas Canary gradually increases traffic to the new version.

---

# Key Takeaways

- Canary Deployment gradually releases new versions to production.
- It minimizes deployment risk through controlled traffic shifting.
- Continuous monitoring is essential for successful rollouts.
- Rollbacks are quick because the previous version remains available.
- It is widely used by organizations operating large-scale production systems.

---

## Previous & Next

← Previous: [Blue-Green Deployment](03-Blue-Green-Deployment.md)

→ Next: [Shadow Deployment](05-Shadow-Deployment.md)