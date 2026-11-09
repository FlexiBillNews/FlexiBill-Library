# FlexiBill Billing and Payment Monitoring

**Document type:** Operations playbook  
**Audience:** Operations, Product, Engineering, Finance, Customer Support, Implementation, and merchant operations  
**Markets:** Indonesia (ID) and Malaysia (MY)  
**Status:** Internal operating reference — validate monitoring sources, thresholds, and responsibilities against actual production arrangements

---

## 1. Purpose

This playbook defines how to monitor FlexiBill billing and payment operations from the moment a billing obligation is expected through payment collection and final resolution.

The monitoring framework should help teams answer five questions:

1. Was the expected billing obligation generated?
2. Was the customer successfully charged or able to pay?
3. If payment failed or remained pending, what happened next?
4. How much value remains uncollected?
5. Is the final outcome reflected correctly in merchant and DOKU records?

The goal is to move from reactive transaction investigation to proactive operational control.

## 2. Monitoring principles

### 2.1 Monitor the complete lifecycle

A recurring billing operation has several distinct stages:

```text
EXPECTED BILLING
       |
       v
BILLING GENERATION
       |
       v
BILL / INVOICE CREATED
       |
       v
PAYMENT ATTEMPT
       |
       v
PAYMENT OUTCOME
       |
       +------> SUCCESS
       |
       +------> FAILED
       |
       +------> PENDING / UNKNOWN
                     |
                     v
              STATUS RESOLUTION
                     |
          +----------+----------+
          |                     |
          v                     v
       SUCCESS               FAILED
          |                     |
          v                     v
   RECONCILIATION       RECOVERY / EXCEPTION
```

The exact events, statuses, and available timestamps depend on the applicable FlexiBill configuration and payment integration.

### 2.2 Separate operational objects

| Object | What it represents | Monitoring question |
|---|---|---|
| Customer / Member | Person or business associated with billing | Is the identity valid and correctly mapped? |
| Subscription / Contract | Commercial relationship | Is the relationship active and eligible for billing? |
| Billing obligation | Amount due for a billing period | Was the expected obligation created? |
| Invoice / Bill | Record or representation of the amount payable | Is it correct and accessible? |
| Payment attempt | An attempt to collect the obligation | Was it submitted and resolved? |
| Payment transaction | Payment processing record | What is its final outcome? |
| Settlement | Financial transfer and accounting process | Was the payment settled correctly? |

Do not use the number of payment attempts as a substitute for the number of bills or subscribers.

### 2.3 Measure count and value

Every major performance report should show both transaction count and monetary value.

A 95% success rate by count can still conceal significant leakage if the failed 5% represents high-value payments.

### 2.4 Preserve pending outcomes

A timeout or missing response is not proof that a payment failed.

Uncertain transactions must follow the approved inquiry and status-resolution process before another collection attempt is initiated.

---

## 3. Monitoring framework

Use six monitoring layers.

| Layer | Monitoring focus | Primary owner |
|---|---|---|
| 1. Billing schedule | Expected billing versus actual execution | Operations |
| 2. Billing generation | Bill creation, amount, due date, references | Operations / Implementation |
| 3. Payment processing | Attempt, success, failure, pending | Operations |
| 4. Recovery | Subsequent attempts and recovered value | Operations |
| 5. Integration health | API, webhook, and data exchange | Engineering |
| 6. Financial completion | Settlement and reconciliation | Finance |

The dashboard should make it possible to move from an aggregate KPI to the underlying merchant, billing reference, and transaction evidence, subject to access controls.

---

## 4. Billing schedule monitoring

### 4.1 Expected versus actual billing

For each merchant, define an expected billing population.

Examples:

- Monthly subscription due on a specific billing date
- Annual policy premium renewal
- School fee for an academic period
- Merchant-generated usage bill
- Contractual installment

Monitor:

| Metric | Definition |
|---|---|
| Expected billings | Obligations expected during the reporting period |
| Generated billings | Obligations successfully generated |
| Missing billings | Expected obligations not found in generated records |
| Duplicate billings | Multiple records representing the same obligation |
| Late billings | Obligations generated later than the expected time |
| Invalid billings | Records rejected or requiring correction |
| Billing value | Total amount expected or generated, clearly identifying the basis |

A missing billing is not a payment failure. It is a billing execution or upstream data issue.

### 4.2 Billing generation rate

\[
\text{Billing Generation Rate}
=
\frac{\text{Generated Billings}}
{\text{Expected Billings}}
\times 100\%
\]

The denominator must be based on an agreed expected-billing population. If no reliable expected population exists, report generated billings without presenting this ratio as complete.

### 4.3 Operational questions

- Are expected billing records missing?
- Did the billing schedule execute at the correct time?
- Are the amounts consistent with the merchant's rules?
- Are billing dates and timezones correct?
- Are there unexpected duplicate records?
- Are overdue and expired records handled according to the configured process?

---

## 5. Payment performance monitoring

### 5.1 Core payment metrics

| Metric | Formula / definition |
|---|---|
| Total Payment Attempts | Count of payment attempts in the reporting scope |
| Successful Attempts | Attempts with confirmed successful outcomes |
| Failed Attempts | Attempts with confirmed failed outcomes |
| Pending Attempts | Attempts without a confirmed final outcome |
| Transaction Success Rate | Successful attempts ÷ resolved attempts |
| Payment Value Success Rate | Successful payment value ÷ resolved payment value |
| Average Ticket Size | Payment value ÷ transaction count, with population stated |
| Failure Value | Value associated with confirmed failed transactions |
| Pending Value | Value associated with pending or unknown outcomes |

For attempt-level metrics:

\[
\text{Transaction Success Rate}
=
\frac{\text{Successful Attempts}}
{\text{Successful Attempts}+\text{Failed Attempts}}
\times 100\%
\]

Pending attempts should be reported separately rather than silently included in the failed denominator.

### 5.2 Billing-level collection performance

A billing obligation may have multiple payment attempts. To measure whether the bill was ultimately collected, use the billing obligation as the unit of analysis.

\[
\text{Billing Collection Rate}
=
\frac{\text{Unique Bills Successfully Paid}}
{\text{Unique Eligible Bills}}
\times 100\%
\]

Define whether the denominator includes only bills due during the reporting period or all bills that became eligible for collection during that period.

### 5.3 Why the distinction matters

Example:

| Billing ID | Attempt 1 | Attempt 2 | Final billing outcome |
|---|---|---|---|
| B001 | Failed | Success | Paid |
| B002 | Success | — | Paid |
| B003 | Failed | Failed | Unpaid |

Attempt-level result:

- 2 successful attempts
- 3 failed attempts
- 40% success by resolved attempt count

Billing-level result:

- 2 unique bills paid
- 3 unique bills in scope
- 66.7% collection rate

These are different metrics answering different questions.

---

## 6. Failure and pending monitoring

### 6.1 Failure categories

Classify failures into meaningful categories.

| Category | Example | Typical investigation owner |
|---|---|---|
| Customer / credential | Invalid or unavailable payment credential | Operations / payment support |
| Issuer / bank | Issuer decline or bank-side rejection | Payment Operations / partner path |
| Insufficient funds | Available balance or credit insufficient | Operations / merchant communication |
| Authorization | Authorization or mandate issue | Payment Operations / merchant |
| Technical | API, connection, or processing error | Engineering |
| Configuration | Incorrect merchant or billing setup | Implementation / Product |
| Business rule | Merchant-defined eligibility or policy rejection | Merchant |
| Unknown | Insufficient evidence to classify | Operations |

Use actual response codes and approved mapping rules. Do not invent a universal failure taxonomy or assume that a specific response code has identical meaning across payment methods.

### 6.2 Pending / unknown monitoring

Monitor:

- Number of pending transactions
- Pending payment value
- Age of pending transactions
- Merchant distribution
- Payment method distribution
- Time since last status update
- Inquiry or investigation status
- Resolution rate

A pending transaction requires status resolution, not automatic classification as failed.

### 6.3 Aging buckets

A suggested reporting structure:

| Bucket | Age since submission |
|---|---|
| Fresh | Within the normal processing window |
| Attention | Beyond the expected response window |
| Escalation | Requires investigation |
| Critical | Exceeds the approved operational threshold |

The actual time limits must be agreed with Payment Operations and the relevant payment partner. Do not use arbitrary aging thresholds as contractual SLAs.

---

## 7. Recovery monitoring

Recovery monitoring measures whether an initially failed billing obligation later becomes successfully paid.

### 7.1 Recovery metrics

| Metric | Definition |
|---|---|
| Initially Failed Bills | Unique bills with an initial confirmed failure |
| Recovered Bills | Initially failed bills that later become successfully paid |
| Unrecovered Bills | Initially failed bills still unpaid at the defined observation cutoff |
| Recovery Rate | Recovered bills ÷ eligible initially failed bills |
| Recovery Value | Value of recovered billing obligations |
| Average Recovery Time | Average time between initial failure and successful recovery |
| Never-Successful Bills | Eligible bills with no successful payment attempt by the observation cutoff |

\[
\text{Recovery Rate}
=
\frac{\text{Recovered Initially Failed Bills}}
{\text{Eligible Initially Failed Bills}}
\times 100\%
\]

State the observation cutoff and treatment of cancelled, expired, and disputed bills.

### 7.2 Recovery monitoring questions

- Which merchants have the highest recoverable value?
- Which payment methods recover most effectively?
- How many customers fail on the first attempt but later succeed?
- How many bills never succeed?
- How long does recovery take?
- Which time windows show stronger collection outcomes?
- Are recovery results driven by retries, customer action, or another payment method?

Do not attribute recovery to a particular intervention unless the underlying data establishes that relationship.

---

## 8. Merchant and segment monitoring

The dashboard should support segmentation where source data is available.

### Recommended dimensions

| Dimension | Example analysis |
|---|---|
| Merchant | Compare collection and recovery performance |
| Country | Compare ID and MY separately |
| Industry | Insurance, education, SaaS, fitness, travel |
| Payment method | Compare method performance |
| Bank / issuer | Identify issuer-level patterns |
| Billing amount | Identify ticket-size effects |
| Billing cycle | Compare monthly, quarterly, annual |
| Attempt number | Compare first attempt and subsequent attempts |
| Billing date | Identify day-of-month patterns |
| Time of day | Identify collection performance windows |
| Customer cohort | Compare new and existing subscribers |
| Billing model | Compare supported operating models |

Segmentation must not imply causation. Differences should be investigated alongside merchant mix, ticket size, authorization type, and data coverage.

---

## 9. Operational alerts

Alerts should be based on measurable conditions and agreed thresholds.

### 9.1 Alert catalogue

| Alert | Trigger concept | Owner | Suggested response |
|---|---|---|---|
| Billing generation drop | Generated bills fall below expected baseline | Operations | Validate schedule and source records |
| Duplicate billing spike | Duplicate records exceed approved tolerance | Operations / Engineering | Stop unsafe repeat processing and investigate |
| Payment success deterioration | Success rate falls materially below baseline | Operations | Segment by merchant and payment method |
| Pending transaction spike | Pending count or value exceeds threshold | Operations | Resolve status and escalate |
| Webhook processing failure | Delivery or processing failure increases | Engineering | Inspect endpoint, signature, and processing logs |
| API error spike | Technical error rate exceeds threshold | Engineering | Investigate service and integration health |
| Recovery deterioration | Recovery rate declines materially | Product / Operations | Analyze failure mix and recovery process |
| Reconciliation mismatch | Unmatched financial records exceed tolerance | Finance | Investigate transaction-to-settlement mapping |
| Merchant inactivity | Expected billing activity disappears | Operations / BD | Confirm merchant schedule and operational status |

### 9.2 Threshold governance

For every alert, document:

- Metric and calculation
- Baseline period
- Threshold
- Evaluation window
- Alert severity
- Notification channel
- Owner
- Escalation route
- Suppression and duplicate-alert rules
- Resolution and closure criteria

Use merchant-specific baselines where volumes differ substantially.

### 9.3 Avoid alert fatigue

- Do not alert on every individual low-value transient error.
- Aggregate repeated failures where appropriate.
- Suppress duplicate alerts during an active incident.
- Escalate based on financial and customer impact.
- Review false positives and missed incidents.

---

## 10. Dashboard design

### 10.1 Executive overview

Recommended headline indicators:

| KPI | Display |
|---|---|
| Total expected billing value | Currency value |
| Generated billing value | Currency value |
| Successful payment value | Currency value |
| Payment success rate | Percentage |
| Billing collection rate | Percentage |
| Failed billing value | Currency value |
| Pending payment value | Currency value |
| Recovered billing value | Currency value |
| Active subscribers | Unique count |
| Reconciliation exceptions | Count and value |

Every monetary metric must specify currency and reporting basis.

### 10.2 Operations view

Recommended sections:

1. Billing schedule health
2. Billing generation exceptions
3. Payment success and failure
4. Pending transactions and aging
5. Failed billing and recovery
6. Merchant-level exception list
7. Integration and webhook health
8. Reconciliation status

### 10.3 Merchant drill-down

The merchant view should allow authorized users to investigate:

- Billing period
- Customer or member reference
- Subscription reference
- Billing or invoice reference
- Payment transaction reference
- Amount and currency
- Payment method
- Attempt history
- Latest known outcome
- Recovery status
- Settlement or reconciliation status, where available

Do not expose sensitive payment credentials or unnecessary personal information.

---

## 11. Daily monitoring procedure

### Start of day

1. Confirm data and dashboard availability.
2. Review unresolved pending transactions.
3. Review billing generation exceptions.
4. Review prior-period payment failures.
5. Review settlement and reconciliation exceptions.
6. Identify merchants with unusual activity changes.
7. Assign owners and due dates to material exceptions.

### During the day

1. Monitor critical alerts.
2. Investigate payment and integration incidents.
3. Resolve unknown outcomes using approved procedures.
4. Coordinate merchant communication.
5. Record recovery actions and outcomes.
6. Escalate incidents based on impact.

### End of day

1. Review unresolved exceptions.
2. Confirm incident and case ownership.
3. Check the completeness of payment and billing records.
4. Review reconciliation progress.
5. Publish the operational summary.
6. Carry forward unresolved items with clear next actions.

---

## 12. Operational exception register

Maintain a structured register.

| Field | Description |
|---|---|
| Case ID | Unique operational case reference |
| Country | ID / MY |
| Merchant | Merchant identifier |
| Issue category | Billing / Payment / API / Webhook / Settlement / Other |
| Billing reference | Relevant billing or invoice ID |
| Payment reference | Relevant transaction ID |
| Amount and currency | Financial impact |
| First observed | Timestamp and timezone |
| Current status | Open / Investigating / Pending / Resolved / Closed |
| Owner | Accountable resolver |
| Root cause | Confirmed cause or unknown |
| Action taken | Investigation and recovery steps |
| Resolution time | Time to resolution |
| Customer impact | Known impact |
| Closure evidence | Supporting reference or record |

Do not mark an issue resolved solely because a retry was initiated. Confirm the final outcome.

---

## 13. Monitoring by integration model

| Integration model | Key monitoring requirements |
|---|---|
| DOKU-hosted Billing Automation | Configuration, expected billing, generated bills, payment outcomes, exceptions |
| API / H2H | API request outcomes, response handling, idempotency, event processing, reconciliation |
| Hybrid | Both FlexiBill and merchant-owned process boundaries, duplicate protection, event synchronization |
| Merchant Hosted Scheduler | Scheduler execution, merchant-side generation, supported payment integration, outcome synchronization |

Merchant Hosted Scheduler is documented for Indonesian Business Account. Do not assume MY applicability without validation.

---

## 14. Country-specific monitoring

Maintain separate operational reporting for Indonesia and Malaysia.

Validate:

- Merchant and account eligibility
- Payment methods and payment partner behavior
- Authorization and recurring collection process
- Available transaction statuses and response data
- Webhook and inquiry behavior
- Settlement timing and reconciliation
- Local currency and reporting conventions
- Customer communication and consent requirements
- Operational support ownership

Never combine ID and MY metrics without showing the country breakdown and confirming comparable definitions.

---

## 15. Data quality controls

Before publishing monitoring results, check:

- Unique billing ID definition
- Unique payment transaction ID definition
- Duplicate and retry handling
- Billing-period attribution
- Payment-date versus billing-date attribution
- Reporting timezone
- Pending transaction treatment
- Refund and reversal treatment
- Currency consistency
- Amount basis: gross, fee, or net
- Merchant and country mapping
- Missing or delayed source records

### Essential analytical rule

If a billing ID has multiple attempts, count the billing obligation once in billing-level metrics and count each valid attempt in attempt-level metrics.

If the source data does not support reliable deduplication, disclose the limitation instead of publishing a misleading KPI.

---

## 16. Monitoring maturity model

| Level | Description | Expected state |
|---|---|---|
| 1. Reactive | Teams investigate issues after complaints | Basic transaction lookup |
| 2. Visible | Daily operational metrics are available | Basic dashboards |
| 3. Controlled | Alerts, ownership, and exception registers exist | Repeatable operations |
| 4. Analytical | Merchant, payment method, cohort, and recovery analysis | Data-driven interventions |
| 5. Proactive | Validated anomaly detection and optimized operational decisions | Mature monitoring and continuous improvement |

This is a maturity framework, not a statement of current FlexiBill operational maturity.

---

## 17. Monitoring readiness checklist

### Data and definitions
- [ ] Expected billing population is defined.
- [ ] Billing and payment identifiers are mapped.
- [ ] Attempt-level and billing-level metrics are separated.
- [ ] Pending transactions are treated separately.
- [ ] Amount and currency definitions are documented.
- [ ] Country and timezone rules are defined.

### Operational controls
- [ ] Billing exceptions have owners.
- [ ] Payment pending and failure procedures are documented.
- [ ] Recovery monitoring is available.
- [ ] Alerts have approved thresholds.
- [ ] Incident escalation is defined.
- [ ] Daily reporting is assigned.

### Financial controls
- [ ] Settlement status is tracked separately.
- [ ] Reconciliation exceptions are visible.
- [ ] Refund and reversal handling is defined.
- [ ] Gross, fee, and net amounts are distinguishable.

### Governance
- [ ] Dashboard access is controlled.
- [ ] Sensitive data is protected.
- [ ] Metric definitions are approved.
- [ ] ID and MY reporting are validated separately.
- [ ] Known data limitations are disclosed.

---

## 18. Final operating principle

A reliable FlexiBill monitoring framework must connect the expected billing obligation to the actual payment outcome and final financial record.

**Monitor the obligation, not just the transaction. Measure both count and value. Resolve uncertainty before retrying. Assign every exception an owner.**
