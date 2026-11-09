# FlexiBill Dunning & Recovery Operations

**Document type:** Billing Collection, Dunning & Recovery Playbook  
**Audience:** Product, Operations, Engineering, Merchant Success, Finance, Customer Support  
**Markets:** Indonesia (ID) and Malaysia (MY)  
**Status:** Operational framework — retry permissions, payment capabilities, customer communication, and merchant policies require validation

---

## 1. Purpose

This playbook defines how FlexiBill merchants and DOKU teams should manage unsuccessful recurring billing and payment collection.

Dunning is the structured process of following up on an unsuccessful or overdue billing obligation to support successful collection, customer action, or an appropriate final business decision.

It connects:

1. Billing status.
2. Payment attempt outcome.
3. Failure classification.
4. Retry eligibility.
5. Customer communication.
6. Payment credential update, where supported.
7. Recovery monitoring.
8. Grace-period and subscription-state management.
9. Final resolution and reporting.

**Core principle:** Recovery must be controlled, status-aware, merchant-authorized, and customer-safe. More retries do not automatically mean more successful collections.

## 2. Dunning operating model

A typical recovery lifecycle is:

1. Billing becomes due.
2. Initial payment attempt is initiated.
3. Payment outcome is received or queried.
4. Successful payment closes the collection obligation.
5. Definitive failure enters recovery assessment.
6. Retry eligibility is evaluated.
7. Customer or merchant action is triggered where appropriate.
8. Eligible recovery attempts are executed.
9. Billing is monitored until successful collection or final resolution.
10. Subscription or account status is updated according to merchant rules.

A pending or unknown payment status must be resolved before treating the transaction as failed and initiating another charge.

## 3. Roles and responsibilities

| Role | Responsibility |
|---|---|
| Merchant | Owns billing obligation, customer relationship, retry policy, and subscription rules |
| DOKU Operations | Monitors collection outcomes and operational exceptions within agreed scope |
| DOKU Product | Defines product behavior and capability boundaries |
| Engineering / Integration | Supports technical investigation and event integrity |
| Merchant Success | Coordinates merchant action and improvement plans |
| Customer Support | Handles customer inquiries and routes unresolved cases |
| Finance | Validates collected, settled, refunded, and reconciled amounts |
| Risk / Compliance | Reviews applicable payment, customer communication, and risk controls |

This is a proposed functional model. Confirm actual DOKU team ownership and merchant contractual responsibilities before operational rollout.

## 4. Recovery state model

Use explicit states so operational teams can distinguish a payment outcome from the billing obligation.

| State | Meaning | Next action |
|---|---|---|
| Due | Billing has reached its due point | Initiate eligible collection |
| Processing | Payment attempt is in progress | Wait for outcome |
| Pending / Unknown | Final payment result is not established | Inquiry or reconciliation |
| Paid | Billing obligation has been collected | Close collection workflow |
| Failed | Definitive payment failure | Evaluate recovery eligibility |
| Retry Eligible | Retry permitted under applicable rules | Schedule approved retry |
| Retry Scheduled | Retry is scheduled | Monitor execution |
| Customer Action Required | Customer needs to take action | Notify through approved channel |
| Overdue | Billing remains unpaid after due date | Follow grace and collection rules |
| Partially Paid | Some value has been collected | Evaluate remaining balance |
| Cancelled / Voided | Obligation is no longer valid | Stop collection |
| Written Off / Closed | Merchant has finalized the obligation | Stop recovery under merchant policy |

These are recommended operational labels. They do not imply every state exists as a native FlexiBill status.

## 5. Classify failures before recovery

### 5.1 Failure categories

| Failure category | Example | Recovery direction |
|---|---|---|
| Insufficient funds | Available balance is insufficient | Consider a later permitted attempt |
| Issuer decline | Issuer rejects the transaction | Review decline reason and permitted action |
| Invalid or expired credential | Payment credential is unusable | Customer credential update, if supported |
| Authentication failure | Required authentication is not completed | Customer action or assisted payment |
| Technical failure | Network or processing issue | Investigate status and technical cause |
| Timeout / unknown | No definitive outcome received | Resolve transaction status before retry |
| Configuration error | Merchant setup or request is invalid | Correct configuration before another attempt |
| Risk / compliance rejection | Transaction rejected by controls | Follow applicable risk and compliance process |
| Billing error | Amount, schedule, or obligation is incorrect | Correct or cancel billing as authorized |

### 5.2 Failure classification principles

- Use source payment response codes as evidence.
- Maintain a normalized business-level failure taxonomy.
- Preserve the original response code for investigation.
- Avoid classifying unknown failures as insufficient funds.
- Distinguish customer-correctable issues from merchant or platform issues.
- Do not repeatedly retry a failure without understanding its eligibility.

## 6. Retry eligibility and safety controls

Before scheduling a retry, verify:

1. The billing obligation is valid and still collectible.
2. The previous transaction has a definitive outcome.
3. No successful payment already fulfilled the billing.
4. No duplicate or concurrent attempt is in progress.
5. Merchant retry rules permit another attempt.
6. The payment credential remains valid and usable.
7. The customer has not cancelled or otherwise ended the obligation.
8. The retry is within the applicable grace and contractual limits.
9. Any required customer notification or authorization is satisfied.
10. The payment method and integration support the proposed action.

### 6.1 Retry decision matrix

| Condition | Recommended operational decision |
|---|---|
| Definitive failure, eligible billing | Evaluate permitted retry |
| Pending or unknown outcome | Resolve status first |
| Billing already paid | Stop recovery |
| Duplicate attempt suspected | Investigate before proceeding |
| Expired or invalid credential | Request supported credential update |
| Customer cancellation confirmed | Stop collection according to merchant rules |
| Billing amount incorrect | Correct or cancel through authorized process |
| Risk or compliance rejection | Follow the relevant control process |
| Grace period expired | Apply merchant policy; do not assume retry remains eligible |

### 6.2 Retry policy dimensions

A merchant-approved retry policy should specify:

- Maximum retry attempts.
- Minimum time between attempts.
- Permitted retry days and hours.
- Retry eligibility by failure reason.
- Grace-period end.
- Customer notification requirements.
- Duplicate prevention controls.
- Treatment of weekends and public holidays.
- Handling of partial payments.
- Final resolution after retry exhaustion.

These parameters are merchant-specific. Do not publish a universal FlexiBill retry schedule without product and operational confirmation.

## 7. Illustrative recovery schedule

The following is an example framework for discussion, not a default system configuration.

| Event | Illustrative timing | Operational action |
|---|---|---|
| Initial collection | Billing due date | Execute eligible collection |
| First failure | After definitive failure | Classify outcome |
| Recovery assessment | Same operational cycle | Check status, eligibility, and duplicate risk |
| Retry opportunity 1 | Merchant-approved window | Retry if permitted |
| Customer follow-up | Based on failure type and policy | Explain issue and available action |
| Retry opportunity 2 | Later approved window | Retry if permitted |
| Grace-period review | Before applicable deadline | Review subscriber and billing status |
| Final resolution | At merchant-defined cutoff | Paid, overdue, cancelled, lapsed, or other final state |

Actual timings must reflect merchant contracts, local rules, payment method, and customer communication policy.

## 8. Customer communication strategy

Customer communication should be timely, accurate, and actionable.

### 8.1 Communication objectives

- Inform customers of unsuccessful collection.
- Explain the next required action.
- Provide a safe way to update payment details or complete payment where supported.
- Avoid duplicate payment.
- Clarify due date and applicable grace period.
- Explain the impact of continued non-payment using merchant-approved wording.
- Provide a support contact or escalation route.

### 8.2 Communication stages

| Stage | Objective | Example message intent |
|---|---|---|
| Upcoming due date | Reduce avoidable failure | Remind customer of upcoming billing |
| Initial failure | Inform and guide | Explain that collection was unsuccessful |
| Retry scheduled | Set expectation | Explain that another permitted attempt may occur |
| Customer action required | Enable resolution | Ask customer to update payment details or complete an approved action |
| Overdue | Clarify outstanding obligation | State amount and due status |
| Final reminder | Explain next steps | Refer to merchant policy and support channel |
| Successful recovery | Confirm resolution | Confirm payment or updated billing status |

### 8.3 Communication channels

Use only channels that are confirmed, authorized, and configured for the merchant.

Potential channels include:
- Email.
- SMS.
- Merchant application or portal notification.
- Merchant website or customer account.
- WhatsApp or PayChat workflows where the relevant integration and customer-facing capability are confirmed.
- Customer support outreach.

Do not assume that a PayChat bulk-upload billing capability automatically provides a complete automated WhatsApp dunning journey.

### 8.4 Message content checklist

Each communication should be reviewed for:
- Merchant identity.
- Customer identity or appropriate reference.
- Billing reference.
- Amount and currency.
- Due date or overdue status.
- Payment status accuracy.
- Clear next action.
- Safe payment or account-update route.
- Support contact.
- Privacy and consent requirements.

Never include full card numbers, security codes, passwords, or other sensitive payment credentials in customer messages.

## 9. Customer payment update journey

When a payment credential is invalid or expired, the customer may need to update their payment details.

A controlled journey should:

1. Identify the affected billing or subscription.
2. Explain why action is required.
3. Authenticate the customer through the merchant's approved process.
4. Present the supported payment update mechanism.
5. Confirm the update result.
6. Verify that the new payment method is eligible for future collection.
7. Reassess the outstanding billing.
8. Initiate a new collection only when permitted.
9. Confirm the outcome to the customer.

**Capability validation:** The exact payment credential update flow depends on the integration, tokenization model, supported payment method, and merchant configuration. Do not promise a universal card-update or payment-method migration capability.

## 10. Grace period and subscription-state management

A grace period defines the merchant-approved interval during which an overdue customer may retain some or all service privileges.

It is not automatically the same as the payment retry window.

### 10.1 State management

| Condition | Possible merchant policy |
|---|---|
| Payment due | Subscription remains active |
| Initial failure | Subscription remains active during evaluation |
| Overdue within grace | Access may continue |
| Recovery during grace | Restore normal collection state |
| Grace expired | Suspend, lapse, cancel, or apply another agreed policy |
| Payment after lapse | Reinstate only under applicable merchant rules |

### 10.2 Important distinctions

- Payment status does not automatically determine entitlement status.
- Subscription status does not automatically prove payment collection.
- Grace-period rules are merchant-specific.
- Insurance policy lapse and reinstatement rules must be confirmed with the insurer.
- A 90-day grace period may apply in some bancassurance arrangements but must never be assumed for every insurance product.

FlexiBill monitoring should preserve the source status and the merchant's final business interpretation.

## 11. Recovery operations dashboard

The daily recovery dashboard should include:

### Billing population
- Unique billings due.
- Billing value due.
- Unique billings overdue.
- Overdue billing value.
- Billing aging.

### Payment outcomes
- Initial payment attempts.
- Successful attempts.
- Definitive failed attempts.
- Pending or unknown attempts.
- Payment success value.

### Recovery performance
- Initially failed unique billings.
- Retry-eligible billings.
- Retry attempts.
- Recovered unique billings.
- Recovered value.
- Recovery rate.
- Median time to recovery.

### Customer action
- Customers requiring payment update.
- Notifications sent and delivery results where available.
- Outstanding customer actions.
- Support cases related to collection.

### Financial exposure
- Initially uncollected billing value.
- Recovered value.
- Remaining outstanding exposure.
- Confirmed loss, if validated.
- Reconciliation exceptions.

Always display the reporting cutoff, currency, observation window, and data freshness.

## 12. Daily operating procedure

### Start of day

1. Review prior-day billing and payment results.
2. Identify pending or unresolved transactions.
3. Reconcile transaction outcomes where required.
4. Refresh retry-eligible billing population.
5. Review overdue billing and grace-period exceptions.
6. Identify high-value and high-priority merchants.

### During the day

1. Monitor payment and billing events.
2. Investigate technical and configuration failures.
3. Track approved recovery actions.
4. Monitor customer communication exceptions.
5. Escalate duplicate-payment risks.
6. Coordinate merchant action where needed.

### End of day

1. Confirm successful recovery.
2. Review outstanding exceptions.
3. Check billing and transaction status consistency.
4. Record unresolved items and accountable owners.
5. Publish operational summary.
6. Carry forward actions with deadlines.

## 13. Exception handling

| Exception | Immediate response | Escalation |
|---|---|---|
| Payment status unknown | Inquiry and transaction resolution | Engineering / Operations |
| Suspected duplicate charge | Stop further attempts and investigate | Operations
