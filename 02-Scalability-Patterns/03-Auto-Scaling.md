# Auto Scaling

## Introduction

Auto Scaling is a scalability pattern that automatically adjusts the number of computing resources based on application demand.

Instead of manually adding or removing servers, the system automatically scales resources up during high traffic and scales down during low traffic.

The main goals of Auto Scaling are:

- Handle traffic spikes.
- Maintain performance.
- Reduce infrastructure cost.
- Improve availability.

---

## Why was it Introduced?

Traditional systems required manual scaling.

Example:

```text
High Traffic

        |

Engineer observes load

        |

Manually adds servers
```

Problems:

- Slow response to traffic spikes.
- Over-provisioning resources.
- Higher infrastructure cost.
- Manual operational effort.

Auto Scaling was introduced to dynamically adjust resources based on real-time demand.

---

## Architecture Diagram

```text
                 Users

                   |

                   ▼

             Load Balancer

                   |

        ┌──────────┼──────────┐

        ▼          ▼          ▼

    Server 1   Server 2   Server 3


                   ▲

                   |

            Auto Scaling Group

                   |

          Monitoring Metrics

        (CPU, Memory, Requests)
```

Auto Scaling monitors system metrics and automatically changes the number of instances.

---

## How It Works

The basic flow:

```text
1. Application runs with multiple instances.

2. Monitoring system collects metrics.

3. Scaling policy evaluates conditions.

4. New instances are added or removed.

5. Load balancer distributes traffic.
```

Example:

```text
Normal Traffic

3 Servers


Traffic Spike

10 Servers


Traffic Reduced

3 Servers
```

---

# Types of Auto Scaling

## 1. Reactive Auto Scaling

Scaling happens after detecting increased demand.

Example:

```text
CPU > 80%

        |

Add More Servers
```

Advantages:

- Simple.
- Based on actual usage.

Disadvantages:

- Scaling happens after the load appears.

---

## 2. Predictive Auto Scaling

Scaling happens before demand increases based on historical patterns.

Example:

```text
Every Friday 8 PM

Traffic increases

        |

Add Servers Before Traffic Spike
```

Advantages:

- Faster response.
- Prevents performance issues.

Disadvantages:

- Requires accurate predictions.

---

## 3. Scheduled Scaling

Resources are adjusted based on predefined schedules.

Example:

```text
Office Hours

9 AM - 6 PM

Increase Servers


Night

Reduce Servers
```

Useful for predictable workloads.

---

# Scaling Policies

## 1. Target Tracking Policy

Maintains a target metric value.

Example:

```text
Maintain CPU utilization at 50%
```

If CPU increases:

```text
CPU = 80%

        |

Add Servers
```

---

## 2. Step Scaling

Scales based on different thresholds.

Example:

```text
CPU 60%

→ Add 2 Servers


CPU 90%

→ Add 10 Servers
```

---

## 3. Simple Scaling

Uses one condition and one action.

Example:

```text
CPU > 70%

→ Add One Server
```

---

# Core Characteristics

## 1. Dynamic Resource Allocation

Resources automatically increase or decrease based on demand.

---

## 2. Monitoring Driven

Scaling decisions depend on metrics.

Common metrics:

- CPU utilization.
- Memory usage.
- Request count.
- Network traffic.
- Queue length.

---

## 3. Integration With Load Balancers

New instances automatically join the traffic pool.

Example:

```text
New Server Created

        |

Health Check

        |

Receive Traffic
```

---

## 4. Elasticity

The system adapts to changing workload.

Example:

```text
Morning:

5 Servers


Night:

2 Servers
```

---

## 5. Automated Recovery

Failed instances can automatically be replaced.

---

# Advantages

## 1. Handles Traffic Spikes

Automatically adds capacity during high demand.

---

## 2. Cost Optimization

Resources are reduced during low traffic periods.

---

## 3. Improved Availability

Failed instances can be replaced automatically.

---

## 4. Reduced Manual Operations

No need for engineers to manually manage servers.

---

## 5. Better User Experience

Maintains application performance during load changes.

---

# Disadvantages

## 1. Scaling Delay

New servers require time to start.

Known as:

- Startup time.
- Provisioning delay.

---

## 2. Incorrect Scaling Rules

Poor configuration can cause:

- Too many servers.
- Too few servers.

---

## 3. Increased Complexity

Requires managing:

- Metrics.
- Policies.
- Thresholds.

---

## 4. Cost Risk

Aggressive scaling can increase infrastructure expenses.

---

# Real-World Examples

## E-Commerce Platforms

During sales events:

```text
Normal Day

20 Servers


Flash Sale

500 Servers
```

---

## Streaming Platforms

During popular content releases:

```text
Traffic Increase

        |

Auto Scaling

        |

More Streaming Instances
```

---

## Cloud Applications

Common architecture:

```text
Users

 |

Load Balancer

 |

Auto Scaling Group

 |

Application Instances

 |

Database
```

---

# When to Use

Use Auto Scaling when:

- Traffic changes frequently.
- Application demand is unpredictable.
- High availability is required.
- Cloud infrastructure is used.
- Manual scaling is inefficient.

---

# When NOT to Use

Avoid Auto Scaling when:

- Workload is constant.
- Application cannot handle dynamic instances.
- Startup time is too high.
- Scaling rules are difficult to define.

---

# Comparison

| Feature | Manual Scaling | Auto Scaling |
|---|---|---|
| Resource Management | Human controlled | Automatic |
| Response Time | Slow | Fast |
| Cost Efficiency | Lower | Higher |
| Operational Effort | High | Low |
| Traffic Handling | Limited | Better |

---

# Interview Questions

## 1. What is Auto Scaling?

Auto Scaling automatically increases or decreases application resources based on workload demand.

---

## 2. Difference between Scaling and Auto Scaling?

Scaling is the process of increasing capacity.

Auto Scaling automates this process based on predefined rules.

---

## 3. What metrics are used for Auto Scaling?

Common metrics:

- CPU utilization.
- Memory usage.
- Request count.
- Network traffic.
- Queue depth.

---

## 4. What is the difference between horizontal scaling and Auto Scaling?

Horizontal scaling adds more machines.

Auto Scaling automatically decides when and how many machines to add or remove.

---

## 5. What happens when traffic decreases?

Auto Scaling removes unnecessary instances to reduce infrastructure cost.

---

# Key Takeaways

- Auto Scaling automatically manages application capacity.
- It helps systems handle unpredictable traffic.
- It works together with load balancers.
- Scaling can be reactive, predictive, or scheduled.
- Proper scaling policies are important for cost and performance.
- It is a key pattern in cloud-native systems.

---

## Previous & Next

← Previous: [Load Balancing](02-Load-Balancing.md)

→ Next: [Caching](04-Caching.md)