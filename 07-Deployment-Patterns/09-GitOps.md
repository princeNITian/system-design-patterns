# GitOps

## Introduction

GitOps is a deployment pattern in which **Git serves as the single source of truth for infrastructure and application deployments**.

Instead of manually deploying changes, developers commit updates to a Git repository. Automated agents continuously monitor the repository and reconcile the actual infrastructure with the desired state defined in Git.

The main goals of GitOps are:

- Automate deployments.
- Improve deployment consistency.
- Enable version-controlled infrastructure.
- Simplify auditing and rollback.

---

## Why was it Introduced?

Traditional deployments often involve manual commands.

Example:

```text
Developer

      |

SSH into Server

      |

Run Deployment Commands

      |

Production Updated
```

Problems include:

- Human error.
- Difficult auditing.
- Inconsistent deployments.
- Manual rollback procedures.

GitOps replaces manual deployments with automated synchronization from Git.

---

## Architecture Diagram

```text
            Developer

                 |

            Git Commit

                 |

                 ▼

          Git Repository

                 |

      GitOps Controller

     (Argo CD / Flux)

                 |

                 ▼

          Kubernetes Cluster

                 |

          Desired State
```

The GitOps controller continuously ensures the cluster matches the repository.

---

## How It Works

The deployment flow:

```text
1. Developer updates configuration.

2. Changes are committed to Git.

3. GitOps controller detects the commit.

4. Controller compares desired and actual state.

5. Differences are reconciled automatically.

6. Infrastructure reaches the desired state.
```

Example:

```text
Git Commit

      |

Argo CD Detects Change

      |

Deploy New Version

      |

Cluster Updated
```

---

# Core Components

## 1. Git Repository

Stores application manifests and infrastructure definitions.

---

## 2. Desired State

The repository defines the intended system configuration.

---

## 3. GitOps Controller

Continuously synchronizes infrastructure with Git.

Examples:

- Argo CD
- Flux

---

## 4. Continuous Reconciliation

Infrastructure is automatically corrected if it drifts from the desired state.

---

## 5. Infrastructure as Code

Infrastructure definitions are maintained as version-controlled code.

---

# Core Characteristics

## 1. Git as the Source of Truth

All desired infrastructure changes originate from Git.

---

## 2. Declarative Configuration

Infrastructure is defined declaratively rather than through manual commands.

---

## 3. Automated Synchronization

Controllers continuously apply repository changes.

---

## 4. Version Control

Every deployment is tracked through Git history.

---

## 5. Continuous Reconciliation

Unexpected infrastructure changes are automatically corrected.

---

# Advantages

## 1. Fully Auditable Deployments

Every change is recorded in Git.

---

## 2. Simplified Rollback

Rollback is performed by reverting Git commits.

---

## 3. Consistent Deployments

Production environments remain synchronized with version-controlled configuration.

---

## 4. Reduced Human Error

Manual production deployments are minimized.

---

## 5. Excellent Automation

Git integrates naturally with CI/CD pipelines.

---

# Disadvantages

## 1. Learning Curve

Teams must understand GitOps workflows and declarative infrastructure.

---

## 2. Additional Components

GitOps controllers introduce extra operational infrastructure.

---

## 3. Git Dependency

Deployment availability depends on repository accessibility and management.

---

## 4. Configuration Management

Large repositories require careful organization and governance.

---

## 5. Not Ideal for Manual Changes

Direct production modifications are overwritten during reconciliation.

---

# Real-World Examples

## Kubernetes

Applications are deployed automatically using GitOps controllers.

---

## Argo CD

Continuously synchronizes Kubernetes clusters with Git repositories.

---

## Flux

Monitors Git repositories and reconciles cluster state.

---

## Cloud-Native Platforms

Infrastructure and application configurations are managed entirely through Git.

---

# When to Use

Use GitOps when:

- Managing Kubernetes clusters.
- Practicing Infrastructure as Code.
- Automating deployments.
- Maintaining declarative infrastructure.

---

# When NOT to Use

Avoid GitOps when:

- Infrastructure changes are primarily manual.
- Small projects do not justify GitOps tooling.
- Teams are not using version-controlled infrastructure.

---

# Comparison

| Feature | Traditional Deployment | GitOps |
|---|---|---|
| Source of Truth | Deployment Scripts | Git Repository |
| Deployment Trigger | Manual or CI/CD | Git Commit |
| Rollback | Manual | Git Revert |
| Auditability | Limited | Excellent |
| Drift Detection | Manual | Automatic |

---

# Interview Questions

## 1. What is GitOps?

A deployment pattern where Git acts as the single source of truth and automated controllers synchronize infrastructure with the repository.

---

## 2. Why is GitOps important?

It automates deployments, improves consistency, and provides complete deployment history through Git.

---

## 3. What is continuous reconciliation?

The process of continuously comparing the desired state in Git with the actual infrastructure and automatically correcting differences.

---

## 4. What are popular GitOps tools?

- Argo CD
- Flux

---

## 5. How is rollback performed in GitOps?

By reverting the relevant Git commit, allowing the GitOps controller to synchronize the infrastructure back to the previous state.

---

# Key Takeaways

- Git is the single source of truth in GitOps.
- Infrastructure is managed declaratively using version-controlled configuration.
- Automated controllers continuously reconcile infrastructure with Git.
- Rollbacks are simple because deployment history is preserved in Git.
- GitOps is a foundational deployment model for Kubernetes and cloud-native platforms.

---

## Previous & Next

← Previous: [Immutable Infrastructure](08-Immutable-Infrastructure.md)

→ Next Module: [08-Distributed-System-Patterns](../08-Distributed-System-Patterns/README.md)