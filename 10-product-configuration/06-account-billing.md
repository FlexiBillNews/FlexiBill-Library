# Account Billing Playbook

**Phase:** 2 — Product Configuration  
**Product:** DOKU FlexiBill  
**Audience:** Product, Engineering, Implementation, Sales, Partnership, Operations  
**Markets:** Indonesia (ID) and Malaysia (MY)  
**Status:** Internal working guide — validate exact behavior against current product documentation and country configuration before merchant commitment.

---

## 1. Overview

Account Billing supports billing organized around a customer account and a defined billing calendar.

Instead of treating every customer subscription as an independent anniversary-based billing event, an account-oriented model can organize billing around a common billing date or cycle.

This model is relevant when a merchant needs to bill customers according to an operational schedule, such as:

- Monthly utility or service charges.
- School or education fees.
- Insurance or membership contributions.
- Corporate service accounts.
- Association or community dues.
- Recurring services with a common invoice date.

**Important distinction:** Account Billing should not automatically be treated as identical to conventional subscription recurring billing. Its precise cycle rules, invoice behavior, payment execution, and account relationships must be confirmed for the implementation.

## 2. Where Account Billing fits

A simplified conceptual flow:

`Merchant → Customer Account → Billing Calendar → Bill Generation → Payment Collection → Reconciliation`

| Component | Role |
|---|---|
| Merchant | Owns the commercial relationship and billing rules |
| Customer account | Groups the relevant customer or service relationship |
| Billing calendar | Defines the intended billing date or cycle |
| Bill generation | Produces the amount due for a billing period |
| Payment collection | Collects through the configured payment method |
| Reconciliation | Tracks the outcome against the bill and account |

The exact relationship between Account Billing, Collection, Plan, Member Center, and payment configuration should be validated against the deployed product setup.

## 3. Account Billing vs Subscription Billing

| Dimension | Account Billing | Subscription Billing |
|---|---|---|
| Organizing principle | Customer account and billing calendar | Subscription and its recurring terms |
| Billing date | May follow a common calendar date | May follow subscription cadence or configured billing anchor |
| Customer relationship | Account-oriented | Subscription-oriented |
| Typical use case | Customers billed on a common schedule | Customers subscribing to a recurring service |
| Amount | Depends on configured account billing rules | Depends on plan and subscription pricing |
| Key question | When and how is the account billed? | What subscription is being renewed, and when? |

This is a conceptual comparison, not a guarantee that every behavior is available in every FlexiBill configuration.

## 4. Merchant use cases

### 4.1 Education

A school bills families on the 5th of each month.

Potential requirements:
- A family or student account.
- A common monthly billing date.
- Tuition or service charges.
- Payment status visibility.
- Follow-up for unpaid bills.

Validate whether one account can represent multiple students and how charges are consolidated.

### 4.2 Insurance

An insurer or distribution partner bills policyholders according to a defined premium schedule.

Potential requirements:
- Policyholder or policy-level account mapping.
- Premium amount and due date.
- Auto-debit where supported.
- Failed collection monitoring.
- Renewal and lapse tracking.

Do not assume Account Billing automatically provides insurance policy administration, premium calculation, or lapse management.

### 4.3 Utilities and recurring services

A service provider bills customers on a standard monthly cycle.

Potential requirements:
- Customer account identification.
- Billing period and due date.
- Fixed or variable amount.
- Payment status.
- Reconciliation and exception handling.

Native metering and real-time usage aggregation should not be assumed. If consumption data is involved, confirm where the usage calculation takes place and how the final bill amount is supplied.

## 5. Merchant configuration workflow

Use this as an implementation checklist. Exact menu names, fields, and API behavior must be verified in the current environment.

### Step 1 — Define the account model

Document:
- Merchant identifier.
- Customer/account identifier.
- Account ownership.
- Relationship between account and individual customers.
- Whether one account can contain multiple services or members.
- Required account status.

### Step 2 — Define the billing calendar

Confirm:
- Billing frequency.
- Intended billing day.
- Billing period start and end.
- Due date.
- Timezone.
- Cut-off time.
- Weekend and public holiday treatment.
- Month-end behavior.

Do not assume a configured billing day automatically resolves invalid calendar dates such as the 29th, 30th, or 31st in shorter months.

### Step 3 — Define the amount calculation

Identify:
- Fixed amount or externally calculated amount.
- Variable charges.
- Discounts.
- Tax treatment.
- Adjustments.
- Outstanding balance treatment.
- Rounding rules.

If the merchant calculates charges externally, document the source system and the data transfer mechanism.

### Step 4 — Define bill generation

Confirm:
- What event triggers bill generation.
- Whether generation is scheduled or initiated through an integration.
- Whether a bill is created for every eligible account.
- How duplicate generation is prevented.
- How failed generation is detected.
- How corrections and cancellations are handled.

### Step 5 — Define payment collection

Confirm:
- Supported payment methods.
- Auto-debit eligibility.
- Customer authorization requirements.
- Payment attempt schedule.
- Retry rules.
- Failure notifications.
- Alternative payment options.

### Step 6 — Define reconciliation

Establish how the merchant can identify:
- Bills generated.
- Bills awaiting payment.
- Successful payments.
- Failed payments.
- Duplicate or unmatched transactions.
- Reversed or refunded transactions.
- Accounts requiring operational follow-up.

## 6. Merchant and customer journeys

### Merchant journey

1. Define customer account structure.
2. Configure or establish the billing calendar.
3. Supply or calculate the amount due.
4. Generate bills for the applicable cycle.
5. Initiate the configured payment collection.
6. Monitor successful and unsuccessful payments.
7. Reconcile payment outcomes.
8. Resolve exceptions before the next cycle.

### Customer journey

1. Customer is associated with a merchant account.
2. Customer receives billing information through the supported communication channel.
3. Customer reviews the amount and due date.
4. Customer pays through an available payment method or an authorized auto-debit arrangement.
5. Customer receives the supported payment confirmation.
6. Customer can check payment status through the available customer interface, if enabled.

The availability of a self-service portal, invoice history, payment-method management, and account-level views must be validated separately.

## 7. Account Billing and payment architecture

A conceptual integration model:

```text
Merchant System
      |
      | Account / Billing Data
      v
FlexiBill Account Billing
      |
      | Billing Cycle / Bill Generation
      v
Bill or Invoice
      |
      | Payment Instruction
      v
DOKU Payment Processing
      |
      | Payment Result
      v
FlexiBill Status / Reconciliation
      |
      v
Merchant System
```

This is a logical view. It does not prescribe a specific API, webhook, scheduler, or database implementation.

Before solution design, confirm:
- Which system owns the account record.
- Which system owns the billing calendar.
- Which system calculates the bill amount.
- Which system initiates bill generation.
- Which system initiates payment.
- How payment status is returned.
- How duplicate events and retries are handled.

## 8. Relationship with integration models

| Integration model | Consideration |
|---|---|
| DOKU-hosted Billing Automation | Confirm whether the required account billing workflow is supported natively |
| H2H API and Webhook | Confirm available APIs, event notifications, and merchant responsibilities |
| Hybrid | Define which billing and payment responsibilities remain with the merchant |
| Merchant Hosted Scheduler | Validate eligibility, country scope, and the exact documented operating model |

**Country restriction:** Merchant Hosted Scheduler has been documented for Indonesian Business Account. Do not assume Malaysia support without explicit confirmation.

## 9. Critical configuration and test scenarios

| Scenario | What to validate |
|---|---|
| Normal monthly cycle | Bill generated on the expected date |
| Month with 28 days | Billing-day behavior |
| Month with 29 days | Leap-year and non-leap-year behavior |
| Month with 30 days | Date adjustment behavior |
| Month with 31 days | Date adjustment behavior |
| Customer joins mid-cycle | First billing treatment |
| Amount changes | Effective date and adjustment |
| Customer becomes inactive | Billing eligibility |
| Payment fails | Retry, notification, and outstanding status |
| Multiple members per account | Account-to-customer mapping |
| Duplicate input | Idempotency and duplicate prevention |
| Timezone boundary | Correct billing date and time |
| Weekend or public holiday | Calendar handling |
| Payment reversal | Status and reconciliation treatment |

## 10. Common implementation risks

| Risk | Potential impact | Mitigation |
|---|---|---|
| Incorrect account mapping | Wrong customer billed | Validate unique account identifiers |
| Calendar assumptions | Unexpected billing dates | Test month-end and leap-year cases |
| Incorrect amount source | Overbilling or underbilling | Reconcile source amount against generated bill |
| Duplicate bill generation | Duplicate collection | Confirm idempotency controls |
| Unclear payment ownership | Missing or duplicated payment instruction | Document system responsibility |
| Unhandled failures
