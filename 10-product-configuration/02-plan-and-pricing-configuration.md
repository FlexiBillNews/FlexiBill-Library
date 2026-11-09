# 02 — Plan & Pricing Configuration

## 1. Overview

Plan & Pricing Configuration defines what a merchant sells, how much the customer pays, and how billing is calculated and executed.

In FlexiBill, a Plan is configured within the Collection structure and establishes the commercial and billing rules associated with the merchant's offering.

The configuration journey is:

**Collection → Plan → Pricing → Customer / Member → Billing → Payment**

A well-designed Plan translates a merchant's commercial model into an operational billing configuration.

## 2. Business Purpose

Merchants use Plans to:

- Define products and services offered to customers.
- Establish pricing and billing frequency.
- Support recurring and fixed-duration billing arrangements.
- Configure different pricing structures.
- Organise commercial offerings for different customer segments.
- Connect billing configuration with customer acquisition and payment execution.

## 3. Collection vs Plan vs Pricing

| Component | Main question | Example |
|---|---|---|
| Collection | Which customer or billing programme is this for? | Gym Membership |
| Plan | What product or service is offered? | Premium Gym Membership |
| Pricing | How much and how is the customer charged? | Rp500,000 monthly |

Example:

A fitness merchant creates a Collection called "Gym Membership".

Within that Collection, the merchant offers:
- Basic Membership
- Premium Membership
- Corporate Membership

Each Plan can have its own pricing and billing configuration, subject to supported product rules.

## 4. Pricing Models

FlexiBill pricing configuration supports the following pricing structures in the documented product model. Confirm the availability and exact behaviour of each option in the relevant merchant dashboard and country before implementation.

### 4.1 Flat Fee

A fixed amount is charged for each billing period or configured billing event.

Example:

| Parameter | Value |
|---|---|
| Plan | Standard Membership |
| Price | Rp250,000 |
| Frequency | Monthly |
| Customer charge | Rp250,000 per billing period |

Suitable for:
- Memberships
- Insurance premiums with fixed amounts
- SaaS subscriptions
- Tuition fees
- Fixed service contracts

### 4.2 Per Unit

The amount is calculated based on a defined unit quantity.

Conceptual formula:

**Total Amount = Unit Price × Quantity**

Example:

| Parameter | Value |
|---|---:|
| Product | Software licences |
| Unit price | Rp100,000 |
| Quantity | 10 |
| Total | Rp1,000,000 |

Suitable for:
- Software licences
- Seats or user subscriptions
- Service units
- Equipment rental

Validate whether quantity entry, calculation, and billing generation are handled natively or by an external integration.

### 4.3 Tiered Pricing

Different unit-price bands apply to different quantity ranges.

Illustrative example:

| Usage range | Price per unit |
|---|---:|
| 1–10 | Rp100,000 |
| 11–50 | Rp90,000 |
| 51+ | Rp80,000 |

The precise calculation depends on whether the configured model is graduated or volume-based. Confirm the actual FlexiBill calculation behaviour before merchant implementation.

### 4.4 Volume Pricing

A single applicable unit price is determined by the total quantity band.

Illustrative example:

| Total quantity | Price per unit |
|---|---:|
| 1–10 | Rp100,000 |
| 11–50 | Rp90,000 |
| 51+ | Rp80,000 |

If the customer purchases 20 units, the applicable band may determine one unit price for all 20 units.

Validate the actual calculation rule in the product configuration.

### 4.5 Stairstep Pricing

A fixed amount applies to a defined quantity or usage range.

Illustrative example:

| Quantity range | Total charge |
|---|---:|
| 1–10 | Rp500,000 |
| 11–20 | Rp850,000 |
| 21–30 | Rp1,100,000 |

Suitable for:
- Service packages
- Operational bundles
- Tiered membership packages
- Contract-based service pricing

### 4.6 Open Amount

The amount is not necessarily fixed in advance and can be supplied or determined for an individual billing requirement.

Example:

A school issues different tuition bills for different students.

| Customer | Billing amount |
|---|---:|
| Student A | Rp1,500,000 |
| Student B | Rp1,750,000 |
| Student C | Rp2,000,000 |

Validate the amount-entry mechanism and whether it is supported through the dashboard, API, or another billing workflow.

## 5. Billing Frequency

Billing frequency determines how often a customer is billed.

Examples of common billing intervals:

| Frequency | Business example |
|---|---|
| Daily | Short-term service |
| Weekly | Weekly membership |
| Monthly | Gym membership |
| Quarterly | Insurance or service subscription |
| Annually | Annual membership |
| Custom interval | Contract-specific billing |

The exact available intervals and custom-frequency rules must be checked against the current product configuration.

## 6. Billing Duration and End Conditions

A merchant must define whether a Plan is intended to continue indefinitely or for a limited period.

Common commercial patterns:

**Unlimited recurring**
- Continues until cancellation or another applicable termination condition.

**Fixed number of charges**
- Ends after the configured number of billing events, if supported.

**Fixed end date**
- Ends at a defined date, subject to supported configuration.

Example:

| Parameter | Example |
|---|---|
| Plan | 12-Month Membership |
| Price | Rp300,000 |
| Frequency | Monthly |
| Duration | 12 billing cycles |
| Total scheduled amount | Rp3,600,000 |

The total above is illustrative and excludes taxes, discounts, fees, and failed-payment effects.

## 7. Step-by-Step Configuration Workflow

Use this as the merchant implementation sequence:

1. Open the FlexiBill merchant dashboard.
2. Select the relevant Collection.
3. Navigate to Plan management.
4. Create a new Plan.
5. Enter the Plan name and required information.
6. Select the applicable pricing model.
7. Configure the price or applicable pricing rules.
8. Configure billing frequency.
9. Configure duration or end conditions, where available.
10. Review the resulting commercial and billing configuration.
11. Save and validate the Plan.
12. Connect the Plan to the appropriate customer acquisition and billing workflow.

**UI validation requirement:** Exact field names, mandatory fields, available dropdown options, and save behaviour must be confirmed against the latest Indonesia and Malaysia dashboard interfaces.

## 8. Practical Merchant Configuration Examples

### Scenario A — Gym Membership

| Parameter | Configuration |
|---|---|
| Collection | Gym Membership |
| Plan | Premium |
| Pricing model | Flat Fee |
| Price | Rp500,000 |
| Frequency | Monthly |
| Duration | Unlimited, if supported |

Business objective: predictable monthly membership revenue.

### Scenario B — Education Tuition

| Parameter | Configuration |
|---|---|
| Collection | Student Tuition |
| Plan | Monthly Tuition |
| Pricing model | Open Amount or applicable fixed pricing |
| Amount | Student-specific |
| Frequency | Monthly |
| Duration | Academic period |

Business objective: organise recurring student billing.

### Scenario C — SaaS Licence

| Parameter | Configuration |
|---|---|
| Collection | Business SaaS |
| Plan | Business Licence |
| Pricing model | Per Unit |
| Unit price | Rp100,000 |
| Quantity | 10 seats |
| Frequency | Monthly |

Business objective: charge based on licence quantity.

### Scenario D — Annual Membership

| Parameter | Configuration |
|---|---|
| Collection | Annual Membership |
| Plan | Annual Premium |
| Pricing model | Flat Fee |
| Price | Rp3,000,000 |
| Frequency | Annually |
| Duration | Unlimited or fixed-term, as required |

Business objective: collect annual membership fees.

## 9. Discounts, Coupons and Taxes

Pricing configuration should be considered together with applicable discounts, coupons, and taxes.

Typical commercial requirements:

- Promotional discounts.
- Campaign pricing.
- Customer-specific pricing.
- Tax-inclusive or tax-exclusive presentation.
- One-time or recurring discounts, where supported.

Important: Do not assume that every discount or tax rule can be applied to every pricing model or billing channel. Confirm the supported configuration and calculation order.

## 10. Pricing Table Relationship

Plans and pricing can support customer-facing product presentation through Pricing Table.

A typical journey:

1. Merchant configures Collection.
2. Merchant creates Plan and pricing.
3. Merchant publishes the applicable Pricing Table.
4. Customer views the offering.
5. Customer proceeds through the configured registration and payment journey.
6. FlexiBill manages the resulting billing relationship according to the configured setup.

Pricing Table capabilities and limitations are documented separately in Playbook 03.

## 11. Common Configuration Risks

| Risk | Recommended control |
|---|---|
| Incorrect price | Validate commercial approval before publication |
| Wrong frequency | Confirm the merchant's billing agreement |
| Incorrect duration | Test expected final billing event |
| Incorrect quantity calculation | Validate calculation with test cases |
| Incorrect pricing tier | Test boundary quantities |
| Tax or discount mismatch | Reconcile displayed and charged amounts |
| Country availability assumption | Validate ID and MY independently |
| Unsupported usage calculation | Confirm whether external calculation is required |

## 12. Testing Scenarios

Before go-live, validate:

1. Flat Fee with one billing cycle.
2. Flat Fee with multiple billing cycles.
3. Per Unit with quantity one.
4. Per Unit with multiple quantities.
5. Tiered pricing at a lower boundary.
6. Tiered pricing at an upper boundary.
7. Volume pricing with quantities across bands.
8. Stairstep pricing across multiple ranges.
9. Open Amount with different customer amounts.
10. Fixed-term billing and final billing behaviour.
11. Applicable coupon and tax behaviour.
12. Successful and failed payment outcomes.

## 13. KPIs and Monitoring

Recommended monitoring dimensions:

- Number of Plans created.
- Number of active customers per Plan.
- Active recurring billing amount.
- Average revenue per subscriber.
- Average ticket size.
- Upgrade and downgrade rates.
- Renewal success rate.
- Failed billing rate.
- Revenue by Plan and pricing model.
- Customer churn by Plan.

These are recommended business metrics; native report availability should be verified separately.

## 14. Indonesia and Malaysia Considerations

| Area | Validation requirement |
|---|---|
| Pricing models | Confirm country-level availability |
| Billing frequency | Confirm supported intervals |
| Currency | Confirm merchant account and transaction currency rules |
| Tax | Confirm applicable local tax configuration |
| Payment methods | Validate available channels and recurring eligibility |
| API | Confirm country-specific API support |
| Merchant eligibility | Confirm account and product prerequisites |

Do not assume full feature parity between Indonesia and Malaysia.

## 15. Related Playbooks

1. [Collection Management](01-collection-management.md)
2. [Pricing Table](03-pricing-table.md)
3. [Member Center](04-member-center.md)
4. [Billing Portal](05-billing-portal.md)
5. [Account Billing](06-account-billing.md)
6. [Subscription Lifecycle](07-subscription-lifecycle.md)
7. [Payment Management](08-payment-management.md)

## 16. Document Governance

- Document: Plan & Pricing Configuration
- Product: DOKU FlexiBill
- Category: Product Configuration
- Country scope: Indonesia and Malaysia
- Status: Working playbook — product behaviour and country validation required
- Owner: FlexiBill Product
- Last reviewed: 9 November 2026

---

*Internal DOKU knowledge base. Illustrative examples are not a substitute for confirmed product configuration rules. Refer to approved product and technical documentation before merchant implementation.*
