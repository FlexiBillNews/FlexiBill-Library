# FlexiBill Incident Management & Escalation

**Document type:** Operational Incident Management Playbook  
**Audience:** Product, Engineering, Operations, Merchant Success, Finance, Customer Support, Risk  
**Markets:** Indonesia (ID) and Malaysia (MY)  
**Status:** Proposed operational framework — confirm actual DOKU incident policies, service ownership, and contractual SLAs before adoption

---

## 1. Purpose

This playbook defines how incidents affecting FlexiBill are identified, classified, escalated, investigated, resolved, and reviewed.

FlexiBill incidents may affect:
- Billing generation.
- Subscription schedules.
- Payment authorization and collection.
- Transaction status and inquiry.
- Webhook delivery and processing.
- Customer notifications.
- Billing Portal and Member Center journeys.
- Merchant integrations.
- Reconciliation and settlement visibility.
- Customer and merchant reporting.

The objective is to protect customers and merchants, minimize financial and operational impact, restore service safely, and prevent recurrence.

**Core principle:** An incident is not resolved merely because a technical component is available again. The team must also establish the impact on billing obligations, payment outcomes, customer experience, and financial records.

## 2. Scope and incident definition

An incident is an unplanned interruption, degradation, or integrity issue that affects a FlexiBill service, integration, operational process, or customer/merchant outcome.

Examples include:
- Billing jobs not executing as expected.
- Duplicate billing generation.
- Payment collection failures beyond normal patterns.
- Incorrect or delayed payment status.
- Webhook delivery interruption.
- Incorrect subscription-state transitions.
- Customer payment update journey unavailable.
- Billing Portal access problems.
- Incorrect billing amount or schedule.
- Reconciliation mismatches.
- Data exposure or suspected security compromise.

A single customer issue may be a support case rather than a platform incident. Multiple related cases or evidence of a systemic problem may require incident escalation.

## 3. Incident management principles

1. Protect customers and prevent duplicate or unauthorized collection.
2. Establish the scope and severity using evidence.
3. Assign one incident owner.
4. Separate technical diagnosis from business-impact assessment.
5. Preserve transaction and billing traceability.
6. Communicate facts, uncertainty, and next update times.
7. Do not retry uncertain transactions without status resolution.
8. Validate financial and operational recovery.
9. Maintain an auditable incident record.
10. Complete a post-incident review for material incidents.

## 4. Incident categories

| Category | Examples | Potential impact |
|---|---|---|
| Billing | Billing generation delayed, missing, or duplicated | Incorrect or missed collection |
| Payment | Collection failure spike or payment processing issue | Merchant cash-flow impact |
| Transaction status | Incorrect, missing, or delayed final status | Duplicate payment risk or unresolved bills |
| Integration | API outage, authentication issue, webhook failure | Merchant workflow disruption |
| Subscription lifecycle | Incorrect activation, cancellation, pause, or expiry | Customer entitlement impact |
| Customer experience | Billing Portal or Member Center unavailable | Customer cannot complete an action |
| Notification | Reminder or payment confirmation not delivered | Customer confusion or delayed action |
| Finance | Settlement or reconciliation mismatch | Financial reporting uncertainty |
| Security / privacy | Suspected unauthorized access or data exposure | Customer, merchant, and regulatory risk |
| Data / reporting | Incorrect dashboard or export | Wrong operational decisions |

## 5. Severity classification

The following severity model is a proposed framework. It is not a statement of DOKU's existing incident severity policy or contractual SLA.

| Severity | Description | Example |
|---|---|---|
| SEV 1 — Critical | Widespread service failure, significant financial/customer impact, or serious security incident | Core collection unavailable across multiple merchants; suspected sensitive-data exposure |
| SEV 2 — High | Major merchant or market impact, significant degradation, or material billing/payment integrity issue | Large merchant collection disruption; duplicate billing affecting a customer population |
| SEV 3 — Medium | Limited scope or partial degradation with a workaround | One integration endpoint affected for a merchant |
| SEV 4 — Low | Minor issue with limited business impact | Non-critical reporting delay or cosmetic issue |

### 5.1 Severity assessment dimensions

Evaluate:
- Number of affected merchants.
- Number of affected customers or subscribers.
- Billing value and transaction value at risk.
- Payment or billing lifecycle stage.
- Duration and recurrence.
- Availability of a safe workaround.
- Customer impact.
- Data integrity and privacy impact.
- Financial and regulatory implications.
- Market scope: ID, MY, or both.

A low-volume issue may still be critical if it creates unauthorized collection or sensitive-data exposure.

### 5.2 Severity ownership

The incident lead should coordinate severity classification with the relevant technical and business owners.

Security, privacy, financial-integrity, or regulatory concerns should be escalated through the applicable specialist process even when the affected transaction volume is small.

## 6. Incident lifecycle

The standard incident lifecycle is:

1. Detect.
2. Record.
3. Triage.
4. Classify severity.
5. Assign incident owner.
6. Contain impact.
7. Investigate root cause.
8. Implement resolution or safe workaround.
9. Validate recovery.
10. Communicate closure.
11. Conduct post-incident review.
12. Track preventive actions.

Every material incident should have a unique incident reference and a traceable timeline.

## 7. Detection and alerting

Incidents may be detected through:

- Monitoring dashboards.
- Billing and payment exception reports.
- API availability and latency alerts.
- Webhook delivery monitoring.
- Merchant reports.
- Customer support cases.
- Finance and reconciliation exceptions.
- Engineering telemetry.
- Security monitoring.
- Partner or bank notifications.

### 7.1 Suggested detection signals

| Signal | Possible incident |
|---|---|
| Billing generation volume suddenly drops | Scheduler or billing-generation issue |
| Duplicate Billing IDs or duplicate obligations increase | Billing integrity issue |
| Payment success rate falls sharply | Payment route, issuer, or integration degradation |
| Pending transaction population grows | Status inquiry or processing issue |
| Webhook delivery drops | Event delivery disruption |
| API error rate rises | API or dependency degradation |
| Reconciliation mismatch increases | Transaction, settlement, or data integrity issue |
| Customer complaints spike | Customer-impacting service issue |
| Unexpected subscription-state changes | Lifecycle processing issue |

Alert thresholds should be calibrated
