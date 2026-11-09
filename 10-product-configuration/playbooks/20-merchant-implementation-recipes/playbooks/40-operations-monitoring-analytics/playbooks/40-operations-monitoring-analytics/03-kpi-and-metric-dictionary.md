# FlexiBill KPI & Metric Dictionary

**Document type:** Operations, Product & Business Measurement Standard  
**Audience:** Product, Engineering, Operations, Finance, Business Development, Merchant Success, Management  
**Markets:** Indonesia (ID) and Malaysia (MY)  
**Status:** Internal measurement framework — validate metric availability and market-specific rules before operational adoption

---

## 1. Purpose

This document establishes a common measurement language for FlexiBill.

It is designed to prevent inconsistent reporting across teams, particularly when payment attempts, billing records, subscribers, recovered amounts, and recognized revenue are treated as if they were the same thing.

Every KPI should have:

1. A clear business definition.
2. A defined measurement grain.
3. A numerator and denominator, where applicable.
4. A reporting period and attribution rule.
5. Explicit treatment of pending, failed, duplicate, refunded, and reversed records.
6. A named data source and accountable owner.
7. Separate IDR and MYR reporting unless an approved FX methodology is applied.

**Core principle:** One payment attempt is not one billing, and one billing is not one subscriber.

## 2. Measurement architecture

FlexiBill reporting should distinguish six measurement layers.

| Layer | Measurement object | Key question |
|---|---|---|
| Billing | Invoice, bill, billing ID | Was the amount due generated correctly? |
| Payment | Transaction and attempt | Did the payment attempt succeed? |
| Collection | Unique billing obligation | Was the bill collected? |
| Subscriber | Member, customer, subscription | Is the subscriber continuing? |
| Recovery | Previously unsuccessful billing | Was the failed billing recovered? |
| Finance | Settlement and accounting record | Was collected money settled and reconciled? |

### 2.1 Required data grains

| Grain | Definition | Example key |
|---|---|---|
| Attempt-level | One payment attempt | Transaction ID / attempt ID |
| Transaction-level | One payment transaction | Transaction ID |
| Billing-level | One unique billing obligation | Billing ID |
| Subscription-level | One subscription agreement | Subscription ID |
| Subscriber-level | One customer or member | Member ID / customer ID |
| Merchant-level | One merchant entity | Merchant ID |
| Settlement-level | One settlement record or batch | Settlement ID / batch ID |

A report must declare its grain. Never aggregate attempt-level counts and describe them as unique billings or subscribers.

## 3. Billing generation KPIs

### 3.1 Billing generation volume

**Definition:** Number of unique billing records generated within the reporting period.

Formula:

`Billing Generation Volume = COUNT(DISTINCT Billing ID)`

**Grain:** Billing ID.

**Attribution:** Billing creation timestamp.

Exclude duplicate technical records representing the same billing obligation. Do not exclude legitimate separate billing cycles for the same subscriber.

### 3.2 Billing generation value

**Definition:** Total amount of unique billings generated in the reporting period.

Formula:

`Billing Generation Value = SUM(Unique Billing Amount)`

Use one record per unique Billing ID.

Report gross billing value separately from tax, discounts, fees, or net receivable where those fields are available.

### 3.3 Billing generation success rate

Use only when the system exposes a meaningful billing-generation request and outcome.

`Billing Generation Success Rate = Successfully Generated Billing Requests / Eligible Billing Generation Requests × 100`

Do not use this KPI as a substitute for payment success.

### 3.4 Billing overdue rate

`Overdue Billing Rate = Unique Overdue Billings / Unique Billings Due × 100`

Define the overdue cutoff, grace period, and treatment of cancelled or disputed billings for each merchant.

### 3.5 Billing aging

Group outstanding billing value by age:

- Not yet due
- 1–7 days overdue
- 8–30 days overdue
- 31–60 days overdue
- 61–90 days overdue
- More than 90 days overdue

These are reporting bands, not universal FlexiBill lapse rules.

## 4. Payment performance KPIs

### 4.1 Payment attempt volume

`Payment Attempt Volume = COUNT(DISTINCT Attempt ID)`

If an attempt ID is unavailable, document the transaction-level proxy and its limitations.

### 4.2 Payment attempt success rate

`Payment Attempt Success Rate = Successful Payment Attempts / Resolved Payment Attempts × 100`

Resolved attempts include definitive successful and failed outcomes.

Pending, unknown, and unresolved timeout records should not automatically be counted as failures. Report them separately.

### 4.3 Payment attempt failure rate

`Payment Attempt Failure Rate = Definitive Failed Attempts / Resolved Payment Attempts × 100`

Classify failure reasons where possible:

- Issuer or bank decline
- Insufficient funds
- Expired or invalid payment credential
- Authentication failure
- Technical or network error
- Merchant configuration issue
- Risk or compliance rejection
- Other / unknown

### 4.4 Pending payment rate

`Pending Payment Rate = Pending or Unknown Attempts / Total Payment Attempts × 100`

Show both pending count and pending value.

A timeout is not proof that a payment failed. Resolve transaction status through the appropriate inquiry or reconciliation process before initiating another charge.

### 4.5 Payment success value

`Payment Success Value = SUM(Amount of Successful Transactions)`

Use the successful transaction amount and clearly state whether the amount is gross or net of fees.

### 4.6 Payment performance segmentation

Where data is available, segment by:

- Merchant and merchant category
- Country
- Payment method
- Issuer or bank
- Card scheme
- Transaction amount band
- Billing cycle
- Attempt sequence
- Day of week
- Hour of day
- Failure reason

Do not infer a causal relationship from a correlation in a segment.

## 5. Billing-level collection KPIs

These KPIs answer whether a billing obligation was collected, rather than whether an individual payment attempt succeeded.

### 5.1 Billing collection success

`Billing Collection Success Rate = Unique Successfully Collected Billings / Eligible Unique Billings Due × 100`

A billing is successfully collected when its obligation is fulfilled under the merchant's defined collection rules.

Count each Billing ID once, even if it has multiple payment attempts.

### 5.2 Billing collection value rate

`Billing Collection Value Rate = Successfully Collected Billing Value / Eligible Billing Value Due × 100`

Use a consistent gross or net billing basis.

### 5.3 Uncollected billing rate

`Uncollected Billing Rate = Unique Uncollected Billings / Eligible Unique Billings Due × 100`

Report pending and unresolved billings separately when their final outcome is not known.

### 5.4 Partial collection rate

Where partial payments are supported and represented in the data:

`Partial Collection Rate = Unique Partially Collected Billings / Eligible Unique Billings Due × 100`

A partially paid billing must not be classified as fully collected.

### 5.5 First-attempt billing collection rate

`First-Attempt Collection Rate = Unique Billings Collected on First Attempt / Eligible Unique Billings Due × 100`

This measures the effectiveness of the initial collection attempt.

### 5.6 Multi-attempt collection rate

`Multi-Attempt Collection Rate = Unique Billings Collected After First Attempt / Eligible Unique Billings Due × 100`

Use the billing's complete attempt history and a consistent observation cutoff.

## 6. Recovery and dunning KPIs

Recovery measures the collection of billings that initially failed or were otherwise unsuccessful.

### 6.1 Initially failed billing population

`Initially Failed Billings = Unique Billings with a Definitive Initial Collection Failure`

Exclude unresolved pending outcomes until their status is known.

The initial failure must be determined using the first eligible collection attempt or another explicitly documented business rule.

### 6.2 Recovery count

`Recovered Billing Count = COUNT(DISTINCT Billing ID Successfully Collected After Initial Failure)`

### 6.3 Recovery rate

`Recovery Rate = Recovered Unique Billings / Eligible Initially Failed Unique Billings × 100`

The denominator must use the same initial-failure cohort and observation window.

Do not compare a fully observed cohort with a recently created cohort that has had less time to recover.

### 6.4 Recovery value

`Recovered Billing Value = SUM(Value of Recovered Unique Billings)`

Count each recovered billing once.

### 6.5 Recovery value rate

`Recovery Value Rate = Recovered Billing Value / Eligible Initially Failed Billing Value × 100`

### 6.6 Time to recovery

`Time to Recovery = Successful Collection Timestamp - Initial Failure Timestamp`

Report median and percentile values, not only the average.

Useful bands include:

- Same day
- 1–3 days
- 4–7 days
- 8–14 days
- 15–30 days
- More than 30 days

Adapt these bands to the merchant's billing cycle and grace period.

### 6.7 Retry effectiveness

`Retry Success Rate = Successful Retry Attempts / Resolved Retry Attempts × 100`

This is attempt-level.

Keep it separate from billing-level recovery rate.

### 6.8 Recovery by retry sequence

Compare outcomes across:

- Initial attempt
- Retry 1
- Retry 2
- Retry 3
- Subsequent retries

Also measure the number of unique billings recovered at each sequence.

Avoid assuming more retries always produce more recovered value. Consider customer experience, issuer behavior, operational cost, and merchant rules.

## 7. Never-successful billing and revenue leakage

### 7.1 Never-successful billing count

**Definition:** Unique eligible billings that have no successful collection within the defined observation window.

`Never-Successful Billing Count = COUNT(DISTINCT Eligible Billing ID with No Successful Collection by Cutoff)`

This is not necessarily the same as a billing that has never had a successful transaction in its entire history. State the observation window.

### 7.2 Never-successful billing value

`Never-Successful Billing Value = SUM(Value of Never-Successful Billings)`

### 7.3 Gross failed billing value

`Gross Failed Billing Value = SUM(Value of Eligible Billings Initially Uncollected)`

This is an exposure measure, not confirmed lost revenue.

### 7.4 Recovered value

`Recovered Value = SUM(Value of Initially Failed Billings Subsequently Collected)`

### 7.5 Outstanding failed value

`Outstanding Failed Value = Gross Failed Billing Value - Recovered Value - Other Validly Resolved Amounts`

Define treatment of partial collections, cancellations, credit notes, write-offs, and adjustments.

### 7.6 Net revenue leakage estimate

A leakage estimate should distinguish:

1. Failed billing exposure.
2. Value recovered within the observation window.
3. Value still outstanding.
4. Value cancelled or otherwise no longer collectible.
5. Value confirmed lost under the merchant's accounting or business rules.

Do not label all failed billing value as lost revenue.

Where confirmed loss data is unavailable, use the term **unrecovered billing exposure**, not confirmed revenue loss.

### 7.7 Recovery opportunity

`Recovery Opportunity = Eligible Unrecovered Billing Value × Assumed Recoverable Share`

The recoverable share must be an explicit assumption or supported by historical cohort data.

Show conservative, base, and upside scenarios separately. Do not present potential recovery as guaranteed revenue.

## 8. Subscriber and subscription health KPIs

### 8.1 Active subscribers

An active subscriber definition must be agreed with the merchant.

A possible operational definition is:

`Active Subscribers = COUNT(DISTINCT Subscriber ID Meeting the Agreed Active-State Rules at Snapshot Date)`

Specify treatment of:

- Active
- Trial
- Paused
- Overdue
- Cancelled
- Expired
- Grace period
- Suspended

A subscriber with an overdue billing may still be considered active under one merchant's rules and inactive under another's.

### 8.2 New subscribers

`New Subscribers = COUNT(DISTINCT Subscriber ID First Activated During Period)`

Use activation date, not merely account creation date, unless the business definition explicitly uses registration.

### 8.3 New business billing cohort

For recurring billing and insurance analysis, use a clearly documented cohort rule.

**Recommended analysis rule:** New business in a month is the set of unique Billing IDs first appearing in that month's available dataset.

`New Business Billing Cohort (Month M) = Billing IDs whose First Observed Month = M`

This is a dataset-based first-observed definition. It may differ from actual customer acquisition or policy inception if historical records are incomplete.

### 8.4 Renewal rate

`Renewal Rate = Eligible Subscribers or Billing Obligations Successfully Renewed / Eligible Subscribers or Billing Obligations Due for Renewal × 100`

State whether the unit is a subscriber, subscription, policy, or billing obligation.

Use one consistent unit in numerator and denominator.

### 8.5 Persistency

Persistency measures the proportion of a defined starting cohort that remains in force or continues to meet the agreed active/renewed condition after a specified period.

`Persistency at Period T = Cohort Members Meeting the Persistency Rule at T / Eligible Starting Cohort Members × 100`

Specify:

- Cohort entry date
- Observation period
- Renewal eligibility
- Grace-period treatment
- Cancellation and reinstatement rules
- Subscriber or policy identifier

### 8.6 Lapse rate

`Lapse Rate = Eligible Cohort Members Lapsed by Cutoff / Eligible Cohort Members Due for Continuation × 100`

A lapse is determined by the merchant's contract and policy rules.

For some bancassurance arrangements, a grace period of approximately 90 days may apply. This is not a universal FlexiBill rule. Validate each insurer's grace, reinstatement, and lapse definitions.

### 8.7 Subscriber churn

`Subscriber Churn Rate = Subscribers Lost During Period / Eligible Starting Active Subscriber Base × 100`

Define whether the denominator is opening subscribers or average subscribers. Do not mix these methods across reports.

### 8.8 ARPU

`ARPU = Recognized Revenue or Agreed Billing Value / Average Active Subscribers`

State whether ARPU uses recognized revenue, collected value, or billed value. These are different business measures.

### 8.9 Amount movement

Track recurring amount changes between comparable billing periods:

- Upgrade: amount increases
- Downgrade: amount decreases
- No change
- New charge or add-on
- Discount or coupon change
- Tax or fee change
- Partial period / proration adjustment

`Amount Movement = Current Comparable Billing Amount - Previous Comparable Billing Amount`

Do not classify a tax, currency, or one-time adjustment as a plan upgrade without checking the underlying commercial reason.

## 9. Finance and reconciliation KPIs

### 9.1 Settlement value

`Settlement Value = SUM(Amount Settled in the Defined Settlement Period)`

Settlement period may differ from transaction creation or payment success period.

### 9.2 Settlement completion rate

`Settlement Completion Rate = Eligible Successful Transaction Value Settled / Eligible Successful Transaction Value Expected to Settle × 100`

Define expected settlement timing and treatment of reserves, fees, reversals, and adjustments.

### 9.3 Reconciliation match rate

`Reconciliation Match Rate = Matched Eligible Records / Total Eligible Records × 100`

Define the reconciliation unit: transaction, billing, settlement line, or accounting entry.

### 9.4 Unmatched transaction count

`Unmatched Transaction Count = COUNT(Eligible Records Without a Valid Match)`

Separate missing, duplicate, amount-mismatch, status-mismatch, and timing-difference exceptions.

### 9.5 Refund rate

`Refund Rate = Refunded Transaction Count / Eligible Successful Transaction Count × 100`

Also report refund value rate:

`Refund Value Rate = Refunded Value / Eligible Successful Transaction Value × 100`

State whether partial refunds are counted by transaction or refund event.

### 9.6 Net collected value

A reporting calculation may be:

`Net Collected Value = Successful Collection Value - Refunds - Reversals`

Do not deduct MDR or other fees unless the metric is explicitly defined as net settlement or merchant proceeds.

## 10. API, webhook, and integration KPIs

### 10.1 API availability

`API Availability = Available Monitoring Intervals / Total Eligible Monitoring Intervals × 100`

Define endpoint scope, maintenance exclusions, monitoring frequency, and timeout threshold.

### 10.2 API success rate

`API Success Rate = Successful Eligible API Requests / Total Eligible API Requests × 100`

Separate technical HTTP/API success from successful business outcomes.

An accepted API request does not prove that a billing was generated or a payment collected.

### 10.3 API latency

Measure response time using median, P95, and P99.

Report by endpoint and operation type where possible.

### 10.4 Webhook delivery success

`Webhook Delivery Success Rate = Successfully Delivered Webhook Events / Eligible Webhook Delivery Events × 100`

Define whether the denominator is unique events or delivery attempts.

Report both when retries are involved.

### 10.5 Webhook processing success

`Webhook Processing Success Rate = Successfully Processed Unique Events / Eligible Unique Events Received × 100`

Delivery success and business processing success are separate measures.

### 10.6 Duplicate event rate

`Duplicate Event Rate = Duplicate Events Detected / Total Events Received × 100`

Use event identifiers or an approved deduplication key.

### 10.7 Event processing delay

`Event Processing Delay = Processing Timestamp - Event Creation or Receipt Timestamp`

State which timestamp starts the measurement.

## 11. Customer experience and operational KPIs

Potential measures include:

| KPI | Definition |
|---|---|
| Support ticket volume | Count of eligible FlexiBill-related support cases |
| Billing-related contact rate | Billing-related cases / eligible billings |
| Payment-related contact rate | Payment-related cases / eligible payment transactions |
| First response time | Time from ticket creation to first human response |
| Resolution time | Time from ticket creation to resolution |
| Repeat contact rate | Cases reopened or repeated for the same issue / eligible cases |
| Dispute rate | Disputed transactions / eligible successful transactions |
| Complaint rate | Relevant complaints / defined customer population |

Define case taxonomy, deduplication, SLA calendar, and customer-level grouping before comparing merchants.

## 12. KPI definition register

Every production dashboard KPI should have a governed definition.

| Required field | Description |
|---|---|
| KPI name | Standard business label |
| Purpose | Decision the KPI supports |
| Definition | Exact business meaning |
| Grain | Attempt, transaction, billing, subscription, subscriber, settlement |
| Numerator | Exact qualifying population |
| Denominator | Exact eligible population |
| Formula | Calculation |
| Attribution date | Creation, due, attempt, success, settlement, or snapshot |
| Observation window | Time allowed for outcome to mature |
| Exclusions | Cancelled, duplicate, test, reversed, or other records |
| Pending treatment | Separate, exclude, or include under an explicit rule |
| Currency | IDR, MYR, or approved converted reporting currency |
| Source | System, table, report, or event |
| Owner | Accountable business or technical function |
| Refresh frequency | Real-time, hourly, daily, monthly |
| Limitations | Known data-quality or interpretation issues |

## 13. Standard dashboard KPI hierarchy

### Executive view

- Unique billing value due
- Unique billing value collected
- Billing-level collection success
- Initially failed billing value
- Recovered value
- Unrecovered billing exposure
- Active subscribers
- Renewal / persistency
- Settlement and reconciliation status

### Operations view

- Billing generation volume
- Overdue billings
- Attempt-level success and failure
- Pending transactions
- Retry performance
- Recovery rate
- Time to recovery
- Exception backlog

### Product and Engineering view

- API availability and latency
- API success rate
- Webhook delivery and processing
- Duplicate events
- Billing generation errors
- Integration exception volume

### Merchant view

- Billing value due and collected
- Collection success by segment
- Failed and recovered billings
- Subscriber continuation
- Outstanding exposure
- Merchant-specific operational exceptions

## 14. Country and currency rules

Indonesia and Malaysia must be measured as separate operating markets.

- Preserve original transaction and billing currency.
- Report IDR and MYR separately.
- Use an approved FX rate, source, and conversion date when consolidated reporting is required.
- Do not compare nominal IDR and MYR amounts without normalization.
- Validate local payment methods, settlement cycles, tax treatment, banking calendars, and merchant configurations independently.
- Do not assume that an integration, retry rule, or product capability available in Indonesia is also available in Malaysia.

## 15. Data quality controls

Before publishing a KPI:

1. Validate unique identifiers.
2. Check duplicate Billing IDs and transaction IDs.
3. Confirm status mapping.
4. Resolve pending and unknown outcomes.
5. Confirm timestamp timezone.
6. Validate currency and decimal precision.
7. Check billing-to-transaction relationships.
8. Confirm refunds and reversals.
9. Verify observation-window completeness.
10. Compare aggregate values against finance or source-system totals.

Flag material data-quality issues on the dashboard rather than silently excluding them.

## 16. Recommended cohort methodology

For monthly renewal and persistency analysis:

1. Identify each Billing ID's first observed month in the available dataset.
2. Assign the Billing ID to that month’s cohort.
3. Track subsequent billing periods using the agreed subscriber, policy, or subscription key.
4. Classify each cohort member as continued, upgraded, downgraded, unchanged, overdue, lapsed, cancelled, or unknown.
5. Measure each cohort only after its observation period is sufficiently mature.
6. Show reinstatements separately from uninterrupted continuation.
7. Explain missing historical data and incomplete future periods.

**Important:** Billing ID is suitable for defining a first-observed billing cohort. Renewal tracking may require a separate stable subscriber, policy, or subscription identifier because each billing cycle can generate a new Billing ID.

## 17. KPI governance and ownership

| Function | Proposed accountability |
|---|---|
| Product | Business definition and product outcome |
| Data / Analytics | Data model, calculation, cohort methodology |
| Engineering | Event integrity, identifiers, technical telemetry |
| Operations | Daily monitoring and exception action |
| Finance | Settlement, fees, reconciliation, accounting interpretation |
| Merchant Success / Business | Merchant-specific rules and commercial interpretation |
| Risk / Compliance | Applicable risk and compliance definitions |

These are proposed functional responsibilities. Confirm actual DOKU team ownership and approval authority before operational rollout.

## 18. KPI adoption checklist

Before a KPI becomes an official management metric, confirm:

- [ ] Definition and business purpose approved.
- [ ] Measurement grain documented.
- [ ] Numerator and denominator validated.
- [ ] Pending and unknown treatment agreed.
- [ ] Observation window defined.
- [ ] Currency and attribution date confirmed.
- [ ] Source and data owner identified.
- [ ] ID and MY applicability validated separately.
- [ ] Historical calculation tested.
- [ ] Dashboard label and limitations documented.

---

## 19. Final measurement principles

1. Payment attempt success is not billing collection success.
2. Billing value due is not collected value.
3. Failed billing exposure is not automatically lost revenue.
4. Recovery rate requires a mature and consistently defined failed-billing cohort.
5. Active subscribers require explicit state rules.
6. Renewal, persistency, lapse, and churn are related but distinct measures.
7. Settlement is not the same as payment success.
8. API acceptance is not proof of business completion.
9. Webhook delivery is not proof of successful event processing.
10. IDR and MYR must not be combined without an approved FX methodology.

**The objective is not to maximize the number of KPIs. It is to make every reported number explainable, reproducible, and actionable.**
