# Fitness & Gym Membership — Merchant Implementation Recipe

**Phase:** 3 — Merchant Implementation Recipes  
**Use case ID:** MER-001  
**Product:** DOKU FlexiBill  
**Target markets:** Indonesia (ID) and Malaysia (MY)  
**Audience:** Sales, Product, Partnership, Implementation, Engineering, Operations  
**Status:** Reference solution — validate all capabilities, payment methods, and country eligibility before merchant commitment.

---

## 1. Executive Summary

### Business scenario

A fitness business wants to move from manual membership administration and payment collection to a structured recurring membership model.

The merchant needs to:

- Sell gym memberships online and offline.
- Offer different membership packages.
- Collect joining fees and recurring membership charges.
- Register and identify members.
- Support recurring auto-debit where eligible.
- Provide customers with billing and payment information.
- Monitor successful and failed collections.
- Recover failed payments.
- Run promotions and membership campaigns.
- Reduce manual reconciliation and collection effort.

### Proposed solution

Use FlexiBill as the merchant's billing and payment orchestration layer.

The proposed solution combines:

| FlexiBill component | Role in the fitness solution |
|---|---|
| Collection | Organize membership customers and billing relationships |
| Plan | Define membership products and commercial rules |
| Pricing | Define membership prices and billing frequency |
| Pricing Table | Present packages and support customer acquisition |
| Member Center | Associate customer identity with membership relationships |
| Subscription | Represent the recurring membership arrangement |
| Billing Automation / supported integration | Generate and manage billing according to the selected operating model |
| Payment Management | Collect payments and manage payment outcomes |
| Billing Portal | Provide supported customer billing visibility and self-service |
| Reporting / reconciliation | Monitor collections, failures, and outstanding amounts |

This is a solution design, not a claim that every customer action or lifecycle transition is available natively.

## 2. Merchant profile

### Example merchant

**Merchant:** FitLife Gym  
**Business:** Multi-branch fitness club  
**Target customers:** Individual members, families, corporate employees  
**Business model:** Joining fee + recurring membership fee + optional services

### Current merchant problems

| Problem | Business impact |
|---|---|
| Manual membership registration | Slow onboarding |
| Manual recurring payment follow-up | High operational workload |
| Failed card or bank collections | Revenue leakage |
| No consolidated membership billing view | Difficult operations |
| Limited customer self-service | More support requests |
| Manual promotion management | Slow campaign execution |
| Fragmented member and payment records | Reconciliation complexity |

### Desired business outcomes

1. Increase membership conversion.
2. Increase recurring collection success.
3. Reduce failed-payment leakage.
4. Reduce manual collection effort.
5. Improve customer billing visibility.
6. Increase retention and membership lifetime value.
7. Enable scalable membership operations across branches.

## 3. Membership product design

Before configuring FlexiBill, define the merchant's commercial catalogue.

### Example membership catalogue

All values below are illustrative.

| Package | Monthly price | Commitment | Target segment |
|---|---:|---|---|
| Basic | Rp350,000 | Monthly | Entry-level members |
| Standard | Rp500,000 | Monthly | Regular gym users |
| Premium | Rp750,000 | Monthly | Premium facilities |
| Annual | Rp5,000,000 | Annual or agreed installment model | Long-term members |
| Corporate | Negotiated | Contract-based | Corporate customers |

Additional commercial items may include:

- Joining fee.
- Personal training.
- Group classes.
- Locker rental.
- Fitness assessment.
- Merchandise.
- Special access packages.

Do not assume these items can all be combined into one native multi-product subscription. Validate the required pricing and billing design.

### Commercial policy decisions

The merchant must define:

| Decision | Example |
|---|---|
| Joining fee | One-time Rp150,000 |
| Membership price | Rp500,000 per month |
| First billing date | At enrollment or agreed start date |
| Recurring date | Configured billing schedule |
| Contract term | Monthly or 12 months |
| Renewal | Continue until cancellation or end condition |
| Trial | 7 days, if supported and configured |
| Cancellation | Immediate or end of paid period |
| Upgrade | Change to a higher package |
| Downgrade | Change to a lower package |
| Failed payment | Notify, recover, and apply merchant policy |

## 4. Solution architecture

### Conceptual architecture

```text
                  CUSTOMER
                     |
                     v
             PRICING TABLE / SALES
                     |
                     v
              REGISTRATION FLOW
                     |
                     v
                MEMBER CENTER
                     |
                     v
             MEMBERSHIP SUBSCRIPTION
                     |
                     v
              COLLECTION / PLAN
                     |
                     v
                BILLING ENGINE
                     |
                     v
              PAYMENT MANAGEMENT
                     |
             +-------+-------+
             |               |
             v               v
          SUCCESS          FAILURE
             |               |
             v               v
       PAID BILLING       RECOVERY
             |               |
             +-------+-------+
                     |
                     v
               BILLING PORTAL
                     |
                     v
             MERCHANT OPERATIONS
                     |
                     v
            REPORTING / RECONCILIATION
```

### Integration responsibility

The architecture must explicitly define:

- Who owns the member record.
- Who creates the subscription.
- Who calculates membership charges.
- Who controls the billing schedule.
- Who initiates collection.
- Which system receives payment results.
- Who controls gym access and member privileges.

FlexiBill should not be assumed to operate the gym's physical access-control system. That may require a separate integration.

## 5. Merchant configuration blueprint

### Step 1 — Create the Collection structure

Example:

| Collection | Purpose |
|---|---|
| FitLife Jakarta | Jakarta membership customers |
| FitLife Bandung | Bandung membership customers |
| FitLife Corporate | Corporate membership relationships |
| FitLife Annual | Annual membership segment |

The actual Collection design should reflect the merchant's operational and reporting requirements.

Avoid creating excessive Collections when a simpler customer grouping or merchant reporting structure is sufficient.

### Step 2 — Configure membership Plans

Example:

| Plan | Commercial description |
|---|---|
| Basic Membership | Access to basic facilities |
| Standard Membership | Standard facility access |
| Premium Membership | Premium facilities and classes |
| Annual Membership | Annual membership arrangement |
| Corporate Membership | Contract-based employee membership |

### Step 3 — Configure Pricing

Illustrative configuration:

| Plan | Pricing model | Amount | Frequency |
|---|---|---:|---|
| Basic | Flat Fee | Rp350,000 | Monthly |
| Standard | Flat Fee | Rp500,000 | Monthly |
| Premium | Flat Fee | Rp750,000 | Monthly |
| Annual | Flat Fee | Rp5,000,000 | Annual |
| Corporate | Contract-defined | Negotiated | Contract-defined |

Validate exact frequency, duration, first billing, end-condition, and pricing fields in the current environment.

### Step 4 — Configure customer acquisition

Use the Pricing Table as an offer presentation and acquisition entry point where supported.

Potential channels:

- Merchant website.
- Social media.
- Email campaigns.
- QR codes in gym branches.
- Digital advertising.
- Merchant landing pages.
- Supported embedded checkout experiences.

Validate whether each channel supports the required customer journey and payment behavior.

### Step 5 — Configure Member Center

Define:

- Member ID.
- Full name.
- Email address.
- Mobile number.
- Selected membership package.
- Branch.
- Membership start date.
- Membership status.
- Subscription or account reference.

Only collect information required for the merchant's business and approved data-handling process.

**Important:** Member Center API availability and customer-facing registration frontend availability must be validated separately.

### Step 6 — Establish the subscription

Define:

- Customer/member association.
- Selected membership Plan and Pricing.
- Subscription start date.
- First billing treatment.
- Recurring frequency.
- Duration or end condition.
- Payment-method association.
- Applicable authorization.

Validate the exact subscription creation workflow and whether it is merchant-operated, API-driven, or supported through a customer checkout journey.

### Step 7 — Configure payment collection

The merchant chooses eligible payment methods according to country, channel, merchant eligibility, and customer authorization.

Potential requirements:

- Recurring auto-debit.
- One-time payment.
- Payment for outstanding invoices.
- Payment-method update.
- Customer notification.
- Failed-payment recovery.

Do not assume that a payment method available for one-time checkout is eligible for recurring auto-debit.

### Step 8 — Configure Billing Portal

Define the customer information required:

- Membership
