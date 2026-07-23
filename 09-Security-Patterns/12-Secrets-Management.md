# Secrets Management

## Introduction

Secrets Management is a security pattern that **securely stores, controls, rotates, and provides access to sensitive credentials used by applications, services, and infrastructure**.

A **secret** is any sensitive information that must remain confidential.

Examples include:

- API Keys
- Database passwords
- Encryption keys
- OAuth client secrets
- TLS private keys
- Access tokens

Secrets Management answers the question:

> **"How do we securely store and access sensitive credentials?"**

The main goals of Secrets Management are:

- Protect sensitive credentials.
- Eliminate hardcoded secrets.
- Enable automatic rotation.
- Provide secure access control.
- Improve auditing and compliance.

---

## Why was it Introduced?

Imagine a developer storing a database password directly in source code.

```text
config.js

↓

password = "MyPassword123"
```

If the code is pushed to a public repository, the password is exposed.

Instead:

```text
Application

↓

Secrets Manager

↓

Database Password

↓

Database
```

The application retrieves the secret securely at runtime.

---

## Architecture Diagram

```text
          Application

               |

      Request Secret

               |

               ▼

      Secrets Manager

               |

      Authenticate Client

               |

      Return Secret

               |

               ▼

        Protected Resource
```

The application never stores secrets directly in its source code.

---

## How It Works

The secret retrieval flow:

```text
1. Application authenticates.

2. Application requests a secret.

3. Secrets Manager verifies identity.

4. Secret is returned securely.

5. Application uses the secret.

6. Secret can be rotated without changing application code.
```

---

# Common Types of Secrets

## Credentials

Examples:

- Database passwords
- Service account passwords
- LDAP credentials

---

## API Credentials

Examples:

- API Keys
- OAuth Client Secrets
- Access Tokens

---

## Encryption Material

Examples:

- Private keys
- Encryption keys
- TLS certificates

---

## Cloud Credentials

Examples:

- AWS Access Keys
- Azure Service Principals
- Google Cloud Service Account Keys

---

# Secret Rotation

Secrets should not remain unchanged indefinitely.

Automatic rotation:

```text
Old Secret

↓

Generate New Secret

↓

Update Target System

↓

Application Retrieves New Secret
```

Rotation minimizes the impact of credential compromise.

---

# Core Characteristics

## 1. Centralized Storage

Secrets are stored in a dedicated secure service.

---

## 2. Strong Access Control

Only authorized applications or users can retrieve secrets.

---

## 3. Encryption

Secrets are encrypted both at rest and in transit.

---

## 4. Auditing

Secret access is logged for monitoring and compliance.

---

## 5. Automatic Rotation

Secrets can be updated without modifying application code.

---

# Advantages

## 1. Improved Security

Sensitive credentials are removed from source code and configuration files.

---

## 2. Easier Credential Rotation

Secrets can be replaced automatically.

---

## 3. Centralized Management

All secrets are managed from a single secure location.

---

## 4. Better Compliance

Supports auditing and regulatory requirements.

---

## 5. Reduced Human Error

Developers do not manually distribute credentials.

---

# Disadvantages

## 1. Additional Infrastructure

Requires deployment or use of a secrets management service.

---

## 2. Service Dependency

Applications depend on the availability of the secrets manager.

---

## 3. Configuration Complexity

Authentication, authorization, and access policies require careful configuration.

---

## 4. Initial Setup Cost

Migrating existing applications may require significant effort.

---

## 5. Operational Overhead

Secret rotation policies and access controls require ongoing maintenance.

---

# Best Practices

- Never hardcode secrets in source code.
- Store secrets in a dedicated secrets manager.
- Rotate secrets regularly.
- Grant only the minimum required access.
- Audit secret usage.
- Use short-lived credentials whenever possible.

---

# Real-World Examples

## AWS Secrets Manager

Stores and rotates application secrets.

---

## AWS Systems Manager Parameter Store

Stores configuration values and secure parameters.

---

## HashiCorp Vault

Provides centralized secrets management and dynamic credentials.

---

## Azure Key Vault

Stores secrets, certificates, and encryption keys.

---

## Google Secret Manager

Manages secrets for Google Cloud applications.

---

# When to Use

Use Secrets Management when:

- Managing production credentials.
- Protecting API keys.
- Securing database passwords.
- Managing encryption keys.
- Running cloud-native applications.

---

# When NOT to Use

Avoid storing secrets manually in:

- Source code
- Git repositories
- Configuration files
- Docker images
- Client-side applications

Secrets should instead be managed through a dedicated secrets management solution.

---

# Comparison

| Feature | Environment Variables | Secrets Manager |
|---|---|---|
| Centralized Storage | No | Yes |
| Encryption | Limited | Yes |
| Rotation | Manual | Automatic |
| Access Control | Limited | Fine-Grained |
| Auditing | Minimal | Comprehensive |

---

# Interview Questions

## 1. What is Secrets Management?

A security practice that securely stores, controls, and provides access to sensitive credentials.

---

## 2. Why should secrets never be hardcoded?

Because source code can be leaked, shared, or committed to version control, exposing sensitive credentials.

---

## 3. What types of data are considered secrets?

- API Keys
- Database passwords
- Encryption keys
- OAuth client secrets
- Access tokens
- Private keys

---

## 4. Why is automatic secret rotation important?

It limits the lifetime of compromised credentials and reduces security risks.

---

## 5. Which systems commonly provide secrets management?

- AWS Secrets Manager
- AWS Systems Manager Parameter Store
- HashiCorp Vault
- Azure Key Vault
- Google Secret Manager

---

# Key Takeaways

- Secrets Management protects sensitive credentials throughout their lifecycle.
- Secrets should never be stored in source code or repositories.
- Centralized storage, encryption, auditing, and rotation improve security.
- Modern cloud platforms provide managed secrets management services.
- Secrets Management is a foundational practice for securing cloud-native and distributed applications.

---

## Previous & Next

← Previous: [Encryption in Transit](11-Encryption-in-Transit.md)

→ Next: [Zero Trust Architecture](13-Zero-Trust-Architecture.md)