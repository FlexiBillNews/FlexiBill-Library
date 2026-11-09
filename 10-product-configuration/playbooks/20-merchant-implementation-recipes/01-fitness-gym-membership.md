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

- Membership billing overview.
- Current billing status.
- Invoice or bill details, where supported.
- Payment status.
- Available payment actions.
- Payment-method management, if supported.
- Support contact.

Validate each customer self-service function independently.

## 6. End-to-end customer journey

### Journey A — New membership acquisition

```text
CUSTOMER DISCOVERS GYM OFFER
          |
          v
SELECT MEMBERSHIP PACKAGE
          |
          v
ENTER CUSTOMER DETAILS
          |
          v
REGISTER / IDENTIFY MEMBER
          |
          v
COMPLETE CHECKOUT / PAYMENT SETUP
          |
          v
SUBSCRIPTION CREATED
          |
          v
ACTIVATION CONDITION MET
          |
          v
MEMBERSHIP STARTS
          |
          v
CUSTOMER RECEIVES CONFIRMATION
```

The merchant must define whether membership activation occurs after subscription creation, successful first payment, or another approval event.

### Journey B — Recurring membership collection

```text
BILLING DATE REACHED
          |
          v
BILLING OBLIGATION CREATED
          |
          v
PAYMENT COLLECTION INITIATED
          |
          v
PAYMENT RESULT
       /       \
      /         \
 SUCCESS       FAILURE
   |              |
   v              v
UPDATE PAID     CLASSIFY FAILURE
STATUS              |
   |                v
   |           RECOVERY PROCESS
   |                |
   +--------+-------+
            |
            v
     UPDATE CUSTOMER
       BILLING STATUS
```

### Journey C — Failed payment recovery

1. Scheduled collection fails.
2. The failure is classified.
3. Customer is notified through the supported channel.
4. Eligible retries follow the approved policy.
5. Customer updates payment details if necessary.
6. Successful recovery updates the billing record.
7. Unrecovered billing follows the merchant's overdue or suspension policy.

Do not promise a specific retry schedule until the payment-method and product configuration are confirmed.

## 7. Customer experience design

### Customer-facing interface roles

| Interface | Customer purpose |
|---|---|
| Pricing Table | Discover and select membership offers |
| Registration journey | Submit required member information |
| Member Center | Establish or manage the customer/member relationship |
| Checkout/payment flow | Complete the initial payment or authorization |
| Billing Portal | Review supported billing information and actions |
| Notification channel | Receive billing reminders and payment results |

### Suggested customer experience principles

- Make the membership price and billing frequency clear.
- Explain joining fees separately from recurring charges.
- Disclose trial terms and first-charge dates.
- Obtain appropriate authorization for recurring collection.
- Show customers how to contact the merchant.
- Explain payment failures and next steps.
- Avoid implying that membership access is active before the merchant's activation condition is met.

## 8. Membership lifecycle management

| Lifecycle event | Merchant action | Product validation |
|---|---|---|
| New member | Create member relationship | Confirm Member Center workflow |
| First payment | Confirm collection outcome | Confirm payment-status mapping |
| Membership activation | Enable gym access | Confirm activation event and external access integration |
| Monthly renewal | Generate next billing obligation | Confirm recurring schedule |
| Payment failure | Apply recovery policy | Confirm retry and status handling |
| Upgrade | Apply new package | Confirm plan-change behavior |
| Downgrade | Apply lower package | Confirm effective date and adjustment |
| Pause | Temporarily restrict membership | Confirm service and billing behavior separately |
| Resume | Reactivate membership | Confirm billing restart rules |
| Cancellation | End future membership arrangement | Confirm termination behavior |
| Expiration | End fixed-term membership | Confirm end-condition handling |

## 9. Promotions and acquisition campaigns

Fitness merchants frequently use promotions to improve acquisition and retention.

Illustrative campaign ideas:

| Campaign | Commercial design | Validation |
|---|---|---|
| First month discount | Discount first billing period | Confirm coupon and discount rules |
| Joining fee waiver | Waive one-time joining fee | Confirm pricing structure |
| Annual membership offer | Discount annual package | Confirm annual billing model |
| Referral promotion | Reward eligible referrals | Confirm campaign and external referral tracking |
| Pay 12, get 1 month free | Promotional membership duration or price adjustment | Validate exact implementation; do not assume automatic entitlement handling |
| Trial membership | Limited free period before paid billing | Confirm trial configuration and first-charge behavior |

Promotion rules should specify:
- Eligibility.
- Start and end date.
- Number of redemptions.
- Applicable Plans.
- Discount amount or percentage.
- First-cycle versus ongoing discount.
- Stacking rules.
- Customer communication.

## 10. Failed-payment and revenue-leakage management

### Key business problem

A failed collection can lead to unpaid membership revenue, increased manual follow-up, and potential customer churn.

The merchant should monitor failure by:

- Membership package.
- Payment method.
- Bank or issuer, where available.
- Billing period.
- Branch.
- Customer cohort.
- Failure category.
- Number of attempts.
- Recovered versus unrecovered amount.

### Example operational dashboard

| Metric | Example value |
|---|---:|
| Active members | 5,000 |
| Members due for billing | 4,000 |
| Successful first collections | 3,400 |
| Failed first collections | 600 |
| First-attempt success rate | 85% |
| Recovered after failure | 300 |
| Unrecovered | 300 |

All figures are illustrative.

### Core calculations

First-attempt success rate:

`Successful first attempts / Total first attempts × 100`

Recovery rate:

`Failed billing obligations subsequently recovered / Eligible failed billing obligations × 100`

Outstanding value:

`Total amount still unpaid at the reporting cut-off`

Use billing-obligation-level calculations for recovery, not payment-attempt-level calculations.

## 11. Merchant operational dashboard

Recommended reporting views:

| Dashboard | Key information |
|---|---|
| Membership overview | New, active, suspended, cancelled, expired |
| Package performance | Members and revenue by package |
| Upcoming billing | Members due and expected billing amount |
| Payment performance | Attempts, success, failure |
| Recovery | Recovered amount and remaining unpaid amount |
| Retention | Renewal, churn, lapse |
| Campaign performance | Offer views, registrations, conversion |
| Branch performance | Membership and collection performance by branch |

Confirm which reports are available natively and which require merchant-side aggregation or integration.

## 12. Merchant value proposition

| Value dimension | Potential benefit |
|---|---|
| Revenue collection | More structured recurring collection |
| Operations | Less manual billing administration |
| Customer experience | Clearer billing and payment journey |
| Retention | Better visibility into renewal and failed-payment risk |
| Acquisition | Digital membership offer distribution |
| Financial control | Better billing-to-payment reconciliation |
| Scalability | Repeatable configuration across branches |

These are intended business outcomes, not guaranteed performance improvements. Establish baseline metrics and measure results after launch.

## 13. Indonesia and Malaysia considerations

Validate the solution separately for each country.

| Area | Indonesia | Malaysia |
|---|---|---|
| Merchant onboarding | Confirm eligibility | Confirm eligibility |
| Collection and Plan setup | Validate current configuration | Validate current configuration |
| Pricing Table | Validate supported customer journey | Validate supported customer journey |
| Member Center API | Confirm current scope | Confirm current scope |
| Member Center frontend | Confirm separately | Confirm separately |
| Billing Portal | Confirm supported functions | Confirm supported functions |
| Recurring card | Confirm eligibility and authorization | Confirm eligibility and authorization |
| Bank-based auto-debit | Confirm available channels | Confirm available channels |
| QR and one-time payment | Confirm supported methods | Confirm supported methods |
| Retry and recovery | Confirm payment-method rules | Confirm payment-method rules |
| Tax and currency | Confirm local configuration | Confirm local configuration |
| Reporting | Confirm available fields and exports | Confirm available fields and exports |

Do not assume that a merchant solution configured in Indonesia can be replicated in Malaysia without country-specific validation.

## 14. Implementation test plan

| Test ID | Scenario | Acceptance criteria |
|---|---|---|
| FIT-001 | Create membership Collection | Correct merchant grouping |
| FIT-002 | Configure membership Plan | Correct product definition |
| FIT-003 | Configure monthly pricing | Correct amount and billing frequency |
| FIT-004 | Publish Pricing Table offer | Correct offer and customer journey |
| FIT-005 | Register member | Correct identity association |
| FIT-006 | Create subscription | Correct Plan, price, and customer relationship |
| FIT-007 | First payment success | Correct payment and activation handling |
| FIT-008 | First payment failure | Correct failure handling |
| FIT-009 | Recurring renewal | Correct next billing event |
| FIT-010 | Failed renewal | Correct recovery workflow |
| FIT-011 | Payment-method update | Correct customer and subscription mapping |
| FIT-012 | Upgrade membership | Correct effective date and amount |
| FIT-013 | Cancel membership | Future billing follows approved policy |
| FIT-014 | Billing Portal access | Customer sees only permitted information |
| FIT-015 | Reconciliation | Payment outcome matches billing record |
| FIT-016 | Duplicate event | No unintended duplicate collection or state change |

## 15. Go-live checklist

### Commercial
- [ ] Membership packages approved.
- [ ] Prices and billing frequencies approved.
- [ ] Joining fees and promotions documented.
- [ ] Trial and cancellation policies approved.

### Product configuration
- [ ] Collection structure validated.
- [ ] Plans and Pricing configured.
- [ ] Pricing Table tested.
- [ ] Member Center workflow validated.
- [ ] Subscription creation tested.
- [ ] Billing Portal scope confirmed.

### Payment
- [ ] Payment methods confirmed.
- [ ] Customer authorization tested.
- [ ] Recurring collection tested.
- [ ] Failure and recovery policy approved.
- [ ] Payment-method update flow tested.

### Operations
- [ ] Member activation process approved.
- [ ] Gym access integration assessed, if required.
- [ ] Reconciliation tested.
- [ ] Dashboard and reports validated.
- [ ] Support and escalation owners assigned.
- [ ] Country-specific readiness approved.

## 16. Known gaps and future opportunities

The following ideas may improve the fitness solution but must not be represented as released FlexiBill capabilities without confirmation.

| Opportunity | Potential value | Internal status |
|---|---|---|
| Automated membership entitlement | Connect successful payment to gym access | Integration / validation required |
| Native pause and resume | Flexible membership lifecycle | Validate current capability |
| Automatic upgrade/downgrade proration | More flexible plan management | Validation required |
| Multi-product membership | Bundle gym, classes, and add-ons | Gap / strategic direction |
| Usage-based personal training billing | Bill by actual usage | Requires usage source and calculation validation |
| Automated recovery optimization | Improve collection recovery | Validate current capabilities |
| Member QR privileges | Identify members and provide merchant benefits | Strategic / integration concept |
| Cross-branch membership | Enable access across branches | Merchant system integration required |
| Cross-merchant bill hub | Pay bills across multiple merchants | Strategic concept, not generally available |

## 17. Success measurement

Establish a baseline before implementation and review performance after launch.

| Outcome | KPI |
|---|---|
| Acquisition improvement | Membership conversion rate |
| Registration improvement | Registration completion rate |
| Collection improvement | First-attempt success rate |
| Revenue recovery | Recovery rate and recovered value |
| Retention improvement | Renewal and churn rates |
| Operational efficiency | Manual follow-up volume and reconciliation effort |
| Customer experience | Billing Portal engagement and support contacts |

Avoid attributing all improvement to FlexiBill alone. Separate product impact from merchant pricing, campaign, customer mix, and payment-method changes.

## 18. Related playbooks

- [Collection Management](../10-product-configuration/01-collection-management.md)
- [Plan and Pricing Configuration](../10-product-configuration/02-plan-and-pricing-configuration.md)
- [Pricing Table](../10-product-configuration/03-pricing-table.md)
- [Member Center](../10-product-configuration/04-member-center.md)
- [Billing Portal](../10-product-configuration/05-billing-portal.md)
- [Account Billing](../10-product-configuration/06-account-billing.md)
- [Subscription Lifecycle](../10-product-configuration/07-subscription-lifecycle.md)
- [Payment Management](../10-product-configuration/08-payment-management.md)
- [Configuration Reference Matrix](../10-product-configuration/09-configuration-reference-matrix.md)

## 19. Governance

This is a reusable reference solution for fitness and gym membership merchants.

Before reusing it:
1. Validate current FlexiBill capabilities.
2. Confirm the merchant's commercial model.
3. Validate payment-method eligibility.
4. Confirm customer-facing interface availability.
5. Validate country-specific scope.
6. Record integration dependencies and product gaps.
7. Obtain merchant and internal sign-off.

**Owner:** FlexiBill Product  
**Use case ID:** MER-001  
**Review trigger:** Product release, payment-channel change, country expansion, or material merchant implementation finding.
