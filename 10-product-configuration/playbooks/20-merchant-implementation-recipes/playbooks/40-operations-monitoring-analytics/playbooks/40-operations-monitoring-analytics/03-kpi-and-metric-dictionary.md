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
5. Value confirmed
