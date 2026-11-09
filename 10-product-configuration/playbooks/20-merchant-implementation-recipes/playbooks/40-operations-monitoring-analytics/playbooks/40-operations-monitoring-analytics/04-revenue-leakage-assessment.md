# FlexiBill Revenue Leakage Assessment

**Document type:** Revenue Assurance & Recovery Playbook  
**Audience:** Product, Business Development, Merchant Success, Operations, Finance, Data & Analytics  
**Markets:** Indonesia (ID) and Malaysia (MY)  
**Status:** Assessment framework — merchant-specific commercial, collection, and accounting rules must be validated

---

## 1. Purpose

This playbook establishes a repeatable methodology to identify, quantify, prioritize, and reduce revenue leakage across FlexiBill merchants.

The objective is to move beyond reporting payment failure rates.

A failed payment can represent:
- A temporary payment interruption.
- An unsuccessful collection attempt that can be recovered.
- An overdue customer obligation.
- A customer who has permanently stopped paying.
- A technical or operational issue.
- A billing error or incorrect amount.
- A transaction whose final status is still unknown.

These situations have different financial implications and require different actions.

**Core principle: Failed payment value is exposure, not automatically lost revenue.**

A revenue leakage assessment must distinguish billed value, failed collection exposure, recovered value, outstanding receivables, and confirmed financial loss.

## 2. What revenue leakage means in FlexiBill

Revenue leakage is the value of a legitimate merchant billing obligation that is not collected as expected, or is otherwise lost through an identifiable billing or collection failure.

Potential causes fall into six categories.

| Leakage category | Description | Example |
|---|---|---|
| Payment failure | Payment cannot be completed | Insufficient funds or issuer decline |
| Credential failure | Payment credential cannot be used | Expired or invalid card |
| Billing failure | Billing is not generated or generated incorrectly | Missing billing cycle |
| Recovery failure | Failed billing is not recovered | No retry or ineffective follow-up |
| Subscriber attrition | Customer stops continuing | Policy or membership lapse |
| Operational leakage | Process or integration issue interrupts collection | Incorrect configuration or unresolved transaction status |

Not all categories can be measured from payment transaction data alone.

Billing-generation gaps, customer churn, and confirmed revenue loss may require merchant-side subscription, policy, accounting, or CRM data.

## 3. Revenue leakage assessment framework

Use the following assessment sequence:

1. Establish the eligible billing population.
2. Identify initially failed or uncollected billings.
3. Separate pending and unresolved outcomes.
4. Measure successful recovery.
5. Determine remaining outstanding exposure.
6. Identify the reason for non-collection.
7. Estimate recoverability.
8. Prioritize interventions.
9. Measure incremental recovery after intervention.
10. Validate the financial impact with the merchant.

### 3.1 The financial waterfall

The assessment should show the movement from billing obligation to final outcome.

| Stage | Measurement | Interpretation |
|---|---|---|
| 1. Billing value due | Eligible billing amount | Expected collection population |
| 2. Initially uncollected | Failed or uncollected billing value | Initial collection exposure |
| 3. Recovered | Value subsequently collected | Successful recovery |
| 4. Other resolved | Cancelled, adjusted, credited, or otherwise resolved value | No longer outstanding under agreed rules |
| 5. Remaining outstanding | Uncollected value still eligible for collection | Current exposure |
| 6. Confirmed loss | Value confirmed lost under merchant rules | Financially validated loss |

A simplified calculation is:

`Remaining Outstanding Exposure = Initially Uncollected Value - Recovered Value - Other Validly Resolved Value`

Use the same billing cohort, currency, and observation cutoff throughout the calculation.

Do not subtract unrelated refunds, unrelated future billings, or amounts from different cohorts.

## 4. Establish the correct population

### 4.1 Define the unit of analysis

The preferred financial assessment unit is the unique Billing ID.

| Unit | Appropriate use |
|---|---|
| Payment attempt | Diagnose payment behavior |
| Transaction | Measure payment outcomes and value |
| Billing ID | Measure collection obligation and recovery |
| Subscription / policy ID | Measure recurring customer continuation |
| Subscriber ID | Measure customer retention |
| Settlement record | Validate funds received and reconciled |

A single billing can have multiple payment attempts. Counting each attempt as a separate billing overstates the number of financial obligations.

### 4.2 Define eligible billings

Include billings that:
- Represent valid merchant obligations.
- Have reached the agreed collection due point.
- Are within the assessment period.
- Have a valid billing amount and currency.
- Have sufficient status and identifier information for analysis.

Define exclusions before calculation:
- Test or sandbox billings.
- Duplicate technical records.
- Cancelled obligations.
- Invalid or voided billings.
- Fully credited or reversed obligations, where appropriate.
- Records outside the agreed observation window.

Do not automatically exclude overdue billings. They may be the most important population for leakage assessment.

### 4.3 Define the reporting period

Record:
- Billing creation period.
- Billing due period.
- Initial payment attempt period.
- Recovery observation period.
- Final assessment cutoff.
- Timezone.

These periods answer different questions.

For example, a billing generated in January may fail in January and recover in February. A report based only on February payment success could incorrectly attribute the recovered value to February's new billing performance.

## 5. Core revenue leakage metrics

### 5.1 Billing value due

`Billing Value Due = SUM(Eligible Unique Billing Amount)`

This is the total obligation expected to be collected for the defined population.

### 5.2 Initially uncollected value

`Initially Uncollected Value = SUM(Value of Unique Billings Not Collected on Initial Eligible Attempt)`

Define the initial-attempt rule and do not include unresolved pending outcomes as definitive failures.

### 5.3 Initial billing collection rate

`Initial Collection Rate = Unique Billings Collected on Initial Attempt / Eligible Unique Billings Due × 100`

This is a billing-level measure, not an attempt-level transaction success rate.

### 5.4 Recovery rate

`Recovery Rate = Unique Initially Failed Billings Subsequently Collected / Eligible Initially Failed Unique Billings × 100`

The denominator must use a defined initial-failure cohort and a consistent observation window.

### 5.5 Recovery value

`Recovery Value = SUM(Value of Initially Failed Billings Subsequently Collected)`

Count each billing once.

### 5.6 Recovery value rate

`Recovery Value Rate = Recovery Value / Eligible Initially Uncollected Value × 100`

### 5.7 Remaining outstanding exposure

`Remaining Outstanding Exposure = Initially Uncollected Value - Recovery Value - Other Validly Resolved Value`

### 5.8 Confirmed leakage

Use only when the merchant's finance or business rules establish that the value is genuinely lost.

`Confirmed Leakage = SUM(Value of Eligible Obligations Confirmed Lost)`

Do not equate this automatically with all overdue or failed billing value.

### 5.9 Potential recovery opportunity

`Potential Recovery Opportunity = Eligible Unrecovered Exposure × Assumed Recoverable Share`

The recoverable share must be grounded in historical recovery, merchant-specific evidence, or a clearly labeled scenario assumption.

## 6. Revenue leakage segmentation

An aggregate failure rate is rarely enough to identify the best intervention.

Segment the population across the following dimensions.

### 6.1 Merchant and business segment

- Merchant
- Merchant category
- Country
- Business line
- Product or plan
- New versus existing subscriber
- Billing cycle

### 6.2 Payment segment

- Payment method
- Card scheme
- Issuer or bank
- Funding source, where available
- Transaction amount band
- Initial attempt versus retry
- Failure reason
- Payment time and day

### 6.3 Subscriber segment

- New subscriber
- Continuing subscriber
- Previously recovered subscriber
- Repeated failure
- Overdue subscriber
- Cancelled or lapsed subscriber
- Customer with invalid or expired payment credentials

### 6.4 Billing segment

- Billing amount band
- Billing cycle
- Days overdue
- Initial versus recurring billing
- One-time versus recurring obligation
- Plan or collection configuration

### 6.5 Required analysis output

For every segment, show:

| Metric | Why it matters |
|---|---|
| Unique billing count | Population size |
| Billing value due | Financial scale |
| Initially uncollected count and value | Initial exposure |
| Recovery count and value | Recovery effectiveness |
| Recovery rate | Recoverability |
| Remaining outstanding value | Current exposure |
| Average ticket size | Value concentration |
| Median days to recovery | Recovery speed |
| Failure reason distribution | Root-cause direction |

Do not rank a segment only by failure percentage. A small segment with a very high failure rate may have less financial impact than a large segment with a moderate failure rate.

## 7. Root-cause classification

Every failed billing should be assigned to a consistent failure category where the available data supports it.

| Root-cause group | Examples | Potential intervention |
|---|---|---|
| Insufficient funds | Balance unavailable | Retry at an appropriate later time |
| Issuer decline | Issuer rejects transaction | Review issuer and decline patterns |
| Invalid credential | Expired or invalid card | Customer credential update |
| Authentication | Authentication not completed | Improve customer completion flow |
| Technical | Timeout, network, processing error | Investigate technical reliability |
| Configuration | Invalid merchant or billing setup | Correct configuration |
| Customer behavior | Customer does not complete action | Improve notification and payment UX |
| Billing issue | Incorrect amount or schedule | Validate billing rules and source data |
| Unknown | Insufficient failure detail | Improve classification and inquiry |

Failure codes vary by payment method and integration. Map source-system codes into a governed business taxonomy; do not assume all payment methods expose equivalent reason detail.

## 8. Recovery opportunity assessment

### 8.1 Separate recoverability from failure

A billing may be initially unsuccessful but still recoverable.

Assess each segment using:

- Historical recovery rate.
- Days since initial failure.
- Failure reason.
- Customer and subscription status.
- Remaining grace period.
- Payment credential validity.
- Merchant retry permissions.
- Customer notification status.
- Contractual collection rules.

### 8.2 Recovery opportunity tiers

| Tier | Definition | Recommended treatment |
|---|---|---|
| Tier 1 — High | Strong historical recovery and valid collection path | Prioritize operational recovery |
| Tier 2 — Medium | Recoverable under specific conditions | Targeted retry or customer action |
| Tier 3 — Low | Limited historical recovery or significant blocker | Investigate root cause |
| Tier 4 — Not currently eligible | Cancelled, invalid, disputed, or otherwise ineligible | Resolve business status before further collection |

These tiers are an analytical prioritization framework, not automatic FlexiBill payment instructions.

### 8.3 Recovery timing

Analyze recovery by elapsed time from initial failure:

- Same day
- 1–3 days
- 4–7 days
- 8–14 days
- 15–30 days
- More than 30 days

Use merchant-specific billing cycles and grace periods to interpret the results.

### 8.4 Retry policy considerations

A retry strategy should consider:
- Failure reason.
- Issuer or payment-method behavior.
- Time since the last attempt.
- Duplicate-payment risk.
- Merchant contract and retry rules.
- Customer notification requirements.
- Maximum attempt limits.
- Grace-period expiry.

Never retry an unresolved timeout as if it were a confirmed failure. First establish the actual transaction outcome.

## 9. Revenue leakage assessment template

Use this template for each merchant assessment.

### 9.1 Executive summary

| Field | Assessment |
|---|---|
| Merchant | Merchant name |
| Country | ID / MY |
| Business segment | Insurance / Fitness / Education / SaaS / Other |
| Assessment period | Start and end date |
| Billing population | Unique Billing IDs |
| Billing value due | Original currency |
| Initially uncollected value | Original currency |
| Recovered value | Original currency |
| Remaining outstanding exposure | Original currency |
| Confirmed leakage | Original currency, if validated |
| Potential recovery opportunity | Scenario-based |
| Main root cause | Evidence-based |
| Recommended intervention | Action and owner |

### 9.2 Segment assessment

| Segment | Unique billings | Value due | Uncollected value | Recovery value | Recovery rate | Remaining exposure |
|---|---:|---:|---:|---:|---:|---:|
| Segment A | | | | | | |
| Segment B | | | | | | |
| Segment C | | | | | | |
| Total | | | | | | |

The total row must be calculated from the underlying records, not by averaging segment percentages.

### 9.3 Root-cause assessment

| Failure reason | Billing count | Billing value | Recovery count | Recovery value | Recommended action |
|---|---:|---:|---:|---:|---|
| Insufficient funds | | | | | |
| Issuer decline | | | | | |
| Invalid credential | | | | | |
| Technical error | | | | | |
| Authentication | | | | | |
| Configuration | | | | | |
| Other / unknown | | | | | |

### 9.4 Action register

| Priority | Issue | Evidence | Proposed action | Owner | Target date | Success metric |
|---|---|---|---|---|---|---|
| P0 | | | | | | |
| P1 | | | | | | |
| P2 | | | | | | |

## 10. Vertical-specific assessment considerations

### 10.1 Insurance

Focus on:
- Premium billing value.
- Policy and subscriber identifiers.
- Renewal and persistency cohorts.
- Failed premium recovery.
- Grace-period and lapse rules.
- Reinstatement.
- Payment-method performance.
- Premium amount bands.

For bancassurance, assess the relationship between initial failure, recovery during the applicable grace period, and eventual lapse.

A 90-day grace period may apply in some arrangements, but must be validated with each insurer. Do not use it as a universal lapse rule.

### 10.2 Fitness and membership

Focus on:
- Membership renewal.
- Monthly and annual billing.
- Failed renewal recovery.
- Paused and cancelled memberships.
- Member payment credential updates.
- Reactivation.
- Member engagement and retention.

Distinguish a payment failure from a member who intentionally cancels.

### 10.3 Education

Focus on:
- Tuition and recurring school fees.
- Installment schedules.
- Partial payments where supported.
- Parent or guardian payment behavior.
- Due-date concentration.
- Outstanding balances.
- Term-based collection.

Separate unpaid obligations from approved scholarships, waivers, discounts, and payment-plan adjustments.

### 10.4 SaaS and digital subscriptions

Focus on:
- Monthly and annual recurring revenue exposure.
- Renewal failures.
- Credential updates.
- Grace-period conversion.
- Subscription suspension and cancellation.
- Plan downgrade and upgrade.
- Customer reactivation.

Do not treat billed subscription value as recognized revenue without finance validation.

### 10.5 Travel and hospitality

Focus on:
- Booking and reservation billing.
- Deposits and installment schedules.
- Payment deadlines.
- Cancellation and refund rules.
- No-show and booking status.
- Multiple payment events for one booking.

Ensure payment failure and booking cancellation are not double-counted as separate lost obligations.

### 10.6 Corporate and B2B

Focus on:
- Invoice value and aging.
- Contractual payment terms.
- Partial settlement.
- Payment reconciliation.
- Disputes and credit notes.
- Collection cycle and debtor concentration.

A delayed B2B payment is not necessarily a failed automated debit or confirmed loss.

## 11. Illustrative calculation

The following example demonstrates the methodology. Figures are illustrative, not actual merchant results.

Assume a merchant has 10,000 eligible unique billings due in a month.

| Measure | Illustrative result |
|---|---:|
| Eligible unique billings | 10,000 |
| Billing value due | Rp10,000,000,000 |
| Initially collected billings | 7,000 |
| Initially collected value | Rp7,000,000,000 |
| Initially uncollected billings | 3,000 |
| Initially uncollected value | Rp3,000,000,000 |
| Recovered billings | 1,200 |
| Recovered value | Rp1,200,000,000 |
| Other validly resolved value | Rp200,000,000 |
| Remaining outstanding exposure | Rp1,600,000,000 |

Calculations:

`Initial Collection Rate = 7,000 / 10,000 = 70%`

`Recovery Rate = 1,200 / 3,000 = 40%`

`Recovery Value Rate = Rp1.2B / Rp3.0B = 40%`

`Remaining Outstanding Exposure = Rp3.0B - Rp1.2B - Rp0.2B = Rp1.6B`

The Rp1.6B is remaining exposure under the example assumptions. It is not automatically confirmed revenue loss.

If historical evidence supports a 25% recoverable share of the remaining exposure:

`Potential Recovery Opportunity = Rp1.6B × 25% = Rp400M`

This Rp400M is a scenario estimate, not a guaranteed recovery.

## 12. Measuring incremental impact

An intervention should be measured against a defensible baseline.

Possible interventions:
- Retry timing changes.
- Failure-reason-based recovery.
- Customer notifications.
- Payment credential update journeys.
- Merchant configuration correction.
- Billing schedule correction.
- Improved transaction inquiry and status resolution.
- Operational exception management.

### 12.1 Before-and-after measurement

Compare:
- Eligible billing population.
- Initial collection rate.
- Recovery rate.
- Recovered value.
- Time to recovery.
- Remaining exposure.
- Customer complaints and disputes.

Control for seasonality, merchant mix, amount changes, payment-method mix, and cohort maturity.

### 12.2 Incremental recovered value

A simple before-and-after comparison is not necessarily causal.

Where a suitable comparison group exists:

`Incremental Recovery = Actual Recovered Value - Expected Recovered Value Without Intervention`

The expected value should come from an appropriate baseline or comparison cohort, adjusted for population and observation differences.

### 12.3 Commercial impact

Where the commercial model is known:

`Incremental DOKU Revenue = Incremental Eligible Successful Payment Value × Applicable Commercial Rate + Applicable Fixed Fees`

Use the actual merchant contract, fee basis, and pricing rules.

Do not assume all recovered value generates incremental DOKU revenue. Consider fees, reversals, refunds, commercial exemptions, and whether the payment would have succeeded anyway.

## 13. Product and operational opportunity mapping

| Leakage issue | Potential FlexiBill / DOKU response | Validation required |
|---|---|---|
| Repeated failed collection | Retry and recovery operations | Retry capability and merchant policy |
| Expired payment credential | Customer payment update journey | Supported credential update flow |
| Billing not generated | Billing configuration and integration review | Source system and API behavior |
| Poor visibility | Monitoring and reporting | Data availability |
| Manual bulk billing | Supported upload / bulk billing workflow | Merchant configuration |
| Customer follow-up burden | Notification and merchant communication | Confirmed channel and product integration |
| Subscriber attrition | Renewal and persistency analytics | Merchant lifecycle data |
| Integration exception | API, webhook, and operational diagnostics | Actual integration model |

Do not promise capabilities that have not been confirmed as available.

For example:
- PayChat is confirmed in the current product context for bulk-upload billing; do not assume a complete Pricing Table or WhatsApp seller frontend.
- Member Center API readiness does not automatically mean the customer-facing registration frontend is ready.
- Digital Catalog integration with Subscription or Pricing Table must be validated.
- Native metering and advanced entitlement management should not be represented as generally available.
- Merchant Hosted Scheduler scope must be validated by market; current documentation identifies an Indonesian Business Account context, not automatic MY parity.

## 14. Data requirements

A robust assessment ideally requires:

| Data domain | Required fields |
|---|---|
| Merchant | Merchant ID, merchant name, country |
| Billing | Billing ID, subscriber ID, subscription/policy ID, amount, currency, due date, status |
| Payment | Transaction ID, attempt ID, amount, currency, payment method, issuer, result, failure reason |
| Recovery | Initial failure timestamp, retry sequence, recovery timestamp, recovered amount |
| Subscriber | Lifecycle state, activation date, cancellation date, lapse or reinstatement date |
| Settlement | Settlement ID, settlement date, amount, fee, adjustment |
| Product | Plan, collection, billing frequency, configuration |
| Integration | API/webhook event, request status, event timestamp, processing result |

Not every merchant will expose every field. Document unavailable fields and do not fabricate substitute metrics.

## 15. Data quality and interpretation controls

Before publishing an assessment:

1. Deduplicate Billing IDs.
2. Validate transaction-to-billing relationships.
3. Separate attempts from unique billing obligations.
4. Resolve pending and unknown payment statuses.
5. Validate refunds, reversals, and partial collections.
6. Confirm observation-window maturity.
7. Verify billing amounts and currencies.
8. Confirm timestamp timezone.
9. Validate subscriber and policy identifiers.
10. Reconcile financial totals where possible.

For ID and MY, preserve the source currency and report separately. Consolidation requires an approved FX source, rate, and conversion date.

## 16. Revenue leakage maturity model

| Level | Capability | Outcome |
|---|---|---|
| 1 — Visibility | Basic billing and payment reporting | Understand the size of collection issues |
| 2 — Diagnosis | Failure reason and segment analysis | Identify where leakage occurs |
| 3 — Recovery | Structured retry and follow-up measurement | Improve collection outcomes |
| 4 — Optimization | Cohort, timing, and recovery opportunity analysis | Prioritize effective interventions |
| 5 — Revenue assurance | Integrated billing, collection, settlement, and finance view | Govern measurable financial outcomes |

This is a maturity framework for assessment and planning, not a statement that every level is currently available as a native FlexiBill capability.

## 17. Assessment deliverable checklist

A completed merchant assessment should contain:

- [ ] Executive summary.
- [ ] Scope, reporting period, and observation cutoff.
- [ ] Eligible billing population.
- [ ] Billing-level collection performance.
- [ ] Attempt-level payment performance.
- [ ] Initially failed billing exposure.
- [ ] Recovery count, value, and timing.
- [ ] Remaining outstanding exposure.
- [ ] Confirmed loss, if validated.
- [ ] Root-cause segmentation.
- [ ] Subscriber and renewal analysis where relevant.
- [ ] Merchant-specific grace and lapse rules.
- [ ] Prioritized action register.
- [ ] Measurement baseline and post-intervention plan.
- [ ] Data-quality limitations.
- [ ] Finance or merchant validation.

## 18. Final principles

1. Start with unique billing obligations, not payment attempts.
2. Separate initial failure from final collection outcome.
3. Measure recovery using mature cohorts.
4. Distinguish outstanding exposure from confirmed loss.
5. Prioritize by financial value and recoverability, not failure percentage alone.
6. Validate lapse, grace, and cancellation rules with the merchant.
7. Measure incremental impact rather than claiming all post-intervention recovery as incremental.
8. Separate IDR and MYR unless approved conversion rules exist.
9. Use product capabilities accurately and distinguish available features from roadmap opportunities.
10. Make every leakage estimate traceable to its source population and assumptions.

**The objective of revenue leakage assessment is to convert billing and payment data into a financially defensible action plan: what is exposed, what can be recovered, why collection is failing, and what measurable intervention should happen next.**
