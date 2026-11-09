# Phase 5 — Operations, Monitoring & Analytics

**Purpose:** Establish the operating model, monitoring framework, performance indicators, and analytical practices required to operate FlexiBill reliably across Indonesia and Malaysia.

**Audience:** Product, Engineering, Operations, Customer Support, Finance, Reconciliation, Business Development, and Management.

---

## 1. Why this phase matters

FlexiBill performance cannot be evaluated only by whether a subscription or billing configuration has been created.

A healthy billing operation must answer:

- Are expected bills generated?
- Are customers successfully paying?
- How much billing value is failing?
- Which failures are recoverable?
- How quickly are failed payments recovered?
- Where is revenue leakage occurring?
- Are payment outcomes reflected correctly in merchant systems?
- Can Finance reconcile transactions and settlements?
- Can Operations identify and resolve incidents before they affect more customers?

This phase connects operational execution with measurable business outcomes.

## 2. Playbook directory

| File | Playbook | Purpose |
|---|---|---|
| `01-operating-model-and-raci.md` | Operating Model and RACI | Define ownership across Product, Engineering, Operations, Finance, and merchants |
| `02-billing-and-payment-monitoring.md` | Billing and Payment Monitoring | Monitor billing generation, collection, and lifecycle performance |
| `03-kpi-and-metric-dictionary.md` | KPI and Metric Dictionary | Standardize definitions, formulas, and reporting rules |
| `04-revenue-leakage-assessment.md` | Revenue Leakage Assessment | Identify failed billing value, recovery opportunities, and revenue at risk |
| `05-dunning-and-recovery-operations.md` | Dunning and Recovery Operations | Design and monitor failed-payment recovery |
| `06-incident-management-and-escalation.md` | Incident Management and Escalation | Manage operational incidents and service-impacting failures |
| `07-customer-support-and-dispute-handling.md` | Customer Support and Dispute Handling | Define customer and merchant support workflows |
| `08-reconciliation-and-finance-operations.md` | Reconciliation and Finance Operations | Connect billing, payment, settlement, fees, and accounting |
| `09-operational-dashboard-and-reporting.md` | Operational Dashboard and Reporting | Establish management and operational reporting |
| `10-cohort-renewal-and-persistency-analysis.md` | Cohort, Renewal and Persistency Analysis | Understand subscriber retention, renewal, lapse, and billing behavior |

## 3. Operating principles

### Principle 1 — Separate billing, payment, and settlement

A bill generated is not necessarily paid. A payment success is not necessarily settled. A settled payment is not automatically reconciled to the correct merchant invoice.

Each stage requires its own metric and control.

### Principle 2 — Measure both transaction count and value

A high transaction success rate can conceal significant financial leakage when failed transactions have larger ticket sizes.

Always evaluate:

- Transaction success rate
- Payment value success rate
- Failed transaction count
- Failed payment value
- Average ticket size
- Recovery value

### Principle 3 — Analyze the full billing lifecycle

Measure the journey from expected billing through generation, payment attempts, recovery, and final resolution.

### Principle 4 — Make recovery measurable

Recovery should be measured by recovered transactions, recovered value, time to recovery, and the proportion of failed billing that never succeeds.

### Principle 5 — Distinguish merchant behavior from payment performance

A missed renewal, a cancelled subscription, an invalid customer credential, and a payment decline are different business outcomes. Do not combine them into one generic failure category.

### Principle 6 — Country-specific operations

Indonesia and Malaysia require separate validation of payment methods, authorization flows, operating procedures, settlement arrangements, and support responsibilities.

## 4. Core operational dimensions

| Dimension | Key questions |
|---|---|
| Billing health | Were all expected bills generated? |
| Payment performance | Are customers successfully paying? |
| Recovery | Are failed payments recovered? |
| Revenue leakage | How much expected value remains uncollected? |
| Subscriber health | Are subscribers renewing or lapsing? |
| Integration health | Are APIs, events, and merchant systems operating correctly? |
| Finance health | Can payment and settlement records be reconciled? |
| Customer experience | Are customers informed and supported? |
| Merchant performance | Which merchants, segments, or configurations need intervention? |

## 5. Recommended reporting layers

1. **Executive:** Revenue collected, payment success, leakage, recovery, active subscribers, and major risks.
2. **Product:** Capability adoption, merchant activation, billing model usage, and feature gaps.
3. **Operations:** Daily billing exceptions, failed transactions, pending outcomes, and unresolved cases.
4. **Engineering:** API availability, webhook processing, latency, error rates, and integration incidents.
5. **Finance:** Gross payment, fees, net settlement, refunds, unmatched records, and reconciliation exceptions.
6. **Merchant:** Billing status, payment outcomes, recovery, and customer-level exceptions.

## 6. Standard analytical segmentation

Where source data supports it, analyze performance by:

- Country: Indonesia / Malaysia
- Merchant and merchant category
- Billing model and integration model
- Payment method and issuer / bank
- Billing amount and ticket-size band
- Billing cycle and due date
- Attempt number
- Time of day and day of week
- Customer or subscriber cohort
- New business versus renewal
- First-time failure versus repeated failure
- Recovered versus never-successful billing

Do not publish a segmented metric when the underlying data cannot support its definition reliably.

## 7. Governance and data quality

Every dashboard and analysis must document:

- Data source and extraction timestamp
- Reporting period and timezone
- Grain of analysis: transaction, billing ID, invoice, subscriber, or merchant
- Unique identifier and deduplication rules
- Numerator and denominator
- Treatment of pending, reversed, refunded, and duplicate transactions
- Currency and amount basis
- Known data limitations
- Responsible owner

**Important:** Transaction-level success rate and billing-level success rate are not interchangeable. Every report must identify which one it uses.

## 8. Expected outcomes

At the end of Phase 5, DOKU teams should have a common operational language and a repeatable way to:

- Monitor FlexiBill performance.
- Detect and resolve operational exceptions.
- Quantify revenue leakage.
- Prioritize recovery opportunities.
- Understand subscriber renewal and persistency.
- Reconcile financial outcomes.
- Report performance consistently to management and merchants.

---

**Document status:** Internal operational playbook index. Each supporting document must be validated against approved FlexiBill product documentation, country operating procedures, and actual data availability.
