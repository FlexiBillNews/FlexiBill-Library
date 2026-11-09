# FlexiBill Cohort, Renewal & Persistency Analysis

**Document type:** Subscriber Analytics, Cohort Performance & Retention Playbook  
**Audience:** Product, Business, Analytics, Merchant Success, Operations, Finance  
**Markets:** Indonesia (ID) and Malaysia (MY)  
**Status:** Proposed analytical framework — validate source data, merchant lifecycle rules, and cohort definitions before reporting

---

## 1. Purpose

This playbook defines how FlexiBill should measure recurring billing performance beyond monthly transaction success.

The objective is to understand whether customers and billing obligations continue over time, and why they stop.

It answers:

- How many new billing records appear each month?
- How many continue into subsequent periods?
- How many successfully renew?
- How many fail but later recover?
- How many upgrade or downgrade?
- How many cancel or expire?
- How many become lapsed?
- Which merchant, product, plan, or payment method has the strongest persistency?
- How much recurring billing value is retained or lost?

**Core principle:** Recurring business quality must be measured across time. A successful payment in one month does not prove long-term subscription retention.

## 2. Key analytical concepts

| Concept | Definition |
|---|---|
| Cohort | A group of entities sharing a defined first-observed event or start period |
| New business | Entity meeting the approved first-seen definition during the period |
| Renewal | Continuation into a subsequent expected billing period |
| Persistency | Continued existence or qualifying renewal of a cohort over time |
| Retention | Share of an eligible starting cohort that remains active under a defined rule |
| Failed renewal | Expected renewal collection with a definitive failed outcome |
| Recovered renewal | Initially failed renewal subsequently paid within the observation window |
| Cancellation | Subscription or billing relationship ended under the applicable merchant process |
| Expiry | Subscription or billing validity reached its configured end |
| Lapse | Entity no longer qualifies as continuing under the approved lapse rule |
| Upgrade | Continued relationship with a higher comparable recurring amount |
| Downgrade | Continued relationship with a lower comparable recurring amount |

Definitions must be consistent across reporting periods.

## 3. Entity and grain selection

A major analytical risk is confusing Billing ID with Subscriber ID.

| Entity | What it represents | Appropriate use |
|---|---|---|
| Billing ID | A billing obligation or billing record | Billing cohort and billing renewal analysis |
| Subscriber / Member ID | A customer membership identity | Subscriber acquisition and retention |
| Subscription ID | A subscription relationship | Subscription lifecycle and plan movement |
| Transaction ID | A payment transaction | Payment performance |
| Merchant ID | Merchant account | Merchant-level performance |
| Plan / Collection ID | Commercial configuration | Product and plan analysis |

**Important:** A unique Billing ID may represent one billing obligation, not one unique customer. Use Subscriber ID or Subscription ID for customer-level persistency where the source data supports it.

If only Billing ID is available, label the output as billing-level cohort analysis. Do not call it customer retention without a validated customer identifier.

## 4. New business definition

For the internal monthly analysis framework:

**New business = unique Billing ID that first appears in the relevant month's dataset.**

Procedure:
1. Combine the available monthly source periods.
2. Normalize Billing ID format.
3. Identify the earliest valid appearance of each Billing ID.
4. Assign the Billing ID to its first-seen month.
5. Count each Billing ID once in its cohort.
6. Retain the first-seen amount and relevant merchant attributes.
7. Check for duplicate records and source coverage.

### Critical limitation

This definition measures new Billing IDs appearing in the dataset. It does not necessarily measure new subscribers or new subscriptions.

For true subscription acquisition reporting, use the validated first activation date and unique Subscriber ID or Subscription ID.

## 5. Cohort construction

A cohort can be created using:

- First-seen Billing ID month.
- Subscription activation month.
- First successful payment month.
- First billing generation month.
- Merchant onboarding month.

Choose one definition for each analytical question.

### Recommended cohort structure

| Cohort attribute | Example |
|---|---|
| Cohort month | January 2026 |
| Merchant | Merchant A |
| Product | Insurance Premium |
| Plan | Monthly Premium |
| Billing cycle | Monthly |
| Starting population | 1,000 eligible entities |
| Starting value | IDR 1,500,000,000 |

Track the same eligible cohort into subsequent expected periods.

## 6. Cohort renewal matrix

A standard renewal matrix shows what happens to each cohort over time.

Illustrative example:

| Cohort | Month 0 | Month 1 | Month 2 | Month 3 | Month 4 |
|---|---:|---:|---:|---:|---:|
| January | 1,000 | 920 | 870 | 820 | 790 |
| February | 1,100 | 990 | 930 | 890 | — |
| March | 950 | 860 | 810 | — | — |
| April | 1,200 | 1,080 | — | — | — |

The figures above are illustrative, not actual FlexiBill performance.

The denominator must remain the original eligible cohort population when calculating cohort retention.

### Cohort retention formula

\[
\text{Cohort Retention}_{n}
=
\frac{\text{Eligible Cohort Entities Continuing at Period }n}
{\text{Original Eligible Cohort Population}}
\times 100\%
\]

Define whether "continuing" means:
- Active subscription state.
- Valid billing generated.
- Successful renewal.
- Paid within grace period.
- Any other merchant-approved event.

Do not mix these definitions in one metric.

## 7. Renewal outcome classification

Every eligible expected renewal should be assigned an outcome.

| Outcome | Meaning |
|---|---|
| Paid on time | Successful collection within the expected window |
| Paid late | Successful collection after due date but within an allowed window |
| Failed, recoverable | Failed collection but still within recovery or grace window |
| Pending | Final outcome is unresolved |
| Cancelled | Subscription or billing relationship cancelled |
| Expired | Subscription reached configured expiry |
| Lapsed | No longer qualifies as continuing under the approved lapse rule |
| Upgraded | Continued with a higher comparable amount |
| Downgraded | Continued with a lower comparable amount |
| Unknown | Insufficient data to classify |

A pending record must not be counted as a definitive failure or lapse.

An entity still inside an allowed grace period should not be classified as lapsed prematurely.

## 8. Renewal and persistency metrics

### 8.1 Renewal rate

\[
\text{Renewal Rate}
=
\frac{\text{Eligible Renewals Completed}}
{\text{Eligible Renewals Due}}
\times 100\%
\]

Specify whether late recovery is included and the observation cutoff.

### 8.2 Persistency rate

\[
\text{Persistency Rate}_{n}
=
\frac{\text{Original Cohort Entities Still Qualifying at }n}
{\text{Original Eligible Cohort Population}}
\times 100\%
\]

The qualifying condition must be documented.

### 8.3 Lapse rate

\[
\text{Lapse Rate}
=
\frac{\text{Eligible Entities Classified as Lapsed}}
{\text{Eligible Entities Subject to Lapse Classification}}
\times 100\%
\]

Exclude entities that have not reached the required observation period.

### 8.4 Cancellation rate

\[
\text{Cancellation Rate}
=
\frac{\text{Eligible Cancellations During Period}}
{\text{Defined Active Population}}
\times 100\%
\]

Define whether the denominator is opening active population, average active population, or another approved base.

### 8.5 Recovery rate

\[
\text{Renewal Recovery Rate}
=
\frac{\text{Initially Failed Renewals Subsequently Paid}}
{\text{Eligible Initially Failed Renewals}}
\times 100\%
\]

Use a consistent recovery observation window.

### 8.6 Amount persistency

\[
\text{Amount Persistency}_{n}
=
\frac{\text{Comparable Recurring Amount Retained at }n}
{\text{Original Cohort Recurring Amount}}
\times 100\%
\]

Use comparable currency and billing basis. Separate genuine plan changes from changes caused by tax, fees, or currency conversion.

## 9. Upgrade and downgrade analysis

A continuing customer may change the recurring amount.

Classify movements:

| Movement | Definition |
|---|---|
| Same amount | Comparable recurring amount unchanged |
| Upgrade | Comparable recurring amount increases |
| Downgrade | Comparable recurring amount decreases |
| New add-on | Additional recurring charge, if supported |
| Removed component | Recurring amount decreases due to component removal |
| Adjustment | Change caused by tax, discount, correction, or other non-plan reason |
| Unknown | Reason for movement cannot be established |

### Amount movement formula

\[
\text{Amount Change}
=
\text{Current Comparable Amount}
-
\text{Previous Comparable Amount}
\]

\[
\text{Amount Change \%}
=
\frac{\text{Amount Change}}
{\text{Previous Comparable Amount}}
\times 100\%
\]

Only compare amounts with consistent:
- Currency.
- Billing interval.
- Tax treatment.
- Discount treatment.
- Product scope.
- Pricing basis.

A monthly amount and an annual amount cannot be compared directly without normalization.

## 10. Lapse analysis and grace-period rules

Lapse rules are merchant- and product-specific.

For bancassurance analysis, a roughly 90-day grace convention may be relevant to particular portfolios. It must not be generalized to every insurance merchant or product.

### Recommended lapse logic

1. Identify the expected renewal date.
2. Identify the merchant-approved grace period.
3. Track failed and pending collection outcomes.
4. Check for successful recovery during the grace period.
5. Confirm cancellation, expiry, or other terminal event where available.
6. Classify as lapsed only when the approved rule is satisfied.
7. Preserve the lapse effective date and evidence.

### Example

A monthly premium is due on 1 January. The merchant-approved grace period is 90 days.

The entity should not automatically be counted as lapsed immediately after the January payment failure. The classification depends on the actual merchant rule, payment history, and applicable effective date.

The 90-day example is illustrative, not a universal DOKU or FlexiBill rule.

## 11. Billing ID cohort analysis workflow

For datasets using Billing ID as the primary key:

### Step 1 — Prepare source data

- Standardize Billing ID.
- Standardize merchant and customer references.
- Normalize date and timestamp fields.
- Preserve original currency.
- Remove exact duplicate source rows.
- Retain valid payment and billing status history.

### Step 2 — Identify first appearance

For each Billing ID, find the earliest valid month in which it appears.

### Step 3 — Assign cohort

Assign each unique Billing ID to its first-seen month.

### Step 4 — Track subsequent periods

Determine whether the same Billing ID appears in subsequent monthly datasets.

### Step 5 — Classify movement

Classify:
- Continues.
- Stops appearing.
- Amount increases.
- Amount decreases.
- Payment failure.
- Recovery.
- Unknown.

### Step 6 — Validate interpretation

Check whether recurring billing creates new Billing IDs for each cycle.

If each cycle creates a new Billing ID, tracking the same Billing ID across months will not measure subscription persistency. Use Subscriber ID or Subscription ID to connect billing obligations across cycles.

This validation is essential before drawing retention conclusions.

## 12. Insurance and bancassurance analysis

Insurance recurring collection requires additional context.

Recommended dimensions:
- Insurer.
- Bancassurance partner.
- Bank.
- Product.
- Premium amount band.
- Payment method.
- Card issuer or bank, where permitted.
- Billing cycle.
- First-seen cohort.
- Renewal period.
- Grace period.
- Lapse status.

### Key questions

- Which insurer has the highest renewal rate?
- Which bank or payment method has the highest collection success?
- How much premium value is retained?
- Which premium bands have high failure or lapse?
- How much failed premium value is recovered?
- Which cohorts are approaching lapse?
- How much business is lost after the grace period?

Separate collection failure from policy cancellation and formal lapse. These may have different effective dates and owners.

## 13. Non-insurance subscription analysis

For SaaS, education, fitness, travel, and other recurring models, tailor the cohort rules.

| Vertical | Useful cohort and lifecycle dimensions |
|---|---|
| SaaS | Activation, plan, seat count, renewal, churn |
| Fitness | Membership start, membership type, attendance, renewal |
| Education | Enrollment, term, course, tuition cycle, continuation |
| Travel / hospitality | Booking, membership, stay or service period |
| Retail membership | Member activation, benefits usage, renewal |
| Community membership | Group, member status, contribution cycle |

Do not apply insurance grace-period logic to other verticals.

## 14. Analytical segmentation

Segment cohorts by:
- Merchant.
- Market.
- Industry.
- Product and plan.
- Billing interval.
- Billing amount band.
- Payment method.
- Issuer or bank, where available.
- Customer acquisition channel.
- Integration model.
- First successful payment.
- Renewal failure reason.

Use minimum sample-size thresholds before presenting granular comparisons.

Small cohorts can produce misleading percentages.

## 15. Recommended visualizations

| Business question | Visualization |
|---|---|
| Are cohorts continuing? | Cohort retention heatmap |
| Which month has the strongest renewal? | Monthly renewal trend |
| How many subscribers lapse? | Lapse funnel |
| How many recover after failure? | Recovery cohort chart |
| Are amounts increasing or decreasing? | Upgrade / downgrade waterfall |
| Which merchants retain best? | Merchant persistency ranking |
| Which premium bands lapse most? | Amount-band heatmap |
| When do cohorts stop renewing? | Survival-style retention curve |

Label every chart with the entity grain, observation period, and denominator.

## 16. Management interpretation framework

A useful cohort report should explain not only what changed, but why.

| Observed pattern | Possible interpretation | Investigation |
|---|---|---|
| High first-period drop | Acquisition quality or first renewal friction | Registration, pricing, payment setup |
| Gradual decline | Ongoing churn or payment failure | Cohort and merchant lifecycle |
| Sudden decline in one month | Product, policy, or operational event | Incident and merchant changes |
| High failure but later recovery | Recoverable payment friction | Dunning and payment methods |
| High downgrade rate | Affordability or product-fit issue | Plan and pricing changes |
| High lapse after grace period | Unresolved renewal failures | Recovery and merchant follow-up |
| Stable subscriber count but falling value | Downgrade or lower-value mix | Amount movement and product mix |

These are hypotheses to investigate, not causal conclusions from a chart alone.

## 17. Data quality and analytical controls

Before publishing results, validate:

- [ ] Unique identifier is appropriate for the analysis.
- [ ] Billing ID is not mistaken for Subscriber ID.
- [ ] First-seen date is correctly determined.
- [ ] Duplicate records are handled.
- [ ] Monthly source coverage is consistent.
- [ ] Billing cycles are normalized.
- [ ] Pending outcomes remain unresolved.
- [ ] Grace periods are merchant-specific.
- [ ] Lapse effective date is validated.
- [ ] Upgrade and downgrade use comparable amounts.
- [ ] Currency is consistent or conversion is documented.
- [ ] Cohort observation windows are mature.
- [ ] Missing source periods are identified.
- [ ] ID and MY are validated independently.

## 18. Recommended monthly cohort report

Every monthly report should include:

### Executive summary
- New cohort population.
- Eligible renewal population.
- Renewal rate.
- Persistency trend.
- Lapsed population.
- Recovered renewals.
- Amount retained.
- Amount upgraded and downgraded.

### Merchant breakdown
- Top merchants by cohort size.
- Best and weakest persistency.
- Highest lapse exposure.
- Highest recovery opportunity.

### Product breakdown
- Product and plan performance.
- Billing interval performance.
- Amount-band performance.
- Payment-method performance.

### Action plan
- At-risk cohorts.
- High-value failed renewals.
- Merchant intervention.
- Payment recovery opportunities.
- Data quality issues.
- Product improvement opportunities.

## 19. Final principles

1. Define the analytical entity before calculating retention.
2. Use Billing ID first-seen cohorts only for billing-level analysis unless identity linkage is validated.
3. Use Subscriber ID or Subscription ID for true subscriber or subscription persistency.
4. Track renewal outcomes across time, not only monthly totals.
5. Separate failed, pending, recovered, cancelled, expired, and lapsed outcomes.
6. Apply grace periods only where merchant policy supports them.
7. Compare recurring amounts on a like-for-like basis.
8. Preserve original currency and country context.
9. Do not interpret correlation as causation.
10. Translate cohort findings into merchant and product actions.

**The objective is to understand the durability of FlexiBill-enabled recurring business: not just how much is collected today, but how much of the customer and billing base continues tomorrow.**
