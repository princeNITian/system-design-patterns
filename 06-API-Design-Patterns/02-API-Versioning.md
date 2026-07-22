# API Versioning

## Introduction

API Versioning is an API design pattern that **allows an API to evolve without breaking existing clients**.

As applications grow, APIs need new features, improved response structures, or behavior changes. Versioning enables these changes while maintaining backward compatibility for existing consumers.

The main goals of API Versioning are:

- Maintain backward compatibility.
- Support API evolution.
- Prevent breaking changes.
- Allow multiple API versions to coexist.

---

## Why was it Introduced?

Consider an API:

```text
GET /users/101
```

Initial response:

```json
{
  "id": 101,
  "name": "Alice"
}
```

Later, the API changes to:

```json
{
  "userId": 101,
  "fullName": "Alice"
}
```

Existing applications expecting `id` and `name` will fail.

API Versioning allows both versions to exist.

---

## Architecture Diagram

```text
             Client

                |

                ▼

          API Gateway

          /          \

         ▼            ▼

      API v1       API v2

         |            |

         ▼            ▼

     Business Logic
```

Different clients can continue using different API versions.

---

## How It Works

The communication flow:

```text
1. Client requests a specific API version.

2. The server identifies the requested version.

3. The request is routed to the appropriate implementation.

4. The server returns the response for that version.

5. Older clients continue working without modification.
```

Example:

```text
GET /v1/users/101

        |

Version 1 Response
```

```text
GET /v2/users/101

        |

Version 2 Response
```

---

# Common Versioning Strategies

## 1. URI Versioning

Version is included in the URL.

Example:

```text
/v1/users

/v2/users
```

Most commonly used approach.

---

## 2. Query Parameter Versioning

Version is passed as a query parameter.

Example:

```text
/users?version=1
```

---

## 3. Header Versioning

Version is specified in an HTTP header.

Example:

```text
API-Version: 2
```

---

## 4. Media Type Versioning

Version is included in the `Accept` header.

Example:

```text
Accept: application/vnd.company.v2+json
```

---

# Core Characteristics

## 1. Backward Compatibility

Existing clients continue functioning after API updates.

---

## 2. Multiple Versions

Different API versions can run simultaneously.

---

## 3. Independent Evolution

New features can be introduced without affecting older clients.

---

## 4. Controlled Deprecation

Older versions can be retired gradually.

---

## 5. Flexible Client Migration

Clients upgrade at their own pace.

---

# Advantages

## 1. Prevents Breaking Changes

Existing integrations continue working.

---

## 2. Supports Continuous Evolution

New features can be added safely.

---

## 3. Easier Client Migration

Consumers can upgrade when ready.

---

## 4. Better Stability

Production systems remain compatible during upgrades.

---

## 5. Industry Standard

Widely adopted in public and enterprise APIs.

---

# Disadvantages

## 1. Increased Maintenance

Multiple API versions require ongoing support.

---

## 2. Code Duplication

Business logic may be duplicated across versions.

---

## 3. Additional Testing

Each version must be tested independently.

---

## 4. Documentation Overhead

Documentation must be maintained for all supported versions.

---

## 5. Delayed Cleanup

Legacy versions may remain in production for years.

---

# Real-World Examples

## GitHub API

Supports multiple API versions to maintain compatibility.

---

## Stripe API

Uses versioning to introduce new features without breaking integrations.

---

## Payment APIs

Different merchant applications may use different API versions simultaneously.

---

## Enterprise APIs

Older business systems continue using previous versions while new applications adopt the latest version.

---

# When to Use

Use API Versioning when:

- Public APIs are exposed.
- Existing clients must remain compatible.
- Breaking changes are expected.
- APIs evolve over time.

---

# When NOT to Use

Avoid introducing a new version when:

- Changes are backward compatible.
- Only internal clients exist and can be updated together.
- The change is purely additive and does not affect existing consumers.

---

# Comparison

| Feature | No Versioning | API Versioning |
|---|---|---|
| Backward Compatibility | No | Yes |
| API Evolution | Difficult | Easy |
| Breaking Changes | Common | Minimized |
| Maintenance Effort | Lower | Higher |
| Client Flexibility | Limited | High |

---

# Interview Questions

## 1. What is API Versioning?

A technique that allows APIs to evolve while maintaining compatibility with existing clients.

---

## 2. Why is API Versioning important?

It prevents breaking existing integrations when APIs change.

---

## 3. What are the common API versioning strategies?

- URI Versioning
- Query Parameter Versioning
- Header Versioning
- Media Type Versioning

---

## 4. Which API versioning strategy is most commonly used?

URI Versioning is the simplest and most widely adopted approach.

---

## 5. Should every API change create a new version?

No.

Only breaking changes typically require a new version. Backward-compatible additions usually do not.

---

# Key Takeaways

- API Versioning enables APIs to evolve safely.
- It preserves backward compatibility for existing clients.
- Multiple versioning strategies are available.
- URI Versioning is the most common approach.
- Proper versioning reduces the impact of breaking changes.

---

## Previous & Next

← Previous: [RESTful API Design](01-RESTful-API-Design.md)

→ Next: [Pagination](03-Pagination.md)