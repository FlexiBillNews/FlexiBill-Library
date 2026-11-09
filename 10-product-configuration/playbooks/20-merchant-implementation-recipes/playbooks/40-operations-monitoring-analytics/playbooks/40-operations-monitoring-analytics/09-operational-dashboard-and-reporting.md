# FlexiBill Operational Dashboard & Reporting

**Document type:** Operational Intelligence, Dashboard & Management Reporting Playbook  
**Audience:** Product, Operations, Merchant Success, Finance, Engineering, Risk, Management  
**Markets:** Indonesia (ID) and Malaysia (MY)  
**Status:** Proposed reporting framework — validate available source data, dashboard access, and approved KPI definitions before implementation

---

## 1. Purpose

This playbook defines the reporting and dashboard framework required to operate FlexiBill effectively.

The objective is to move beyond transaction-volume reporting and create an operational view that answers:

- Are merchants generating billing correctly?
- Are customers successfully paying?
- Are recurring collections working?
- How much revenue is being collected or lost?
- Are failed payments being recovered?
- Are subscribers renewing or becoming inactive?
- Are technical integrations healthy?
- Are settlement and payout processes accurate?
- Where should DOKU and merchants take action?

**Core principle:** A dashboard should lead to a decision or an action, not simply display a number.

## 2. Dashboard architecture

Organize reporting into three levels.

| Level | Audience | Primary purpose |
|---|---|---|
| L1 — Executive | Management, Product leadership, Country leadership | Business performance, revenue, growth, risk |
| L2 — Operational | Operations, Merchant Success, Finance, Risk | Performance monitoring, exceptions, recovery |
| L3 — Diagnostic | Engineering, Product, Technical Operations | Transaction traces, API/webhook failures, root cause |

The same underlying metric may appear at different levels, but the detail and action should differ.

### L1 — Executive dashboard

Answers:
- Is FlexiBill growing?
- Are merchants and subscribers active?
- Is collection performance improving?
- What is the financial exposure?
- Which merchants or segments need attention?

### L2 — Operational dashboard

Answers:
- Which billing or payment process is failing?
- Which customers or merchants need intervention?
- What is the unresolved exception value?
- Which recovery actions should happen today?

### L3 — Diagnostic dashboard

Answers:
- Which transaction, event, or API call failed?
- What was the response?
- Did the webhook arrive and process successfully?
- Is there a recurring technical failure pattern?

## 3. Core dashboard dimensions

Use nine dimensions to organize FlexiBill reporting.

| Dimension | What to monitor | Primary action |
|---|---|---|
| Business growth | Merchants, subscribers, billing volume, TPV | Growth and activation |
| Billing health | Billing generation, outstanding, overdue | Configuration and billing operations |
| Payment performance | Success, failure, pending, payment method | Collection optimization |
| Recovery | Retry, recovered bills, recovery time | Dunning improvement |
| Revenue leakage | Failed billing value, unrecovered value | Financial recovery |
| Subscriber health | Renewal, persistency, cancellation, lapse | Retention |
| Integration health | API, webhook, batch, event processing | Technical remediation |
| Finance | Settlement, payout, fees, reconciliation | Financial control |
| Customer experience | Complaints, portal issues, disputes | Service improvement |

Every dashboard should support filtering by:
- Country.
- Merchant.
- Merchant segment.
- Industry / vertical.
- Integration model.
- Billing model.
- Payment method.
- Billing cycle.
- Reporting period.
- Currency.

Only expose filters supported by the underlying source data.

## 4. Executive dashboard — recommended layout

### Section A. Business scale

Display:
- Active merchants.
- New merchants.
- Active subscribers.
- New subscriber registrations.
- Billing count.
- Billing value.
- Successful payment count.
- Successful payment value.

Show current period, prior comparable period, and trend.

### Section B. Collection performance

Display:
- Billing-level collection success rate.
- Payment-attempt success rate.
- Failed billing value.
- Pending billing value.
- Recovery rate.
- Average recovery time.

**Important:** Payment-attempt success rate and billing-level collection success rate must remain separate.

### Section C. Revenue and leakage

Display:
- Successful collection value.
- Gross failed billing value.
- Estimated recoverable value.
- Recovered value.
- Net unrecovered value.
- Estimated potential upside.

Clearly label estimates and assumptions. Gross failed billing value is not automatically recoverable revenue.

### Section D. Subscriber health

Display:
- Active subscribers.
- New subscriber cohort.
- Renewal rate.
- Persistency.
- Lapsed subscribers.
- Cancellation rate.
- Upgrade and downgrade movement.

Show cohort trends rather than relying only on monthly totals.

### Section E. Operational risk

Display:
- Critical incidents.
- Open reconciliation exceptions.
- Unresolved pending transactions.
- API and webhook failure rate.
- High-value merchant exceptions.
- Support backlog.

## 5. Operational dashboard — recommended layout

### A. Billing monitoring

| KPI | Description |
|---|---|
| Billing generated | Count of billing records created |
| Billing value | Total amount generated |
| Billing generation failure | Failed billing generation events / eligible events |
| Outstanding billing | Valid billing value not yet allocated to payment |
| Overdue billing | Billing value past due under applicable rules |
| Expired billing | Billing obligations that have reached configured expiry |
| Duplicate billing exception | Suspected duplicate obligations requiring investigation |

Segment by merchant, plan, collection, and billing cycle where data is available.

### B. Payment monitoring

| KPI | Description |
|---|---|
| Payment attempts | Total eligible collection attempts |
| Successful attempts | Attempts with definitive successful status |
| Failed attempts | Attempts with definitive failed status |
| Pending attempts | Attempts without final status |
| Attempt success rate | Successful attempts / eligible attempts |
| Billing collection success rate | Unique eligible paid billings / eligible billings |
| Successful collection value | Amount from eligible successful transactions |

Always state the reporting grain and treatment of pending, refunded, and reversed transactions.

### C. Recovery monitoring

| KPI | Description |
|---|---|
| Initially failed billings | Unique billing obligations initially failing |
| Recovered billings | Initially failed billings subsequently paid within the observation window |
| Recovery rate | Recovered eligible billings / eligible initially failed billings |
| Recovery value | Value recovered from initially failed billings |
| Average recovery days | Average time from initial failure to successful recovery |
| Retry attempts | Number of eligible retries |
| Retry efficiency | Recovered eligible billings / defined retry population |

Avoid comparing recovery rates with different observation windows or eligibility rules.

### D. Subscriber monitoring

Display:
- New subscribers.
- Active subscribers.
- Renewed subscribers.
- Failed renewals.
- Cancelled subscribers.
- Paused subscribers, where supported.
- Expired subscribers.
- Lapsed subscribers.
- Amount upgrade / downgrade movements.

Define whether the dashboard is a period flow or a point-in-time snapshot.

## 6. Technical operations dashboard

### API monitoring

Track:
- API request count.
- Successful response rate.
- Error rate.
- Timeout rate.
- Latency distribution.
- Endpoint-level failures.
- Merchant-level failure concentration.

### Webhook monitoring

Track:
- Events generated.
- Events delivered.
- Delivery failures.
- Retry count.
- Processing success.
- Duplicate events.
- Event processing delay.
- Unresolved delivery backlog.

Distinguish delivery success from successful merchant-side business processing.

### Batch and SFTP monitoring

Where applicable, track:
- Files expected.
- Files received.
- Files rejected.
- Records processed.
- Records failed.
- Duplicate records.
- Processing completion time.

### Technical drill-down

Provide traceability using available references:
- Merchant ID.
- Billing ID.
- Transaction ID.
- Event ID.
- Request / correlation ID.
- Timestamp.
- Endpoint or process.
- Error code.
- Final status.

Do not expose sensitive credentials or payment data in diagnostic dashboards.

## 7. Finance dashboard

Display:
- Successful collection value.
- Settlement-eligible value.
- Settlement processed value.
- Settlement pending value.
- Actual payout value.
- Fees and deductions.
- Refund and reversal value.
- Unreconciled value.
- Open exception count.
- Exception aging.

Show original currency by default.

For consolidated reporting:
- Preserve IDR and MYR as separate original currencies.
- Use an approved FX source and conversion date.
- Show converted and original values separately.
- Never add amounts across currencies without conversion.

## 8. Merchant performance dashboard

Provide a merchant-level view combining business and operational health.

Recommended dimensions:

| Dimension | Example metrics |
|---|---|
| Scale | Billing volume, TPV, active subscribers |
| Collection | Billing success, payment method performance |
| Recovery | Recovered value, recovery rate |
| Subscriber | Renewal, persistency, lapse |
| Operations | Pending, overdue, exception count |
| Finance | Settlement, payout, reconciliation |
| Experience | Support cases, disputes, complaints |
| Integration | API and webhook health |

A merchant health score may be introduced only after:
1. KPI definitions are agreed.
2. Weights are approved.
3. Missing-data treatment is defined.
4. Merchant size and business model are considered.
5. The score is tested against real outcomes.

Do not create arbitrary scores that imply precision without validated methodology.

## 9. Revenue leakage dashboard

Revenue leakage reporting should distinguish:

| Metric | Meaning |
|---|---|
| Gross failed billing value | Value of billing obligations with qualifying failed collection outcomes |
| Eligible recoverable value | Portion meeting the defined recovery eligibility rules |
| Recovered value | Value subsequently collected within the observation window |
| Net unrecovered value | Eligible value not recovered within the defined window |
| Potential upside | Estimated additional value from an explicitly defined improvement scenario |

Recommended visualizations:
- Failed billing value by merchant.
- Failed billing value by payment method.
- Failure reason distribution.
- Recovery rate by retry number.
- Recovery by time of day.
- Recovery by billing amount band.
- Recovery by cohort.
- High-exposure merchant heatmap.

Document the observation window, denominator, exclusions, currency, and assumptions for each metric.

## 10. Cohort and renewal dashboard

Cohort analysis is essential for understanding recurring business quality.

### Cohort definition

For the internal new-business analysis framework:

**New business = unique Billing ID first appearing in the relevant month's dataset.**

Validate this definition against the source dataset and business question before using it for subscriber acquisition reporting. Billing ID and subscriber ID are not necessarily the same entity.

### Recommended cohort dimensions

- First-seen month.
- Merchant.
- Product / plan.
- Customer or subscriber reference.
- Billing amount.
- Billing cycle.
- Payment outcome.
- Subsequent billing periods.

### Renewal outcomes

Classify each eligible cohort member into:
- Continued at same amount.
- Continued with higher amount.
- Continued with lower amount.
- Failed but still within an observation or grace window.
- Cancelled.
- Expired.
- Lapsed.
- Unknown / insufficient observation.

For bancassurance, a roughly 90-day grace or lapse convention may be relevant to specific analyses, but it is not universal. Validate the merchant's actual lapse rule and observation window.

## 11. Reporting standards and metric governance

Every published KPI must have a documented definition.

Minimum metadata:

| Metadata | Requirement |
|---|---|
| KPI name | Standardized label |
| Business definition | What the metric measures |
| Formula | Numerator and denominator |
| Grain | Attempt, transaction, billing, subscriber, merchant, or settlement |
| Source | System and report |
| Period | Daily, weekly, monthly, cohort |
| Timezone | Explicit reporting timezone |
| Currency | Original currency and conversion policy |
| Exclusions | Cancelled, refunded, reversed, pending, or other treatment |
| Owner | Responsible function |
| Refresh timestamp | When data was last updated |
| Limitation | Known source or calculation constraints |

Do not compare two metrics simply because they share the same label. Their grain and denominator must also match.

## 12. Recommended dashboard visualization library

| Business question | Recommended visualization |
|---|---|
| Is the business growing? | KPI cards and monthly trend |
| Which merchants drive volume? | Ranked bar chart |
| Where are collections failing? | Failure reason stacked bar |
| Which segments have high leakage? | Heatmap |
| Is recovery improving? | Cohort or time-series chart |
| How do subscribers renew? | Cohort retention matrix |
| Where are integration issues concentrated? | Merchant / endpoint error matrix |
| Are settlement amounts aligned? | Reconciliation waterfall |
| How old are exceptions? | Aging distribution |
| Which merchants need attention? | Merchant operational scorecard |

Use clear labels and avoid excessive colors. A chart should communicate one primary message.

## 13. Management reporting cadence

Proposed cadence:

| Report | Frequency | Audience |
|---|---|---|
| Payment and billing operations | Daily | Operations |
| Recovery and leakage | Weekly | Operations, Merchant Success |
| Merchant performance | Weekly / Monthly | Merchant Success, Product |
| Finance reconciliation | Daily / Monthly close | Finance, Operations |
| Subscriber cohort and renewal | Monthly | Product, Business |
| Executive FlexiBill performance | Monthly | Leadership |
| Product capability and adoption | Monthly / Quarterly | Product leadership |
| ID / MY strategic performance | Monthly / Quarterly | Country and regional leadership |

Actual cadence should reflect available data, business scale, and operational ownership.

## 14. Dashboard access and governance

Define role-based access.

| User group | Suggested visibility |
|---|---|
| Executive | Aggregated business and financial indicators |
| Product | Product adoption, usage, performance, capability gaps |
| Operations | Billing, payment, recovery, exception details |
| Finance | Settlement, payout, fees, reconciliation |
| Engineering | Technical traces and integration diagnostics |
| Merchant | Only its own authorized merchant data |
| Support | Minimum customer and transaction information required for cases |

Apply approved access control, privacy, and retention requirements.

Merchant-facing reporting must not reveal another merchant's customer or financial information.

## 15. Implementation approach

### Stage 1 — Metric foundation

- Confirm source systems.
- Agree metric definitions.
- Map source fields.
- Establish reporting grain.
- Validate country and currency handling.
- Identify data gaps.

### Stage 2 — Operational visibility

Prioritize:
- Billing health.
- Payment outcomes.
- Pending transactions.
- Recovery.
- Open exceptions.
- Basic merchant filters.

### Stage 3 — Finance and technical intelligence

Add:
- Settlement and payout reconciliation.
- Fee analysis.
- API and webhook monitoring.
- Batch processing.
- Exception aging.

### Stage 4 — Strategic intelligence

Add:
- Subscriber cohorts.
- Persistency and lapse.
- Revenue leakage optimization.
- Merchant performance benchmarking.
- Product adoption and capability analysis.

Do not wait for advanced analytics before providing reliable daily operational visibility.

## 16. Dashboard quality checklist

- [ ] Every KPI has an approved definition.
- [ ] Attempt, transaction, billing, and subscriber grains are separated.
- [ ] Pending transactions are not automatically classified as failed.
- [ ] Duplicate and reversed transactions are handled consistently.
- [ ] Currency and FX rules are documented.
- [ ] ID and MY are independently validated.
- [ ] Reporting period and timezone are visible.
- [ ] Data refresh timestamp is visible.
- [ ] Merchant access is restricted to authorized data.
- [ ] High-value exceptions can be traced to source references.
- [ ] Cohort observation windows are consistent.
- [ ] Estimated leakage is clearly labeled as an estimate.
- [ ] Dashboard owners and escalation routes are assigned.

## 17. Final principles

1. Build dashboards around operational and commercial decisions.
2. Use consistent KPI definitions and data grains.
3. Separate billing, payment, settlement, and subscriber views.
4. Make recovery and revenue leakage measurable.
5. Include technical and financial controls.
6. Preserve original market currency.
7. Treat ID and MY as separate validation contexts.
8. Provide merchant-level drill-down with proper access controls.
9. Show source, timestamp, and metric limitations.
10. Turn dashboard insights into accountable actions.

**The objective is to make FlexiBill measurable end to end — from merchant billing activity to customer collection, operational recovery, financial settlement, and recurring business performance.**
