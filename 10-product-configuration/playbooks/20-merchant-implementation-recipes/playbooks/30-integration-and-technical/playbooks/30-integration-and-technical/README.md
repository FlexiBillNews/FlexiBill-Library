# FlexiBill Integration & Technical Playbooks

> Technical implementation guidance for integrating, orchestrating, operating, and troubleshooting FlexiBill.

## 1. Purpose

This section explains how FlexiBill connects with merchant systems, DOKU payment infrastructure, and operational workflows.

It is designed for:
- Engineering and Architecture
- Solution Engineering
- Product and Technical Product Management
- Integration and Implementation
- Technical Support and Operations
- Business Development teams preparing technical solutions

The objective is to establish a consistent technical understanding of FlexiBill implementation patterns, system boundaries, integration responsibilities, and delivery controls.

**Documentation principle:** This library is an implementation guide, not a replacement for the official DOKU API specification. Endpoint paths, request schemas, authentication requirements, response codes, and webhook contracts must be verified against the current official technical documentation before implementation.

## 2. Technical Playbook Directory

The following documents will be developed in this section.

| # | Document | What it covers |
|---|---|---|
| 01 | [Integration Architecture](01-integration-architecture.md) | System context, integration models, component boundaries, and reference architecture |
| 02 | [API & H2H Integration](02-api-and-h2h-integration.md) | Merchant-to-FlexiBill integration patterns and API responsibilities |
| 03 | [Webhook & Event Management](03-webhook-and-event-management.md) | Event delivery, status updates, retries, idempotency, and event processing |
| 04 | [Billing Orchestration](04-billing-orchestration.md) | Billing lifecycle, scheduling, invoice generation, and payment orchestration |
| 05 | [Payment Authorization & Collection](05-payment-authorization-and-collection.md) | Payment method setup, authorization, recurring collection, and payment outcomes |
| 06 | [Error Handling & Recovery](06-error-handling-and-recovery.md) | Failure classification, retry patterns, recovery ownership, and exception handling |
| 07 | [Reconciliation & Reporting](07-reconciliation-and-reporting.md) | Billing-to-payment matching, settlement reconciliation, and reporting controls |
| 08 | [Security & Data Protection](08-security-and-data-protection.md) | Credential handling, sensitive data, access control, and secure integration practices |
| 09 | [Testing & Certification](09-testing-and-certification.md) | Test scenarios, integration validation, UAT, and go-live readiness |
| 10 | [Technical Solution Patterns](10-technical-solution-patterns.md) | Reference patterns for common merchant and industry requirements |

## 3. Integration Models

FlexiBill implementations should be evaluated against the merchant's system architecture and operating model.

### A. DOKU-hosted Billing Automation

FlexiBill manages supported billing and subscription workflows within the DOKU-hosted environment.

The merchant configures and operates the applicable billing capabilities through supported interfaces and integrations.

### B. API / H2H Integration

The merchant integrates its own systems with FlexiBill using supported APIs and event mechanisms.

The merchant may retain ownership of customer experience, business rules, and upstream systems while using FlexiBill for supported billing and payment functions.

### C. Hybrid Integration

The merchant and FlexiBill share responsibilities.

For example, the merchant may calculate usage or determine a billing obligation while FlexiBill handles supported billing and payment workflows.

The exact division of responsibilities must be documented for each implementation.

### D. Merchant Hosted Scheduler

The merchant controls the billing schedule and initiates supported payment workflows.

Eligibility, country availability, integration requirements, and supported payment behavior must be confirmed. Do not assume this model is available for every merchant or country.

## 4. Core Technical Principles

Every integration should follow these principles.

| Principle | Required practice |
|---|---|
| Clear system ownership | Identify the authoritative system for each business and payment data element |
| API contract accuracy | Use current official API specifications rather than assumed endpoint behavior |
| Idempotency | Prevent duplicate business actions and duplicate payment initiation where supported |
| Event-driven processing | Process asynchronous status updates safely and consistently |
| State management | Maintain a clear billing and payment state model |
| Retry discipline | Distinguish transient failures from permanent failures |
| Reconciliation | Match billing obligations, payment transactions, and settlement records |
| Security by design | Protect credentials, tokens, personal data, and sensitive payment information |
| Observability | Maintain logs, metrics, traceability, and operational alerts |
| Country validation | Confirm local payment methods, operating rules, and product availability |

## 5. Important System Boundaries

An integration design must explicitly identify which system owns each responsibility.

| Responsibility | Typical system owner |
|---|---|
| Customer master data | Merchant CRM or customer platform |
| Product and commercial contract | Merchant product or contract system |
| Pricing and complex usage calculation | Merchant system, unless explicitly supported by FlexiBill configuration |
| Billing schedule | FlexiBill or merchant scheduler, depending on the model |
| Billing obligation and invoice workflow | Defined by the selected implementation model |
| Payment processing | DOKU payment infrastructure and relevant payment partners |
| Payment result | DOKU payment flow, with merchant-side status synchronization |
| Service entitlement and fulfillment | Merchant platform |
| Accounting and general ledger | Merchant finance or ERP |
| Settlement and reconciliation | Defined DOKU and merchant operational processes |

These are reference ownership patterns. The actual implementation must be agreed and documented.

## 6. Technical Validation Rules

Before a technical design is approved, validate:

- The exact API operation and its current request/response contract.
- Authentication and authorization requirements.
- Required merchant configuration and onboarding prerequisites.
- Synchronous response versus asynchronous event behavior.
- Webhook delivery and verification requirements.
- Idempotency and duplicate-processing controls.
- Payment authorization and credential requirements.
- Supported payment methods and recurring payment restrictions.
- Error codes and recovery behavior.
- Data retention, privacy, and security requirements.
- Reconciliation and reporting requirements.
- Country-specific differences between Indonesia and Malaysia.

Do not invent endpoint names, parameters, response codes, retry intervals, or authentication mechanisms.

## 7. Relationship to Other Library Sections

| Library section | How it connects |
|---|---|
| Product Foundation | Explains FlexiBill's positioning and billing fundamentals |
| Product Configuration | Explains the product configuration building blocks |
| Merchant Implementation Recipes | Shows how merchant business models apply those building blocks |
| Integration & Technical Playbooks | Explains how to implement and operate the technical solution |

Recommended reading order:

1. Understand the product capability.
2. Identify the merchant's business and billing model.
3. Select the integration architecture.
4. Define system ownership and technical contracts.
5. Validate payment and billing behavior.
6. Execute testing and operational readiness.
7. Launch with monitoring and reconciliation controls.

## 8. Document Governance

Each technical playbook should include:

- Document owner and last-updated date.
- Scope and intended audience.
- Applicable country and integration model.
- Architecture or sequence diagram where useful.
- Confirmed API and webhook references.
- Merchant and DOKU responsibilities.
- Failure and recovery scenarios.
- Security considerations.
- Test cases and acceptance criteria.
- Known limitations and validation requirements.

Use these status labels consistently:

| Label | Meaning |
|---|---|
| Available | Confirmed for the stated scope |
| Conditional | Depends on configuration, eligibility, or integration |
| Validation required | Must be confirmed with the relevant owner |
| Gap | Not supported in the confirmed scope |
| Future / Strategic | Potential future capability, not a current commitment |

**Final principle:** A technically successful payment integration is not automatically a complete billing solution. The design must also address billing state, customer communication, failure recovery, reconciliation, service fulfillment, and operational ownership.

---

*FlexiBill Integration & Technical Playbooks — From product capability to reliable merchant implementation.*
