# FlexiBill Technical Solution Patterns

**Document type:** Technical solution playbook  
**Audience:** Product, Engineering, Solution Architecture, Integration, Implementation, Partnership, Operations  
**Markets:** Indonesia (ID) and Malaysia (MY)  
**Status:** Internal reference — validate product and country capabilities before implementation

---

## 1. Purpose

This playbook provides reusable technical solution patterns for implementing FlexiBill across different merchant types and billing scenarios.

It translates business requirements into practical architecture decisions covering:

- System ownership and boundaries
- FlexiBill configuration and integration role
- Billing and payment flows
- Data exchange and event handling
- Failure recovery and reconciliation
- Testing and implementation dependencies
- Country-specific validation

These patterns are reference architectures, not a guarantee that every workflow is available as an out-of-the-box FlexiBill feature.

### Capability classification

| Label | Meaning |
|---|---|
| Available | Documented or established capability; confirm configuration and eligibility |
| Conditional | Depends on product setup, integration model, payment method, or merchant eligibility |
| Validation required | Must be checked with Product, Engineering, Operations, or country teams |
| Gap | Not established as a native capability |
| Future / Strategic | Proposed direction, not a current production commitment |

## 2. Architecture principles

### 2.1 Establish system ownership first

Every implementation must identify which system owns each business object.

A typical ownership model:

| Business object | Typical system owner |
|---|---|
| Merchant customer profile | Merchant CRM / core platform |
| Product or service entitlement | Merchant application |
| Contract or policy | Merchant core system |
| Subscription billing configuration | FlexiBill or merchant billing system, depending on model |
| Invoice / billing obligation | FlexiBill or merchant ERP, depending on model |
| Payment authorization | DOKU payment infrastructure and applicable payment partners |
| Payment result | DOKU payment infrastructure, communicated through supported response/event channels |
| Settlement | DOKU settlement and merchant finance processes |
| Accounting / revenue recognition | Merchant finance or ERP |

The ownership model must be agreed before designing API contracts or user journeys.

### 2.2 Separate billing from payment

A billing obligation and a payment transaction are different objects.

A customer may have an invoice even when payment has not been attempted. A payment may be pending even though the billing schedule has already run.

The solution must distinguish:

1. Customer and subscription identity
2. Billing obligation
3. Invoice or bill reference
4. Payment attempt
5. Payment result
6. Settlement and reconciliation

Do not treat a successful billing-generation event as proof of successful payment.

### 2.3 Keep business logic with the system that owns it

FlexiBill should orchestrate supported billing and collection workflows. It should not silently become the owner of a merchant's policy administration, student records, inventory, entitlement, accounting, or contract logic.

### 2.4 Design for asynchronous outcomes

Payment and integration outcomes may not be immediately final.

Implementations must support:

- Duplicate events
- Delayed responses
- Pending transactions
- Out-of-order notifications
- Inquiry before retry where transaction status is uncertain
- Reconciliation of unresolved records

### 2.5 Validate each market independently

Indonesia and Malaysia must have separate capability and operational sign-off.

Do not infer MY availability from ID documentation, or vice versa.

---

## 3. Integration model selection

Choose the integration model based on who should control billing schedules, business logic, and customer experience.

| Model | FlexiBill role | Merchant role | Best fit | Validation |
|---|---|---|---|---|
| DOKU-hosted Billing Automation | Hosts supported billing configuration and orchestration | Supplies customer, product, and billing information | Merchants seeking managed billing operations | Confirm supported configuration and payment methods |
| API / H2H | Provides supported billing and payment integration capabilities | Controls application and business workflow | SaaS, platforms, enterprise integrations | Confirm API scope, lifecycle support, and technical contract |
| Hybrid | Combines FlexiBill-managed capabilities with merchant-owned application logic | Owns selected customer experience and business decisions | Merchants needing faster implementation with custom workflows | Agree system ownership and avoid duplicate billing logic |
| Merchant Hosted Scheduler | Supports the documented merchant-hosted recurring billing pattern | Controls schedule execution and related orchestration | Merchants requiring scheduler control | Documented for Indonesian Business Account; MY applicability requires validation |

### Decision guide

Use DOKU-hosted Billing Automation when the merchant wants to configure and operate supported billing workflows through FlexiBill.

Use API / H2H when the merchant requires direct integration with its own application, backend, or customer journey.

Use Hybrid when the merchant wants FlexiBill to manage selected billing and payment capabilities while retaining business logic or customer experience in its own systems.

Use Merchant Hosted Scheduler only after confirming the applicable merchant eligibility, account setup, country availability, and technical documentation.

**Important:** Do not select a model solely because it is technically possible. Confirm the product capability, operational ownership, and support model.

---

## 4. Reference architecture

A reusable logical architecture is:

```text
                    MERCHANT EXPERIENCE
          Web / Mobile / Portal / CRM / Agent / App
                              |
                              v
                    MERCHANT APPLICATION
           Customer / Contract / Product / Entitlement
                              |
                              v
                  MERCHANT INTEGRATION LAYER
            API Adapter / Scheduler / Event Consumer
                              |
                              v
                    FLEXIBILL PLATFORM
          Member / Collection / Plan / Pricing / Billing
                  Invoice / Billing Orchestration
                              |
                              v
                    DOKU PAYMENT LAYER
           Payment Authorization / Collection / Inquiry
                              |
                              v
                  PAYMENT METHOD / PARTNER
                              |
                              v
                    PAYMENT OUTCOME
                              |
                 +------------+------------+
                 |                         |
                 v                         v
           WEBHOOK / EVENT             INQUIRY / STATUS
                 |                         |
                 +------------+------------+
                              |
                              v
                  MERCHANT RECONCILIATION
              Billing / Payment / Settlement / ERP
```

This is a logical reference architecture. Actual components, interfaces, deployment boundaries, and data contracts must follow the approved technical documentation.

### Architecture responsibilities

| Layer | Responsibility |
|---|---|
| Merchant experience | Customer registration, plan selection, billing visibility, service access |
| Merchant application | Customer, contract, product, entitlement, and business rules |
| Merchant integration | API adaptation, scheduling where applicable, event consumption, mapping |
| FlexiBill | Supported member, billing configuration, billing orchestration, and related workflows |
| DOKU payment layer | Payment processing and applicable authorization, collection, inquiry, and payment status |
| Payment partner | Bank, card, or other payment rail processing |
| Reconciliation | Matching billing, payment, settlement, and accounting records |

---

## 5. Solution pattern 01 — Insurance premium collection

### Context

An insurer or insurance distribution partner needs to collect recurring premiums from policyholders.

Examples:

- Monthly insurance premium
- Annual premium installment
- Bancassurance premium
- Policy renewal collection
- Failed premium recovery

### System ownership

| Domain | Owner |
|---|---|
| Policy number and policy status | Insurer policy administration system |
| Premium calculation | Insurer |
| Coverage and eligibility | Insurer |
| Policyholder identity | Insurer / authorized distribution partner |
| Billing schedule configuration | FlexiBill or insurer system, depending on integration model |
| Payment collection | DOKU / FlexiBill supported payment flow |
| Policy lapse and reinstatement | Insurer |

### Recommended pattern

```text
Policy Administration
        |
        | Policyholder + premium + due date
        v
Merchant Integration Layer
        |
        v
FlexiBill Billing Configuration
        |
        v
Billing Obligation / Invoice
        |
        v
Payment Collection
        |
        v
Payment Result
        |
        +----> Insurer policy system
        |
        +----> Reconciliation / finance
```

### Implementation steps

1. Map policyholder, policy, premium, and billing references.
2. Confirm who calculates the premium.
3. Define the billing schedule and payment authorization approach.
4. Configure the supported FlexiBill billing workflow.
5. Connect payment outcomes to the insurer's policy system.
6. Reconcile billing obligations against payment and settlement records.
7. Define how failed and overdue premiums are handled by the insurer.

### Critical controls

- Preserve policy number and premium period in the reference mapping.
- Do not assume FlexiBill determines coverage status.
- Do not assume every insurer uses a 90-day grace period.
- The insurer owns lapse, reinstatement, and coverage decisions.
- Do not automatically retry indefinitely.
- Confirm whether payment credentials or mandates can be reused under the insurer's approved consent model.

### KPIs

- Premium collection success rate
- First-attempt success rate
- Recovery rate
- Failed premium value
- Never-successful billing population
- Days from due date to successful payment
- Policy lapse attributable to payment failure, as defined by the insurer

---

## 6. Solution pattern 02 — Fitness and gym membership

### Context

A gym or fitness operator collects recurring membership fees and wants to connect payment status with membership operations.

Examples:

- Monthly membership
- Annual membership
- Class packages
- Membership renewal
- Promotional membership offers

### System ownership

| Domain | Owner |
|---|---|
| Member profile | Gym membership system |
| Membership agreement | Gym |
| Plan and price | Gym, configured in FlexiBill where supported |
| Billing schedule | FlexiBill or gym scheduler |
| Payment collection | FlexiBill / DOKU |
| Door access and attendance | Gym access-control system |
| Membership privileges | Gym membership system |

### Recommended pattern

```text
Gym CRM / Membership System
        |
        | Member + membership + price
        v
FlexiBill
        |
        v
Recurring Billing
        |
        v
Payment Collection
        |
        v
Payment Result / Event
        |
        v
Gym Membership System
        |
        +----> Update membership payment status
        |
        +----> Apply gym-defined access rules
```

### Implementation steps

1. Define membership products and pricing.
2. Map member ID to FlexiBill member and billing references.
3. Configure supported recurring billing.
4. Define payment authorization and collection.
5. Receive and process payment outcomes.
6. Update the gym's membership system.
7. Let the gym system determine whether access should be enabled, restricted, or restored.

### Critical controls

- Successful payment does not automatically grant physical access unless an access-control integration exists.
- FlexiBill should not be assumed to own attendance or class booking.
- Pause, freeze, cancellation, upgrade, downgrade, and proration require capability validation.
- Promotional benefits such as "pay 12 months, receive 1 month free" require explicit pricing and entitlement design.

### KPIs

- Active paying members
- Collection success rate
- Failed renewal rate
- Membership renewal rate
- Recovery rate
- Revenue per member
- Payment-related membership suspension

---

## 7. Solution pattern 03 — Education and school fees

### Context

Schools, universities, and education platforms collect recurring or periodic fees.

Examples:

- Monthly school fees
- Semester tuition
- Registration fees
- Course installments
- Extracurricular fees

### System ownership

| Domain | Owner |
|---|---|
| Student record | Student Information System (SIS) |
| Parent / guardian relationship | SIS / school |
| Tuition calculation | School / ERP |
| Academic period | SIS |
| Billing schedule | FlexiBill or school ERP, depending on model |
| Payment collection | FlexiBill / DOKU |
| Student enrollment and access | School SIS |

### Recommended pattern

```text
School SIS / ERP
        |
        | Student + payer + fee obligation
        v
Integration Layer
        |
        v
FlexiBill Billing
        |
        v
Invoice / Payment Request
        |
        v
Payment Collection
        |
        v
Payment Result
        |
        v
School ERP / SIS
        |
        +----> Update fee status
        |
        +----> Update finance records
```

### Implementation steps

1. Identify the student and the responsible payer.
2. Define fee types and academic periods.
3. Calculate tuition and adjustments in the school system unless explicitly designed otherwise.
4. Map fee obligation and payer references.
5. Generate the billing obligation through the agreed FlexiBill model.
6. Process payment results and reconcile them to the correct student and fee period.
7. Update the school's finance and student systems.

### Critical controls

- The payer may be different from the student.
- A family may have multiple students.
- Do not assume native family account hierarchy or consolidated invoicing.
- The SIS remains the authority for enrollment and academic status.
- Changes to tuition, scholarship, discount, or academic period must follow school policy.

### KPIs

- Fee collection rate
- Outstanding tuition value
- On-time payment rate
- Failed payment rate
- Collection recovery rate
- Outstanding balance by academic period

---

## 8. Solution pattern 04 — SaaS and digital subscriptions

### Context

A SaaS merchant charges customers for recurring access to software or digital services.

Examples:

- Monthly software subscription
- Annual subscription
- Tier-based pricing
- Fixed-price digital service
- Merchant-calculated usage charges

### System ownership

| Domain | Owner |
|---|---|
| User identity | Merchant application |
| Subscription entitlement | Merchant application |
| Product functionality | Merchant |
| Plan and billing configuration | FlexiBill or merchant application |
| Usage measurement | Merchant, unless a native meter is separately confirmed |
| Billing obligation | FlexiBill or merchant billing system |
| Payment collection | FlexiBill / DOKU |
| Access restriction | Merchant application |

### Recommended pattern

```text
SaaS Application
        |
        | Customer + subscription + plan
        v
FlexiBill Billing
        |
        v
Recurring Billing / Invoice
        |
        v
Payment Collection
        |
        v
Payment Result / Event
        |
        v
SaaS Entitlement Service
        |
        +----> Grant / continue access
        |
        +----> Apply merchant-defined restrictions
```

### Usage-based variation

```text
Merchant Usage System
        |
        | Usage calculation
        v
Merchant Billing Adapter
        |
        | Supported bill-generation process
        v
FlexiBill
        |
        v
Billing / Payment Collection
```

In this variation, the merchant calculates and validates usage before passing the bill amount through the supported integration.

### Critical controls

- Do not assume payment status automatically controls application entitlement.
- Do not assume native real-time metering or usage aggregation.
- Validate plan changes, proration, add-ons, and multi-product billing independently.
- The merchant must define how access behaves during pending, overdue, and failed payment states.
- Do not calculate usage twice in both merchant and FlexiBill systems.

### KPIs

- Monthly recurring revenue (MRR)
- Annual recurring revenue (ARR)
- Renewal success rate
- Churn rate
- Failed payment recovery
- Revenue leakage
- Average revenue per account

---

## 9. Solution pattern 05 — Travel and hospitality

### Context

Travel, hotel, and hospitality merchants collect deposits, installments, or recurring payments related to reservations and services.

Examples:

- Hotel deposits
- Tour installments
- Travel membership
- Recurring travel services
- Scheduled payment for a booking

### System ownership

| Domain | Owner |
|---|---|
| Reservation / booking | Booking engine |
| Room or seat inventory | PMS / CRS / airline or travel system |
| Travel dates | Booking system |
| Price and taxes | Merchant booking / pricing system |
| Billing obligation | FlexiBill or merchant system |
| Payment collection | FlexiBill / DOKU |
| Fulfillment | Travel / hospitality system |
| Cancellation and refund policy | Merchant |

### Recommended pattern

```text
Booking Engine / PMS / CRS
        |
        | Booking + payer + amount + due date
        v
Integration Layer
        |
        v
FlexiBill Billing
        |
        v
Payment Collection
        |
        v
Payment Result
        |
        v
Booking System
        |
        +----> Confirm / update payment status
        |
        +----> Continue booking workflow
```

### Implementation steps

1. Confirm the booking lifecycle and payment milestones.
2. Identify deposit, installment, and final-payment obligations.
3. Map booking ID, customer ID, amount, currency, and due date.
4. Generate the appropriate billing obligation.
5. Process payment and return the outcome to the booking system.
6. Reconcile payment against booking and settlement records.
7. Handle cancellations and refunds according to merchant policy and supported payment processes.

### Critical controls

- Do not assume FlexiBill owns reservation inventory.
- Do not assume payment success guarantees room, seat, or service availability.
- The booking engine owns cancellation, fulfillment, and reservation status.
- Refunds must follow merchant policy and the applicable payment method's capabilities.
- Confirm whether the original payment method supports the required refund flow.

### KPIs

- Deposit collection rate
- Installment success rate
- Booking payment completion
- Failed payment value
- Refund rate
- Outstanding booking balance

---

## 10. Solution pattern 06 — Corporate and B2B billing

### Context

An enterprise merchant collects recurring or periodic charges from business customers.

Examples:

- Monthly service fees
- Contracted service charges
- Corporate subscriptions
- Branch-level charges
- Usage-based enterprise billing

### System ownership

| Domain | Owner |
|---|---|
| Corporate customer hierarchy | Merchant CRM / ERP |
| Contract and commercial terms | Merchant contract system |
| Tax determination | Merchant tax / ERP process |
| Invoice consolidation | Merchant ERP unless separately supported |
| Billing schedule | FlexiBill or merchant system |
| Payment collection | FlexiBill / DOKU |
| Accounting | Merchant ERP |

### Recommended pattern

```text
Merchant CRM / Contract / ERP
        |
        | Customer + contract + billing obligation
        v
Integration Layer
        |
        v
FlexiBill
        |
        v
Billing / Payment Collection
        |
        v
Payment Result
        |
        v
Merchant ERP
        |
        +----> Accounts receivable
        |
        +----> Reconciliation and accounting
```

### Critical controls

- The merchant ERP remains the source of truth for legal entity and contract hierarchy.
- Do not assume native parent-child account hierarchy.
- Do not assume consolidated invoicing across multiple subscriptions.
- Confirm tax calculation, tax display, and tax reporting responsibilities.
- Map each invoice or billing obligation to the correct legal entity and contract.
- Define how partial payment and outstanding balances are handled.

### KPIs

- Days sales outstanding (DSO)
- Invoice collection rate
- Overdue receivables
- Collection recovery
- Payment allocation accuracy
- Reconciliation exception rate

---

## 11. Solution pattern 07 — Community and association membership

### Context

Associations, cooperatives, communities, and membership organizations collect recurring fees or contributions.

Examples:

- Monthly membership fees
- Annual membership
- Community contributions
- Cooperative member fees
- Agent or community-leader collections

### System ownership

| Domain | Owner |
|---|---|
| Member identity | Association / cooperative system |
| Membership status | Association / cooperative |
| Benefits and privileges | Organization |
| Fee rules | Organization |
| Billing configuration | FlexiBill or organization system |
| Payment collection | FlexiBill / DOKU |
| Member engagement | Organization |

### Recommended pattern

```text
Association / Cooperative System
        |
        | Member + membership + fee
        v
FlexiBill Member / Billing Configuration
        |
        v
Billing / Payment Collection
        |
        v
Payment Result
        |
        v
Organization Member System
        |
        +----> Update payment status
        |
        +----> Apply member-defined benefits
```

### Member Center consideration

Member Center-related APIs and the customer-facing registration experience must be treated as separate readiness items.

Before committing to a self-service registration journey, validate:

- API availability and scope
- Frontend availability
- Authentication and verification
- Customer data ownership
- Registration and consent flow
- Supported payment authorization journey

Do not describe an API as a complete customer-facing registration solution unless the frontend and end-to-end journey are confirmed.

### Critical controls

- Organization remains the authority for membership status.
- Benefits and privileges require integration with the organization's system.
- Do not assume a native community wallet or entitlement engine.
- Validate member identity deduplication and delegated collection workflows.

### KPIs

- Active members
- Membership renewal rate
- Fee collection rate
- Failed collection recovery
- Member registration conversion
- Payment-related inactive membership

---

## 12. Solution pattern 08 — Merchant migration to FlexiBill

### Context

An existing merchant migrates recurring billing or subscription operations from a legacy platform to FlexiBill.

### Ownership and responsibilities

| Area | Source system | Target / FlexiBill | Merchant responsibility |
|---|---|---|---|
| Customer records | Existing source | New member mapping where supported | Deduplicate and validate |
| Subscription records | Existing source | New configuration / subscription records | Reconcile lifecycle |
| Pricing | Existing source | Reconfigure supported pricing | Validate equivalence |
| Billing schedule | Existing source | Configure target schedule | Prevent overlap |
| Payment credentials | Existing source / partner | Target authorization capability | Confirm portability or reauthorization |
| Historical invoices | Existing source | Target history only if supported | Preserve archive |
| Payment history | Existing source | New payment records | Reconcile historical and new periods |

### Recommended migration sequence

```text
SOURCE SYSTEM
     |
     v
DATA INVENTORY
     |
     v
DATA MAPPING & CLEANUP
     |
     v
TARGET CONFIGURATION
     |
     v
CUSTOMER / SUBSCRIPTION VALIDATION
     |
     v
PAYMENT AUTHORIZATION CHECK
     |
     v
PILOT MIGRATION
     |
     v
RECONCILIATION
     |
     v
CONTROLLED CUTOVER
     |
     v
POST-MIGRATION MONITORING
```

### Migration controls

1. Establish a source-of-truth snapshot.
2. Identify active, overdue, suspended, and cancelled subscriptions.
3. Map source customer, subscription, billing, and payment references.
4. Validate plan, amount, interval, billing date, and lifecycle configuration.
5. Confirm whether payment tokens or mandates are portable.
6. If portability is not supported, design customer reauthorization.
7. Pilot with a controlled merchant population.
8. Reconcile source and target records before cutover.
9. Prevent the source and target systems from charging the same obligation.
10. Monitor the first billing cycles and maintain a rollback or exception process.

### Critical warning

**Token and mandate portability must never be assumed.**

A migration may require new customer consent or payment reauthorization. This must be confirmed with the relevant payment and compliance teams.

### Migration KPIs

- Customer migration completion
- Subscription mapping accuracy
- Payment authorization completion
- First-cycle collection success
- Duplicate billing incidents
- Migration-related payment failures
- Reconciliation exceptions

---

## 13. Solution pattern 09 — Merchant-calculated usage / Meter-Lite

### Context

A merchant charges customers based on measured usage but calculates the usage externally.

Examples:

- API calls
- Data consumption
- Number of transactions
- Units consumed
- Service utilization

### Recommended architecture

```text
Merchant Product / Usage System
        |
        v
Usage Aggregation & Validation
        |
        v
Merchant Pricing Calculation
        |
        v
Billing Integration Adapter
        |
        v
FlexiBill Supported Bill Generation
        |
        v
Invoice / Payment Collection
```

### Responsibility split

| Responsibility | Owner |
|---|---|
| Capture usage events | Merchant |
| Aggregate usage | Merchant |
| Validate usage records | Merchant |
| Apply usage pricing | Merchant |
| Produce final billing amount | Merchant |
| Generate bill through supported integration | FlexiBill / agreed integration |
| Collect payment | FlexiBill / DOKU |
| Usage dispute and adjustment | Merchant |

### Implementation controls

- Define usage period and cutoff time.
- Preserve source usage records.
- Validate calculation and rounding rules.
- Define how late-arriving usage is handled.
- Prevent duplicate bill generation.
- Maintain a link between the usage statement and the generated billing reference.
- Define adjustment and credit processes.

### Capability boundary

This pattern does not imply native real-time metering or usage aggregation in FlexiBill.

A merchant-calculated usage model is different from a native metering platform such as a dedicated usage-rating engine.

### KPIs

- Usage-to-bill accuracy
- Bill generation success
- Usage dispute rate
- Billing adjustment rate
- Collection success
- Revenue leakage from unbilled usage

---

## 14. Solution pattern 10 — Cross-merchant Bill Connector / one-VA hub

<badge>Future / Strategic concept — not a released FlexiBill capability</badge>

### 14.1 Concept

A cross-merchant Bill Connector would allow a customer to access bills from multiple participating merchants through a common payment experience.

The strategic inspiration is the JomPAY-style proposition of simplifying bill payment across participating billers and payment channels.

The concept should be evaluated separately from current FlexiBill subscription and billing capabilities.

### 14.2 Strategic customer proposition

A customer could:

- Discover bills from participating merchants.
- Select one bill to pay.
- Pay the oldest eligible bill.
- Pay multiple bills through a defined payment journey, if supported by the eventual design.
- Set up auto-debit for one or more eligible billing relationships, subject to consent and payment-rail rules.
- Access merchant-specific privileges through an agreed member identification mechanism.

### 14.3 Strategic merchant proposition

A participating merchant could:

- Register as a biller.
- Make eligible bills discoverable through the hub.
- Promote bill payment through the shared customer experience.
- Use payment-linked campaigns or privileges.
- Potentially support recurring collection through an approved authorization model.
- Access payment and billing reconciliation for its own obligations.

### 14.4 Logical architecture

```text
                  CUSTOMER CHANNEL
             App / Web / Member QR
                       |
                       v
                BILL CONNECTOR HUB
          Customer Identity / Bill Discovery
          Bill Selection / Payment Orchestration
                       |
             +---------+---------+
             |                   |
             v                   v
        MERCHANT A           MERCHANT B
        BILL SYSTEM          BILL SYSTEM
             |                   |
             +---------+---------+
                       |
                       v
              DOKU PAYMENT LAYER
                       |
                       v
             PARTICIPATING BANK RAILS
```

This diagram is conceptual. It does not represent an existing production integration or confirmed one-VA payment network.

### 14.5 Important distinction: one VA versus one payment experience

These are not automatically the same architecture.

**Single biller VA model:** A virtual account or payment reference identifies a biller or bill obligation under a particular payment arrangement.

**Cross-bank payment acceptance:** A payment reference may be payable through multiple participating bank rails, subject to network and partner agreements.

**Cross-merchant bill hub:** A customer-facing platform discovers and presents bills from multiple billers.

A single VA that works across multiple banks does not automatically provide cross-merchant bill discovery, and a cross-merchant hub does not automatically create one universal VA.

The product and partnership teams must define which of these propositions is intended.

### 14.6 Bill payment flows to evaluate

**Flow A — Pay one selected bill**

1. Customer opens the Bill Connector.
2. Customer is authenticated.
3. Hub retrieves eligible bills from participating merchants.
4. Customer selects one bill.
5. Hub creates or retrieves the payment instruction.
6. Customer pays through an approved DOKU payment route.
7. Payment outcome is returned to the hub and biller.
8. Biller updates the bill status.

**Flow B — Pay oldest eligible bill**

1. Hub retrieves eligible outstanding bills.
2. Billers provide due dates, balances, and payment eligibility.
3. Hub applies a transparent oldest-bill selection rule.
4. Customer reviews the selected bill.
5. Customer confirms payment.
6. Payment result is distributed to the relevant biller.

The hub must not silently decide which bill is paid. The selection rule and customer confirmation must be explicit.

**Flow C — Pay multiple bills**

1. Hub retrieves eligible bills.
2. Customer selects multiple bills.
3. Hub calculates the total and displays the bill-level breakdown.
4. Payment orchestration determines whether one payment can settle all selected bills.
5. Each biller receives its own allocation and payment result.
6. Partial success, partial failure, refund, and allocation exceptions are handled explicitly.

A multi-bill checkout requires payment allocation, settlement, reconciliation, and failure-handling design. It must not be assumed to be supported by a single ordinary payment transaction.

**Flow D — Auto-debit for one or multiple billers**

1. Customer selects a biller or billers.
2. Customer reviews the authorization scope and terms.
3. Customer completes the required payment authorization.
4. Hub stores or references the approved authorization according to the agreed security model.
5. Each eligible billing obligation is submitted under the applicable authorization.
6. Payment outcomes are reported to the relevant billers.
7. Customer can view and manage authorization status through the agreed experience.

Authorization for one merchant must not be assumed to authorize deductions for another merchant.

### 14.7 Member QR and merchant privileges

A potential member QR could identify a customer or membership relationship and enable a merchant-specific journey.

Example:

- A fitness merchant configures a membership offer.
- Customer presents an approved Bill Connector member QR.
- Merchant resolves the member identity through an agreed integration.
- Merchant checks eligibility in its own membership system.
- Payment is completed through the approved payment flow.
- Merchant applies its own benefit rule, such as a promotional free month.

The QR is an identification or journey-enablement mechanism; it is not itself proof of payment or entitlement.

### 14.8 Dependencies and partnership requirements

This concept requires further discovery across:

- Participating biller onboarding and agreements
- Bank and payment network participation
- VA issuing and acceptance rules
- Customer identity and consent
- Payment authorization and mandate model
- Bill inquiry and bill status interfaces
- Multi-bill allocation and settlement
- Refund and dispute handling
- Data sharing and privacy
- Customer support and dispute ownership
- Regulatory and compliance review
- Merchant privileges and campaign governance

### 14.9 Strategic KPIs

- Participating billers
- Active customers
- Bills discovered
- Bill payment conversion
- Successful payment value
- Repeat bill payment frequency
- Auto-debit adoption
- Cross-merchant engagement
- Payment success rate
- Bill status synchronization accuracy
- Reconciliation exception rate

### 14.10 Product status

The Bill Connector is a strategic concept requiring product discovery, architecture validation, partnership feasibility, regulatory assessment, and commercial approval.

Do not include it in a current FlexiBill feature list or merchant implementation commitment until formally approved and released.

---

## 15. Cross-cutting technical patterns

These controls apply to all solution patterns.

### 15.1 Identity and reference mapping

Maintain a clear mapping between:

- Merchant customer ID
- FlexiBill member reference
- Subscription or contract reference
- Billing obligation / invoice reference
- Payment transaction reference
- Settlement reference
- External ERP or core-system reference

Do not use one identifier as a substitute for every business object.

### 15.2 Idempotency and duplicate protection

Every integration must define:

- Which operations can be repeated safely
- How duplicate requests are detected
- How duplicate webhook events are handled
- Which reference is used to identify the original operation
- How uncertain outcomes are resolved

For uncertain payment outcomes, perform the appropriate inquiry or status resolution before initiating another collection attempt.

### 15.3 Event-driven processing

Where supported, process payment and billing events asynchronously.

A robust event consumer should:

1. Receive the event.
2. Validate its authenticity.
3. Store the event or processing reference.
4. Detect duplicates.
5. Resolve the relevant billing and payment records.
6. Apply the permitted state transition.
7. Record processing outcome.
8. Retry safely or route exceptions for investigation.

### 15.4 State separation

Maintain separate state models for:

- Customer/member
- Subscription or contract
- Billing obligation
- Invoice
- Payment attempt
- Payment transaction
- Settlement
- Merchant entitlement

For example, a subscription can remain active while one invoice is overdue, depending on merchant policy. A payment can be pending while a billing obligation remains open.

### 15.5 Reconciliation

Reconcile at multiple levels:

| Reconciliation layer | Key question |
|---|---|
| Billing | Was every expected obligation generated correctly? |
| Payment | Was each collection attempt resolved correctly? |
| Settlement | Does the settled amount match payment records after applicable fees and adjustments? |
| Merchant finance | Was the payment allocated to the correct customer, invoice, contract, and accounting period? |

### 15.6 Security

- Apply least-privilege access.
- Protect API credentials and signing secrets.
- Avoid storing raw payment credentials.
- Use approved token and authorization handling.
- Protect webhook endpoints.
- Minimize sensitive data in logs.
- Define retention and deletion requirements.
- Review market-specific compliance obligations.

### 15.7 Failure handling

Every implementation should distinguish:

- Validation error
- Configuration error
- Integration error
- Payment decline
- Pending or unknown payment outcome
- Timeout
- Duplicate request
- Webhook delivery failure
- Reconciliation mismatch

A timeout is not proof of payment failure. Follow the approved inquiry and recovery process.

---

## 16. Pattern comparison matrix

| Pattern | Primary merchant system | FlexiBill role | Key external dependency |
|---|---|---|---|
| Insurance | Policy administration | Premium billing and collection | Policy status and lapse rules |
| Fitness | Membership system | Membership billing and collection | Access and entitlement |
| Education | SIS / ERP | Fee billing and collection | Student, payer, academic records |
| SaaS | SaaS application | Subscription billing and collection | Entitlement and usage |
| Travel | Booking / PMS / CRS | Deposit and installment collection | Inventory and reservation |
| B2B | CRM / ERP | Contract-related billing and collection | Hierarchy, tax, accounting |
| Community | Member system | Membership fee billing and collection | Membership benefits |
| Migration | Source and target platforms | Target billing and collection | Data and authorization migration |
| Meter-Lite | Merchant usage system | Bill generation and collection | Usage calculation |
| Bill Connector | Proposed hub and biller systems | Potential shared billing/payment orchestration | Banks, billers, network, regulation |

---

## 17. Solution design checklist

Before approving an implementation, confirm the following.

### Business design

- [ ] Merchant use case and billing model are defined.
- [ ] Customer and payer roles are identified.
- [ ] Billing frequency and due-date rules are documented.
- [ ] Pricing and amount calculation ownership is explicit.
- [ ] Cancellation, refund, overdue, and recovery policies are defined.
- [ ] Customer communication responsibilities are assigned.

### Product capability

- [ ] Required FlexiBill capabilities are documented.
- [ ] Each capability is classified as Available, Conditional, Validation required, Gap, or Future.
- [ ] Country availability is confirmed.
- [ ] Member Center and customer-facing frontend readiness are assessed separately.
- [ ] Required plan changes and payment-management journeys are
