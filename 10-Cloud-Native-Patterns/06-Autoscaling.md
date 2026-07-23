# Autoscaling

## Introduction

Autoscaling is a cloud-native pattern that **automatically increases or decreases application resources based on workload demand**.

Instead of manually provisioning infrastructure for peak traffic, autoscaling dynamically adjusts capacity to maintain performance while optimizing resource utilization and cost.

Autoscaling answers the question:

> **"How can applications automatically adapt to changing workloads?"**

The main goals of Autoscaling are:

- Maintain application performance.
- Optimize infrastructure costs.
- Improve availability.
- Handle unpredictable traffic spikes.
- Reduce manual operations.

---

# Why was it Introduced?

Imagine an e-commerce website during a flash sale.

Normal traffic:

```text
Users

↓

3 Application Instances
```

Flash sale:

```text
100x Users

↓

3 Application Instances

↓

Slow Response

↓

Failures
```

Autoscaling solves this problem.

```text
100x Users

↓

Autoscaler

↓

20 Application Instances
```

When traffic decreases, unnecessary instances are automatically removed.

---

# Architecture Diagram

```text
              Users

                |

        Load Balancer

                |

                ▼

          Autoscaler

                |

      +-------------------+

      |                   |

  Create Pods        Remove Pods

      |                   |

      ▼                   ▼

 Kubernetes Cluster (Pods)
```

The Autoscaler continuously adjusts the number of running instances.

---

# How It Works

The workflow:

```text
1. Monitoring system collects metrics.

2. Autoscaler evaluates scaling rules.

3. If demand increases:
      Create new instances.

4. If demand decreases:
      Remove excess instances.

5. Load balancer distributes traffic across available instances.
```

---

# Types of Autoscaling

## 1. Horizontal Scaling (Scale Out/In)

Adds or removes application instances.

Example:

```text
3 Pods

↓

Scale Out

↓

10 Pods
```

This is the most common cloud-native scaling approach.

---

## 2. Vertical Scaling (Scale Up/Down)

Changes the resources of an existing instance.

Example:

```text
2 CPU

↓

8 CPU
```

No additional instances are created.

---

## 3. Cluster Autoscaling

Automatically adds or removes worker nodes in a Kubernetes cluster.

Example:

```text
More Pods

↓

No Available Nodes

↓

Create New Node
```

---

# Common Scaling Metrics

## CPU Utilization

Example:

```text
CPU > 70%

↓

Scale Out
```

---

## Memory Utilization

Scale based on memory consumption.

---

## Request Rate

Scale based on incoming requests per second.

---

## Queue Length

Scale workers according to message queue depth.

---

## Custom Metrics

Examples:

- Active users
- Kafka lag
- Business transactions
- Response time

---

# Kubernetes Autoscaling

## Horizontal Pod Autoscaler (HPA)

Scales Pods based on CPU, memory, or custom metrics.

---

## Vertical Pod Autoscaler (VPA)

Adjusts CPU and memory requests for Pods.

---

## Cluster Autoscaler

Adds or removes worker nodes based on scheduling needs.

---

# Core Characteristics

## 1. Dynamic Scaling

Capacity changes automatically based on demand.

---

## 2. Metric-Driven

Scaling decisions rely on monitored metrics.

---

## 3. Elastic

Resources expand and shrink as needed.

---

## 4. Cost Efficient

Unused resources are automatically released.

---

## 5. High Availability

Maintains application performance during traffic spikes.

---

# Advantages

## 1. Better Availability

Applications remain responsive under varying workloads.

---

## 2. Lower Costs

Infrastructure is provisioned only when needed.

---

## 3. Reduced Manual Intervention

Scaling happens automatically.

---

## 4. Cloud-Native Ready

Works seamlessly with Kubernetes and cloud platforms.

---

## 5. Improved User Experience

Applications can maintain consistent response times during traffic increases.

---

# Disadvantages

## 1. Scaling Delay

Launching new instances may take several seconds or minutes.

---

## 2. Metric Selection

Poorly chosen metrics can lead to inefficient scaling.

---

## 3. Stateless Requirement

Horizontal scaling works best with stateless applications.

---

## 4. Resource Limits

Cloud quotas may restrict scaling capacity.

---

## 5. Increased Operational Complexity

Monitoring and scaling policies require careful tuning.

---

# Real-World Examples

## Kubernetes HPA

Automatically scales Pods using CPU, memory, or custom metrics.

---

## AWS Auto Scaling

Scales EC2 instances based on CloudWatch metrics.

---

## Google Cloud Managed Instance Groups

Automatically adjusts VM instances.

---

## Azure Virtual Machine Scale Sets

Provides automatic scaling for virtual machines.

---

## AWS Lambda

Automatically scales function invocations without manual configuration.

---

# When to Use

Use Autoscaling when:

- Traffic is unpredictable.
- Applications experience periodic spikes.
- Running cloud-native workloads.
- Optimizing infrastructure costs.
- Maintaining high availability.

---

# When NOT to Use

Avoid Autoscaling when:

- Running workloads with fixed, predictable capacity requirements.
- Applications cannot safely scale horizontally or vertically.
- Scaling delays are unacceptable for extremely latency-sensitive workloads without additional capacity planning.

---

# Comparison

| Feature | Horizontal Scaling | Vertical Scaling |
|---|---|---|
| Adds Instances | Yes | No |
| Increases CPU/Memory | No | Yes |
| Fault Tolerance | Higher | Lower |
| Maximum Capacity | Very High | Limited by Machine Size |
| Cloud-Native Preferred | Yes | Less Common |

---

# Interview Questions

## 1. What is Autoscaling?

A mechanism that automatically adjusts computing resources based on workload demand.

---

## 2. What is the difference between Horizontal and Vertical Scaling?

Horizontal Scaling adds or removes instances, while Vertical Scaling increases or decreases resources within an existing instance.

---

## 3. What is the Kubernetes HPA?

The Horizontal Pod Autoscaler automatically scales Pods using resource or custom metrics.

---

## 4. Which metrics are commonly used for Autoscaling?

- CPU utilization
- Memory utilization
- Request rate
- Queue length
- Custom business metrics

---

## 5. Why is Horizontal Scaling preferred for cloud-native applications?

Because it improves fault tolerance, elasticity, and scalability while aligning with stateless microservice architectures.

---

# Key Takeaways

- Autoscaling automatically adjusts infrastructure based on workload demand.
- Horizontal Scaling adds instances, while Vertical Scaling increases resources per instance.
- Kubernetes provides HPA, VPA, and Cluster Autoscaler for different scaling needs.
- Metric-driven scaling improves availability and optimizes infrastructure costs.
- Autoscaling is a core capability of modern cloud-native platforms.

---

## Previous & Next

← Previous: [Service Mesh](05-Service-Mesh.md)

→ Next: [Multi-Tenancy](07-Multi-Tenancy.md)