# Vertical Strategy and Industry Proposition

**Playbook:** Commercial Strategy & Sales Enablement  
**Document:** 02 — Vertical Strategy and Industry Proposition  
**Audience:** DOKU Sales, Product, Presales, Partnership, Merchant Success, and Country Teams  
**Status:** Internal working playbook — country and capability validation required

---

## 1. Purpose

This playbook translates FlexiBill's billing and payment orchestration capabilities into industry-specific merchant propositions.

The objective is to help DOKU teams answer five questions:

1. Which industries have meaningful recurring or scheduled billing needs?
2. What billing and collection problems exist in each industry?
3. Which FlexiBill solution pattern may address those problems?
4. What customer and merchant experience should be designed?
5. What capabilities, integrations, partnerships, or approvals must be validated?

The guiding principle:

> Do not sell the same feature list to every industry. Sell the business outcome that matters to each merchant.

---

## 2. Vertical prioritization framework

Prioritize opportunities using a combination of commercial potential, product fit, and implementation feasibility.

| Dimension | Assessment question |
|---|---|
| Billing frequency | Does the merchant bill customers repeatedly or on a predictable schedule? |
| Payment dependency | Does timely payment materially affect service delivery or revenue? |
| Collection complexity | Are there failed payments, manual follow-ups, multiple billing cycles, or fragmented collection channels? |
| Customer scale | Is the merchant managing a meaningful number of customers, members, or accounts? |
| Payment opportunity | Can DOKU-supported payment methods improve the collection experience? |
| Integration readiness | Can the merchant support the required hosted, API, batch, or hybrid workflow? |
| Revenue potential | Is there meaningful recurring payment volume or a broader payment opportunity? |
| Strategic value | Can the opportunity create a repeatable proposition or distribution partnership? |

### Suggested qualification score

Score each dimension from 1 to 5.

| Score | Interpretation |
|---:|---|
| 1 | Very limited opportunity |
| 2 | Low opportunity |
| 3 | Moderate opportunity |
| 4 | Strong opportunity |
| 5 | Very strong opportunity |

Suggested internal prioritization:
- **High priority:** 32–40
- **Medium priority:** 23–31
- **Exploratory:** 8–22

These thresholds are a proposed commercial screening tool, not an approved DOKU scoring policy. Apply judgment and document the assumptions.

---

## 3. Industry proposition overview

| Vertical | Primary billing model | Main merchant problem | FlexiBill opportunity |
|---|---|---|---|
| Insurance | Monthly, quarterly, annual premiums | Failed premium collection and persistency | Recurring premium collection and recovery visibility |
| Fitness and wellness | Membership and packages | Manual renewals and membership administration | Membership-linked recurring billing |
| Education | Tuition and periodic fees | Fragmented fee collection and follow-up | Structured scheduled billing |
| SaaS and technology | Monthly or annual subscription | Subscription administration and payment continuity | API-connected subscription billing |
| Travel and hospitality | Deposits, installments, and scheduled payments | Complex payment schedules | Structured billing and payment collection |
| Retail and digital commerce | Membership, repeat services, and campaigns | Fragmented customer payment journeys | Billing and payment entry points for repeat services |
| Corporate and B2B | Contractual invoices and retainers | Manual invoicing and reconciliation | Scheduled business billing |
| Lending and embedded finance | Scheduled repayment obligations | Collection operations and payment visibility | Billing-linked payment collection, subject to regulatory and product validation |
| Associations and communities | Member dues and periodic contributions | Member administration and dues collection | Membership and recurring billing |
| Agents and microfinance networks | Distributed collections | Collection visibility and operational coordination | Structured billing workflows, subject to partner and operating-model validation |

A vertical can contain multiple business models. Confirm the merchant's actual workflow rather than assuming every business in the industry has the same requirements.

---

## 4. Vertical 1 — Insurance

<badge label="High-priority opportunity hypothesis" color="success" />

### Business context

Insurance providers and distribution partners collect premiums according to policy schedules. A failed collection can create additional follow-up work and may affect policy continuity or persistency.

### Typical billing model
- Monthly premiums.
- Quarterly premiums.
- Semi-annual premiums.
- Annual premiums.
- Policy renewal collections.
- Bancassurance-related premium collections.

### Merchant pain points
- Failed auto-debit transactions.
- Limited visibility into repeated collection failures.
- Manual customer follow-up.
- Payment-method performance differences.
- Difficulty identifying customers who never successfully pay.
- Lapsed policy monitoring and recovery.

### FlexiBill proposition

> Improve the structure and visibility of premium billing and payment collection, helping insurance teams monitor collection outcomes and identify recovery opportunities.

### Relevant solution areas
- Customer and membership-related records.
- Scheduled billing.
- Supported recurring payment and auto-debit workflows.
- Billing and payment status monitoring.
- Failed collection analysis.
- Recovery and dunning processes where supported.
- API or batch integration where validated.

### Example commercial metrics
- Premium billing value.
- Collection success rate.
- Failed premium value.
- Unique policies with failed collection.
- Recovery rate.
- Days to recovery.
- Never-successful billing population.
- Renewal and persistency rate.

### Discovery questions
1. How many active policies are billed each month?
2. What are the premium frequencies and average amounts?
3. Which payment methods are currently supported?
4. What percentage of premiums fail on the initial collection?
5. What happens after the first failed collection?
6. How does the insurer define overdue, grace period, and lapse?
7. Can the insurer identify unique policies across billing cycles?

### Important validation

Insurance grace periods and lapse definitions vary by product, insurer, policy, and country. A 90-day period may be relevant to a specific bancassurance operating model but must not be treated as a universal insurance rule.

---

## 5. Vertical 2 — Fitness and wellness

### Business context

Gyms, fitness studios, wellness providers, and sports clubs often operate membership-based business models.

### Typical billing model
- Monthly membership.
- Quarterly or annual membership.
- Class packages.
- Personal training packages.
- Family or corporate memberships.
- Introductory trials followed by paid plans.

### Merchant pain points
- Manual renewal administration.
- Missed membership payments.
- Inconsistent member records.
- Difficulty tracking payment status.
- Manual plan changes and cancellations.
- Limited visibility into inactive or overdue members.

### FlexiBill proposition

> Make membership billing more structured and connect recurring collection with a better-managed member payment journey.

### Relevant solution areas
- Member Center.
- Collection and plan configuration.
- Pricing Table, where suitable.
- Recurring billing and supported auto-debit.
- Billing Portal, where the required customer workflows are available.
- Payment status visibility.
- Billing reminders and recovery processes where supported.

### Illustrative customer journey

1. Customer selects a membership plan.
2. Customer completes the supported registration and payment flow.
3. Membership and billing records are established.
4. Billing is initiated according to the configured schedule.
5. Payment outcome is recorded.
6. Failed collection enters the applicable recovery process.
7. Renewal, cancellation, or other lifecycle actions follow the supported workflow.

### Example commercial metrics
- Active paying members.
- Monthly recurring billing value.
- First-attempt collection success.
- Failed membership value.
- Recovery rate.
- Membership renewal rate.
- Average revenue per member.
- Overdue member count.

### Discovery questions
- How many active members are billed each month?
- Are memberships fixed-term or open-ended?
- Can members change plans or pause membership?
- How are failed payments handled?
- Does the gym have its own member-management system?
- Does it need a customer-facing portal?

### Important validation

Do not promise automated plan changes, proration, pause/resume, entitlement control, or gym access integration without confirming the exact available capability and implementation.

---

## 6. Vertical 3 — Education and schools

### Business context

Schools, universities, tutoring providers, training institutions, and education platforms collect tuition and other fees on recurring or scheduled cycles.

### Typical billing model
- Monthly tuition.
- Semester fees.
- Annual fees.
- Installment-based enrollment fees.
- Extracurricular and activity fees.
- Course or learning subscriptions.

### Merchant pain points
- Manual fee issuance.
- Multiple payment deadlines.
- Parent or student payment follow-up.
- Difficulty reconciling payments by student or invoice.
- Different billing schedules and fee structures.
- Inconsistent payment status visibility.

### FlexiBill proposition

> Organize scheduled education billing and connect student fee obligations with convenient payment collection workflows.

### Relevant solution areas
- Collection and plan configuration.
- Scheduled billing.
- Pricing Table or customer payment entry points.
- API and batch integration where supported.
- Payment status monitoring.
- Reconciliation and reporting.

### Example customer journey

1. School or institution creates a fee obligation.
2. Student or parent receives the relevant payment information.
3. Customer completes payment through a supported channel.
4. Payment status is reflected in the billing workflow.
5. Finance reconciles collections against student or invoice references.
6. Outstanding obligations are followed up.

### Example commercial metrics
- Students billed.
- Monthly or semester billing value.
- Collection success rate.
- Outstanding tuition value.
- Average days to payment.
- Reconciliation exception rate.
- Collection performance by campus or program.

### Discovery questions
- Is billing monthly, semester-based, or annual?
- Are fees the same for every student?
- Are there multiple campuses or education programs?
- Does the institution use a student information system?
- How are student and parent records linked?
- Does the institution need partial or installment payments?

### Important validation

Do not assume native student-account hierarchy, consolidated family invoicing, installment-plan management, or student-system integration. These may require merchant-side logic or additional integration.

---

## 7. Vertical 4 — SaaS and technology

### Business context

Software companies and digital platforms charge customers for access to software, services, or digital features.

### Typical billing model
- Monthly subscription.
- Annual subscription.
- Fixed recurring fee.
- Per-seat or per-unit billing.
- Usage-based billing.
- Tiered subscription plans.
- Enterprise contracts.

### Merchant pain points
- Subscription billing complexity.
- Payment failures and involuntary churn.
- Customer plan administration.
- Billing integration with the SaaS platform.
- Need for predictable recurring revenue.
- Customer payment-method management.

### FlexiBill proposition

> Connect subscription billing and payment collection with the merchant's own digital platform, using a solution pattern that fits its technical architecture.

### Relevant solution areas
- API / Host-to-Host integration.
- Collection and plan configuration.
- Pricing models supported by the product.
- Member Center and customer records.
- Recurring payment and supported auto-debit.
- Billing and payment status events.
- Reporting and recovery processes.

### Example commercial metrics
- Monthly recurring billing value.
- Active paying subscribers.
- First-attempt collection success.
- Failed recurring billing value.
- Recovered value.
- Payment-related churn.
- Average revenue per account.

### Discovery questions
- Is the product subscription-based or usage-based?
- Is billing fixed, per-seat, tiered, or metered?
- Does the merchant own its subscription database?
- Does it require API-driven billing?
- How are plan changes handled?
- Does the merchant calculate usage internally?
- What happens when a payment fails?

### Important validation

Do not position FlexiBill as a complete native real-time metering, entitlement, or subscription revenue management platform. Usage calculation may require merchant-side processing. Validate plan-change, add-on, proration, and lifecycle APIs individually.

---

## 8. Vertical 5 — Travel and hospitality

### Business context

Travel agencies, airlines, hotels, accommodation providers, and online travel platforms may collect payments at different stages of a booking.

### Typical billing model
- Booking deposits.
- Installments.
- Balance-due payments.
- Scheduled travel payments.
- Membership or loyalty subscriptions.
- Corporate travel billing.

### Merchant pain points
- Multiple payment milestones.
- Missed balance-due payments.
- Manual customer reminders.
- Booking and payment status fragmentation.
- Different payment schedules by product or booking type.

### FlexiBill proposition

> Structure scheduled payment obligations and connect them with payment collection workflows throughout the booking journey.

### Relevant solution areas
- Billing schedules.
- Customer billing records.
- Payment links or customer payment entry points.
- API integration with booking platforms.
- Payment status monitoring.
- Recovery workflows where supported.

### Example customer journey

1. Customer makes a booking.
2. Merchant establishes a deposit or initial payment obligation.
3. Merchant schedules subsequent payment obligations.
4. Customer receives payment information.
5. Payments are collected through supported methods.
6. Merchant monitors outstanding amounts and payment completion.

### Example commercial metrics
- Bookings with scheduled payments.
- Deposit collection rate.
- Balance-due collection rate.
- Outstanding booking value.
- Days between invoice and payment.
- Payment completion before service date.

### Discovery questions
- Are customers charged upfront or in installments?
- How many payment milestones exist?
- Are payment schedules linked to booking dates?
- Can customers change or cancel bookings?
- What happens when a payment is late?
- Does the booking system need real-time payment status?

### Important validation

Do not assume native booking inventory, reservation management, cancellation-fee calculation, dynamic FX, or automated refund orchestration. These typically require additional merchant systems and solution design.

---

## 9. Vertical 6 — Retail and digital commerce

### Business context

Retailers and digital platforms may offer memberships, repeat services, recurring deliveries, subscriptions, or campaign-based payment programs.

### Potential billing model
- Paid membership.
- Recurring service plans.
- Scheduled delivery payments.
- Digital service subscriptions.
- Repeat purchase programs.
- Campaign or package payments.

### Merchant pain points
- Fragmented customer payment journeys.
- Difficulty managing repeat billing.
- Manual membership administration.
- Limited visibility into recurring customer value.
- Disconnected campaign and payment workflows.

### FlexiBill proposition

> Create more structured payment journeys for repeat services, memberships, and scheduled customer billing.

### Relevant solution areas
- Pricing Table and supported customer payment flows.
- Member Center.
- Collection and plan configuration.
- Recurring payment where supported.
- API integration with merchant commerce systems.
- Billing and payment reporting.

### Discovery questions
- Is the merchant selling a product, service, membership, or subscription?
- Is payment repeated automatically or initiated by the customer?
- Is the customer required to register as a member?
- Is the payment tied to a campaign or benefit?
- Does the merchant need integration with its commerce platform?

### Important validation

A recurring billing solution is not automatically an e-commerce order management, inventory, loyalty, or campaign engine. Digital Catalog and Pricing Table integration must be confirmed before proposing a connected experience.

---

## 10. Vertical 7 — Corporate and B2B billing

### Business context

Corporate service providers, distributors, facility operators, and B2B vendors often bill clients under contractual arrangements.

### Typical billing model
- Monthly retainers.
- Contractual recurring invoices.
- Service subscriptions.
- Periodic maintenance fees.
- Fixed or variable service charges.
- Project milestone payments.

### Merchant pain points
- Manual invoice generation.
- Different billing dates by customer.
- Complex contract references.
- Payment follow-up.
- Reconciliation across multiple corporate accounts.

### FlexiBill proposition

> Bring structure to recurring and scheduled B2B billing while connecting payment collection and reporting processes.

### Relevant solution areas
- Billing schedules.
- Plan and pricing configuration.
- Batch or API integration where supported.
- Payment status tracking.
- Finance reconciliation workflows.

### Discovery questions
- How many corporate accounts are billed?
- Are invoices fixed or variable?
- Are billing dates contract-specific?
- Does the merchant require purchase order references?
- Are partial payments or multiple funding sources required?
- How is reconciliation performed today?

### Important validation

Do not assume native enterprise account hierarchy, purchase-order matching, consolidated invoicing, or complex accounts-receivable automation. Map these requirements explicitly.

---

## 11. Vertical 8 — Lending and embedded finance

### Business context

Lenders and embedded-finance providers collect scheduled repayment obligations from borrowers or platform users.

### Typical billing model
- Monthly installments.
- Fixed repayment schedules.
- Service fees.
- Membership or platform fees.
- Other contractual payment obligations.

### Merchant pain points
- Repayment collection failures.
- Large-scale payment follow-up.
- Payment status fragmentation.
- Reconciliation across loan accounts.
- Need for controlled retry and recovery processes.

### FlexiBill proposition

> Connect scheduled payment obligations with supported payment collection workflows and improve visibility into collection outcomes.

### Relevant solution areas
- Scheduled billing.
- API integration.
- Batch billing where supported.
- Payment status monitoring.
- Recovery analysis.
- Reconciliation support.

### Discovery questions
- What is the repayment schedule?
- Does the merchant own the loan ledger?
- How are partial and early repayments treated?
- How are overdue and delinquent accounts classified?
- What payment methods are permitted?
- Which regulatory and data-handling requirements apply?

### Important validation

Lending is a regulated and risk-sensitive use case. Validate regulatory requirements, licensing, payment authorization, data handling, customer consent, collections practices, and the lender's system of record. FlexiBill should not be represented as a loan origination, credit decisioning, or loan servicing platform unless separately validated.

---

## 12. Vertical 9 — Associations and communities

### Business context

Professional associations, clubs, cooperatives, membership organizations, and community groups collect recurring dues or contributions.

### Typical billing model
- Monthly membership dues.
- Annual membership fees.
- Community contributions.
- Training or event fees.
- Paid membership tiers.

### Merchant pain points
- Manual member registration.
- Inconsistent dues collection.
- Limited visibility into unpaid members.
- Fragmented communication.
- Difficulty administering large member populations.

### FlexiBill proposition

> Make membership-related billing more organized and connect member payment obligations with supported collection workflows.

### Relevant solution areas
- Member Center.
- Collection and plan configuration.
- Pricing Table.
- Billing and payment status visibility.
- Batch or API workflows where supported.

### Discovery questions
- How many members are managed?
- Are dues fixed or variable?
- How are new members registered?
- Can members have different fee categories?
- How are unpaid members followed up?
- Does the organization have branches or local administrators?

### Important validation

Do not assume cooperative ledger, member wallet, fund distribution, benefit entitlement, or multi-level organization management capabilities.

---

## 13. Vertical 10 — Agents and microfinance networks

### Business context

Some businesses collect payments through agents, field representatives, community leaders, or distributed networks.

### Potential billing model
- Periodic contributions.
- Scheduled member payments.
- Service fees.
- Group-based collections.
- Contractual recurring obligations.

### Merchant pain points
- Distributed collection operations.
- Inconsistent reporting across agents.
- Manual payment confirmation.
- Limited central visibility.
- Complex customer and agent attribution.

### FlexiBill proposition

> Structure billing obligations and connect payment collection with a more visible operating process across the merchant's distribution network.

### Potential solution components
- Central billing configuration.
- Customer and member records.
- Supported payment entry points.
- API or batch integration.
- Payment reporting.
- Agent-system integration, where available.

### Discovery questions
- Who is the legal biller and payment beneficiary?
- Who creates the billing obligation?
- How are agents identified?
- Does the agent collect funds or only facilitate payment?
- How is customer attribution recorded?
- What settlement and reconciliation model applies?

### Important validation

Agent attribution, commission calculation, fund distribution, agent wallets, and field-agent applications must not be assumed to be native FlexiBill capabilities.

---

## 14. Cross-vertical solution design

Some merchants operate across multiple industries or business lines. Use the following sequence to determine whether one solution design can support them.

1. Identify the legal merchant and biller.
2. Identify the customer or member.
3. Define the billing obligation.
4. Identify the applicable collection, plan, and pricing model.
5. Define the billing schedule.
6. Map supported payment methods.
7. Define the customer payment experience.
8. Define failure and recovery handling.
9. Map payment status and reconciliation.
10. Validate country, integration, and operational requirements.

Do not assume that a shared customer database or consolidated billing experience exists across separate merchants.

---

## 15. Indonesia and Malaysia market considerations

| Assessment | Indonesia | Malaysia |
|---|---|---|
| Merchant billing model | Validate by vertical and merchant | Validate independently |
| Payment method coverage | Confirm supported methods and recurring eligibility | Confirm supported methods and recurring eligibility |
| Auto-debit | Validate payment method, consent, and setup | Validate payment method, consent, and setup |
| Integration | Confirm API, batch, and hosted-flow scope | Confirm API, batch, and hosted-flow scope |
| Merchant Hosted Scheduler | Documented for Indonesian Business Account | Availability requires validation |
| Customer experience | Confirm actual interface and flow | Confirm actual interface and flow |
| Regulatory and operational requirements | Country-specific review | Country-specific review |

The table is a validation checklist, not a statement of feature parity.

---

## 16. Vertical prioritization scorecard template

Use this table during pipeline reviews.

| Merchant / Prospect | Vertical | Billing frequency | Monthly billing value | Payment failure problem | Integration readiness | Strategic fit | Priority |
|---|---|---|---:|---|---|---|---|
| Prospect A | Insurance | Monthly | To validate | To validate | To validate | To validate | Pending |
| Prospect B | Fitness | Monthly | To validate | To validate | To validate | To validate | Pending |
| Prospect C | Education | Monthly / semester | To validate | To validate | To validate | To validate | Pending |

Do not populate estimated values as actual merchant data. Mark missing inputs as pending validation.

---

## 17. Recommended go-to-market sequence

### Wave 1 — Repeatable billing use cases
Prioritize merchants with clear recurring billing needs, measurable collection problems, and relatively straightforward implementation paths.

Potential focus:
- Fitness and wellness.
- Associations and memberships.
- Selected education providers.
- Insurance collection opportunities.

### Wave 2 — Platform-integrated subscriptions
Develop propositions requiring stronger API and platform integration.

Potential focus:
- SaaS and technology.
- Digital platforms.
- Selected corporate and B2B billing.

### Wave 3 — Ecosystem and complex collection models
Develop opportunities requiring broader partnership, operating-model, or regulatory alignment.

Potential focus:
- Lending and embedded finance.
- Agent and community networks.
- Complex travel and hospitality.
- Cross-merchant billing concepts.

These waves are strategic recommendations, not approved launch commitments. Validate market demand, product readiness, commercial capacity, and delivery dependencies.

---

## 18. Final vertical proposition checklist

Before presenting an industry proposition:

- [ ] Industry-specific billing model is documented.
- [ ] Merchant pain points are supported by discovery.
- [ ] Commercial opportunity is quantified or clearly marked as an assumption.
- [ ] Proposed FlexiBill capabilities are validated.
- [ ] Payment methods and recurring eligibility are confirmed.
- [ ] Country-specific availability is confirmed.
- [ ] Customer experience is mapped.
- [ ] Integration and system ownership are documented.
- [ ] Product gaps and dependencies are disclosed.
- [ ] Regulatory and operational requirements are assessed.
- [ ] The proposition has a measurable success definition.

---

## 19. Final principle

The strongest FlexiBill vertical proposition is not the one with the most features.

It is the one that connects:

**A real industry billing problem → a feasible FlexiBill solution → a measurable merchant outcome → a repeatable commercial opportunity.**

---

**End of Playbook 02**
