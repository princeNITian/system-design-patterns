# Zero Trust Architecture

## Introduction

Zero Trust Architecture (ZTA) is a security pattern based on the principle:

> **"Never Trust, Always Verify."**

Unlike traditional security models that trust users and devices once they are inside the corporate network, Zero Trust assumes that **no user, device, application, or network should be trusted by default**, regardless of its location.

Every request must be continuously authenticated, authorized, and validated.

The main goals of Zero Trust Architecture are:

- Eliminate implicit trust.
- Verify every access request.
- Minimize attack surfaces.
- Reduce lateral movement.
- Protect modern cloud-native and distributed systems.

---

## Why was it Introduced?

Traditional network security follows a perimeter-based approach.

```text
Internet

↓

Firewall

↓

Trusted Network
```

Once an attacker enters the internal network, they often gain broad access.

Zero Trust removes this assumption.

```text
User

↓

Verify Identity

↓

Verify Device

↓

Verify Context

↓

Grant Limited Access
```

Every request is evaluated independently.

---

## Architecture Diagram

```text
            User / Device

                  |

         Authentication

                  |

         Authorization

                  |

       Policy Engine

                  |

     Risk Evaluation

                  |

        Allow / Deny

                  |

                  ▼

      Protected Resource
```

Every access request passes through policy evaluation before reaching protected resources.

---

## How It Works

The access flow:

```text
1. User requests access.

2. Identity is authenticated.

3. Device posture is verified.

4. Context is evaluated.

5. Policies are applied.

6. Least privilege permissions are granted.

7. Continuous monitoring validates ongoing access.
```

---

# Core Principles

## 1. Never Trust

No request is automatically trusted.

---

## 2. Always Verify

Every access request is authenticated and authorized.

---

## 3. Least Privilege

Users receive only the minimum permissions necessary.

---

## 4. Assume Breach

Design systems under the assumption that attackers may already be inside the network.

---

## 5. Continuous Verification

Access is continuously evaluated throughout the session.

---

# Key Components

## 1. Identity Verification

Authenticate users using strong identity providers.

Examples:

- Multi-Factor Authentication (MFA)
- OpenID Connect (OIDC)
- SAML

---

## 2. Device Verification

Evaluate the security posture of the requesting device.

Examples:

- Operating system version
- Security patches
- Disk encryption
- Endpoint protection

---

## 3. Policy Engine

Makes authorization decisions based on:

- Identity
- Device
- Resource
- Risk
- Location
- Time

---

## 4. Continuous Monitoring

Detects suspicious behavior after access has been granted.

---

## 5. Micro-Segmentation

Divides infrastructure into smaller security zones to reduce lateral movement.

---

# Core Characteristics

## 1. Identity-Centric Security

Identity becomes the primary security boundary.

---

## 2. Continuous Authorization

Access is continuously re-evaluated.

---

## 3. Context Awareness

Authorization decisions consider environmental context.

---

## 4. Fine-Grained Access

Permissions are narrowly scoped to specific resources.

---

## 5. Cloud-Native Ready

Well suited for modern distributed systems and remote work environments.

---

# Advantages

## 1. Stronger Security

Eliminates implicit trust within internal networks.

---

## 2. Reduced Lateral Movement

Compromised accounts have limited access.

---

## 3. Better Protection for Remote Work

Security no longer depends on network location.

---

## 4. Improved Compliance

Supports modern regulatory and security frameworks.

---

## 5. Works Across Hybrid and Cloud Environments

Protects users and services regardless of where they are deployed.

---

# Disadvantages

## 1. Higher Implementation Complexity

Requires integration across identity, networking, devices, and policy systems.

---

## 2. Infrastructure Investment

Organizations may need new security tools and platforms.

---

## 3. Performance Overhead

Additional policy evaluations can introduce latency.

---

## 4. Operational Changes

Security teams must adopt new operational practices.

---

## 5. Migration Challenges

Transitioning from traditional perimeter security can be time-consuming.

---

# Real-World Examples

## Google BeyondCorp

One of the earliest large-scale Zero Trust implementations, enabling secure access without relying on a traditional corporate VPN.

---

## Microsoft Zero Trust

Applies identity, device, application, and data protection across Microsoft cloud services.

---

## AWS Zero Trust Guidance

Uses IAM, security groups, network segmentation, encryption, and continuous monitoring to implement Zero Trust principles.

---

## Cloudflare Zero Trust

Provides secure access to applications without exposing internal networks.

---

# When to Use

Use Zero Trust Architecture when:

- Building cloud-native applications.
- Supporting remote or hybrid workforces.
- Protecting sensitive enterprise systems.
- Designing microservices architectures.
- Securing multi-cloud or hybrid cloud environments.

---

# When NOT to Use

Zero Trust principles are broadly applicable. However, implementing a full Zero Trust Architecture may be unnecessary for very small, isolated systems with limited security requirements.

---

# Comparison

| Feature | Traditional Security | Zero Trust Architecture |
|---|---|---|
| Trust Model | Trust Internal Network | Trust No One by Default |
| Authentication | Often Once | Continuous |
| Authorization | Initial Access | Continuous Evaluation |
| Network Focus | Perimeter-Based | Identity-Based |
| Lateral Movement | Easier | Strongly Limited |

---

# Interview Questions

## 1. What is Zero Trust Architecture?

A security model based on the principle of "Never Trust, Always Verify," where every access request is authenticated, authorized, and continuously validated.

---

## 2. What is the core principle of Zero Trust?

No user, device, application, or network is trusted by default.

---

## 3. What is Micro-Segmentation?

The practice of dividing infrastructure into smaller security zones to limit lateral movement after a compromise.

---

## 4. Why is Identity central to Zero Trust?

Because access decisions are based on verified identities rather than network location.

---

## 5. Name companies known for Zero Trust implementations.

- Google (BeyondCorp)
- Microsoft
- AWS
- Cloudflare

---

# Key Takeaways

- Zero Trust replaces implicit trust with continuous verification.
- Every request is authenticated, authorized, and evaluated against security policies.
- Least privilege and micro-segmentation reduce attack impact.
- Identity becomes the new security perimeter.
- Zero Trust is a foundational security model for cloud-native, distributed, and remote-first environments.

---

## Previous & Next

← Previous: [Secrets Management](12-Secrets-Management.md)

→ Next Module: [10-Cloud-Native-Patterns](../10-Cloud-Native-Patterns/README.md)