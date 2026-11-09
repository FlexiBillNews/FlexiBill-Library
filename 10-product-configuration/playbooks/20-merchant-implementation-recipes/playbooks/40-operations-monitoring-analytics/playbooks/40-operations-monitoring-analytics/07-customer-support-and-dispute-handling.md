# FlexiBill Customer Support & Dispute Handling

**Document type:** Customer Support, Merchant Support & Dispute Operations Playbook  
**Audience:** Customer Support, Merchant Success, Operations, Product, Engineering, Finance, Risk  
**Markets:** Indonesia (ID) and Malaysia (MY)  
**Status:** Proposed operating framework — validate actual DOKU support ownership, merchant agreements, payment-method rules, and local requirements before adoption

---

## 1. Purpose

This playbook establishes a consistent approach to customer and merchant support for FlexiBill billing, subscription, and payment journeys.

It covers:
- Billing questions and incorrect invoices.
- Failed, pending, and successful payment inquiries.
- Duplicate payment concerns.
- Refund and reversal inquiries.
- Subscription activation, renewal, cancellation, and expiry.
- Payment credential update issues.
- Billing Portal and Member Center access.
- Merchant integration and operational questions.
- Payment disputes and chargebacks.
- Complaints involving collection frequency or customer communication.

The objective is to resolve issues accurately, protect customers, preserve merchant control, and maintain a clear audit trail.

**Core principle:** Every support case must be investigated against the actual billing obligation, transaction status, and merchant policy. A payment attempt, billing record, and subscription state are not interchangeable.

## 2. Support operating model

FlexiBill support involves several parties.

| Party | Primary responsibility |
|---|---|
| Customer | Raises an inquiry, complaint, or request |
| Merchant | Owns the commercial relationship, billing obligation, subscription terms, and customer policy |
| DOKU Customer / Merchant Support | Handles issues within the agreed DOKU support scope |
| DOKU Operations | Investigates relevant payment and billing operational exceptions |
| Product | Clarifies expected product behavior and capability |
| Engineering / Integration | Investigates technical and integration issues |
| Finance | Validates settlement, fees, refunds, and reconciliation |
| Risk / Disputes | Handles relevant risk, dispute, and payment-scheme processes |

The exact customer-facing support route must be defined by the merchant's operating model and DOKU agreement.

Do not assume that DOKU directly owns every merchant's customer support relationship.

## 3. Support principles

1. Acknowledge the issue and establish the customer's intended outcome.
2. Verify identity through the approved process.
3. Use transaction and billing references to investigate.
4. Confirm the final payment outcome before advising the customer.
5. Avoid asking for sensitive payment credentials.
6. Explain merchant-specific subscription and cancellation rules accurately.
7. Protect customers from duplicate payment or unauthorized collection.
8. Escalate disputes and potential fraud through approved channels.
9. Record the investigation and resolution.
10. Keep customer and merchant communication consistent.

## 4. Support case taxonomy

Use a consistent category and subcategory structure.

| Category | Example subcategories |
|---|---|
| Billing inquiry | Amount, due date, invoice, duplicate billing |
| Payment inquiry | Failed, pending, successful, unknown status |
| Collection complaint | Unexpected debit, repeated debit, amount dispute |
| Refund / reversal | Refund status, partial refund, reversal |
| Subscription | Activation, renewal, pause, cancellation, expiry |
| Payment credential | Expired card, failed update, replacement credential |
| Customer access | Billing Portal, Member Center, login or registration |
| Merchant integration | API, webhook, billing generation, status mismatch |
| Notification | Missing reminder, incorrect message, payment confirmation |
| Reconciliation | Payment record mismatch, settlement question |
| Dispute / chargeback | Unauthorized transaction, service not received, duplicate charge |
| Technical issue | Application, portal, or payment journey unavailable |

Each case should have:
- A unique case reference.
- Category and subcategory.
- Merchant and country.
- Billing or transaction reference, where applicable.
- Customer impact.
- Priority.
- Current owner.
- Status.
- Next action and due date.

## 5. Priority classification

The following priority model is proposed and should be aligned with approved DOKU and merchant support policies.

| Priority | Description | Example |
|---|---|---|
| P1 — Critical | Potential unauthorized collection, widespread customer impact, suspected fraud or sensitive-data exposure | Multiple customers report unexpected duplicate debits |
| P2 — High | Significant financial or service impact for a customer or merchant | Customer paid but subscription remains suspended |
| P3 — Normal | Individual billing or payment inquiry with limited impact | Customer asks about an invoice amount |
| P4 — Low | General information or non-urgent guidance | Customer asks how recurring billing works |

Potential security, privacy, fraud, and financial-integrity concerns must be escalated to the relevant specialist process regardless of ordinary ticket priority.

## 6. Case intake and information requirements

### 6.1 Minimum information

| Field | Purpose |
|---|---|
| Case reference | Track the support request |
| Customer / merchant reference | Identify the relevant account |
| Merchant ID | Establish merchant ownership |
| Country | Apply the correct market rules |
| Billing ID | Identify the billing obligation |
| Transaction ID | Identify a payment transaction |
| Attempt reference | Identify a specific attempt, where available |
| Amount and currency | Validate financial details |
| Date and time | Locate the event |
| Payment method | Identify the payment route |
| Issue description | Understand the customer's concern |
| Desired resolution | Clarify what the customer expects |
| Supporting evidence | Approved evidence relevant to the case |

Not every case requires every field. Collect only what is necessary.

### 6.2 Privacy and security

Never request:
- Full card number.
- Card security code.
- Internet banking password.
- One-time password.
- Payment PIN.
- Full authentication credentials.

Use approved secure verification and evidence channels.

Do not expose another customer's billing or payment information when investigating a shared merchant account.

## 7. Standard support workflow

1. **Receive:** Register the case and acknowledge it.
2. **Classify:** Assign category, priority, market, and merchant.
3. **Verify:** Authenticate the customer or merchant contact using approved procedures.
4. **Identify:** Locate the billing and relevant transaction history.
5. **Investigate:** Review status, timestamps, amount, payment method, and relevant merchant records.
6. **Determine ownership:** Identify whether the next action belongs to the merchant, DOKU, a partner, or the customer.
7. **Resolve or escalate:** Apply an authorized resolution or transfer the case with evidence.
8. **Communicate:** Explain the result and next action.
9. **Close:** Record the resolution and evidence.
10. **Learn:** Tag recurring patterns for product and operational improvement.

Do not close a case solely because it has been transferred to another team.

## 8. Billing and invoice inquiries

### Common issues

- Customer does not recognize a billing amount.
- Billing appears duplicated.
- Billing due date is incorrect.
- Customer believes the service was cancelled.
- Customer disputes tax, discount, or proration.
- Customer cannot locate an invoice.

### Investigation

1. Identify the Billing ID.
2. Confirm merchant and customer references.
3. Review billing creation date and due date.
4. Validate amount and currency.
5. Check collection, plan, or pricing configuration as relevant.
6. Review discounts, taxes, and adjustments where available.
7. Compare with the merchant's contractual terms.
8. Confirm whether the billing is valid, modified, cancelled, or duplicated.

### Resolution

- Explain the billing basis using merchant-approved terms.
- Refer commercial or contractual questions to the merchant.
- Correct inaccurate billing through an authorized merchant process.
- Stop collection of invalid obligations where authorized.
- Preserve the original and corrected billing references.

A payment failure does not automatically invalidate the billing obligation.

## 9. Failed and pending payment inquiries

### 9.1 Failed payment

Investigate:
- Transaction ID and attempt reference.
- Final transaction status.
- Failure reason.
- Payment method and issuer response, where available.
- Related Billing ID.
- Whether a later attempt succeeded.

Explain the next action based on the actual failure reason and merchant policy.

Do not promise that another attempt will succeed.

### 9.2 Pending or unknown payment

A pending transaction may still be processing or awaiting final status resolution.

Procedure:
1. Locate the transaction.
2. Check the latest available status.
3. Use the appropriate transaction inquiry or reconciliation route.
4. Review relevant event and webhook history.
5. Avoid initiating another charge until the outcome is established.
6. Communicate that the status is being verified.
7. Update the customer after a definitive outcome is available.

Do not label an unresolved transaction as failed merely because a response timed out.

### 9.3 Successful payment not reflected in billing

Investigate:
- Successful transaction record.
- Billing-to-transaction mapping.
- Webhook delivery and processing.
- Merchant-side billing update.
- Subscription-state transition.
- Reconciliation records.

Coordinate with the merchant to correct the billing or subscription state through an authorized process.

## 10. Duplicate payment complaints

Duplicate payment complaints require careful investigation because multiple attempts do not necessarily mean multiple successful charges.

### Investigation checklist

1. Collect the relevant transaction references.
2. Identify the Billing ID.
3. List all attempts associated with the billing.
4. Identify definitive successful transactions.
5. Compare amount, currency, and timestamps.
6. Check whether any transaction was reversed or refunded.
7. Confirm whether the records represent separate legitimate billing obligations.
8. Check settlement and reconciliation status where necessary.

### Resolution

- If only one payment succeeded, explain the verified result.
- If multiple payments succeeded for one obligation, escalate for merchant and Finance review.
- Follow the approved refund or adjustment process.
- Confirm the final financial outcome.
- Investigate duplicate retry, webhook, or billing-generation behavior if systemic.

Never promise an immediate refund without confirming authority, eligibility, and processing requirements.

## 11. Refund, reversal, and adjustment inquiries

Distinguish the following:

| Term | Meaning |
|---|---|
| Refund | A payment is returned through an applicable refund process |
| Reversal | A transaction is reversed through the relevant payment process |
| Void | An eligible transaction or authorization is cancelled before completion under applicable rules |
| Credit note | Merchant-side adjustment to an invoiced obligation |
| Billing cancellation | Merchant cancels a billing obligation |
| Subscription cancellation | Merchant or customer ends a subscription under applicable terms |

These are not interchangeable.

### Investigation

- Original transaction reference.
- Original billing reference.
- Refund or reversal reference.
- Amount and currency.
- Current status.
- Merchant approval or instruction.
- Settlement implications.
- Customer communication.

### Resolution

Explain the confirmed status and next steps.

Any refund timing estimate must come from the applicable payment method, partner, and approved policy. Do not invent universal processing timelines.

## 12. Subscription lifecycle inquiries

### Common issues

- Subscription not activated after payment.
- Renewal failed.
- Customer wants to cancel.
- Subscription remains active after cancellation request.
- Customer cannot pause or resume.
- Plan or billing amount changed unexpectedly.
- Subscription expired or was suspended.

### Investigation

1. Identify subscriber and subscription references.
2. Review current subscription state.
3. Check relevant lifecycle events.
4. Verify billing and payment history.
5. Review merchant terms and lifecycle rules.
6. Identify whether the requested action is supported in the current merchant journey.
7. Determine the system responsible for the state transition.

### Important distinctions

- A successful payment does not by itself prove that every subscription-state update has completed.
- A failed payment does not automatically mean immediate cancellation.
- Pause, resume, upgrade, downgrade, proration, and cancellation behavior depends on the configured product and merchant workflow.
- Do not promise a plan-change or lifecycle API capability without validating current availability.

The merchant remains responsible for the contractual subscription terms and final customer entitlement policy.

## 13. Billing Portal and Member Center support

### Billing Portal inquiries

Potential issues:
- Customer cannot open a billing link.
- Invoice is not visible.
- Customer cannot complete payment.
- Payment status is not updated.
- Portal content differs from merchant expectations.

Check:
- Link validity and expiry.
- Customer identity and access.
- Billing reference.
- Portal configuration.
- Payment status.
- Merchant integration and page behavior.

### Member Center inquiries

Potential issues:
- Customer cannot register.
- Customer cannot log in.
- Membership record is missing.
- Customer cannot access billing information.
- Customer data does not match the merchant record.

Validate the exact implementation.

**Important capability distinction:** Member Center API readiness and customer-facing registration frontend readiness are separate. Do not assume that a ready API means the merchant's customer-facing journey is already available.

## 14. Payment credential update support

When customers cannot update their payment method:

1. Verify customer identity through the approved process.
2. Confirm the merchant's supported update journey.
3. Check whether the existing credential is expired, invalid, or otherwise unusable.
4. Review any update error.
5. Confirm whether the new credential was successfully registered.
6. Check whether another collection attempt is required and permitted.
7. Confirm the next billing action.

Do not ask customers to send card details through email, chat, or support tickets.

Payment credential update capability depends on the relevant payment method, integration, tokenization, and merchant configuration.

## 15. Dispute and chargeback handling

A dispute is a formal or informal challenge to a payment or billing obligation. A chargeback is a payment-method-specific dispute process that may involve an issuer, scheme, acquirer, or other relevant parties.

Not every customer complaint is a chargeback.

### 15.1 Dispute categories

| Category | Example |
|---|---|
| Unauthorized transaction | Customer does not recognize the payment |
| Duplicate transaction | Customer believes the same obligation was charged more than once |
| Incorrect amount | Charged amount differs from expected amount |
| Cancelled subscription | Collection occurred after an alleged cancellation |
| Service not received | Customer claims the service was not provided |
| Credit not processed | Refund or adjustment was expected |
| Subscription terms | Customer disputes recurring billing terms |
| Other | Additional payment-specific reason |

### 15.2 Initial handling

1. Record the dispute or complaint.
2. Identify the transaction and Billing ID.
3. Verify the payment outcome.
4. Identify the merchant and relevant contractual terms.
5. Determine the applicable dispute process and deadline.
6. Preserve evidence.
7. Escalate to the authorized dispute or Risk owner.
8. Track submission and outcome.

### 15.3 Evidence checklist

Depending on the dispute reason and applicable payment rules, evidence may include:

- Transaction reference and payment status.
- Billing record and invoice.
- Customer subscription or policy terms.
- Customer consent or authorization evidence, where applicable.
- Registration or membership record.
- Service delivery or usage evidence.
- Customer communication history.
- Cancellation or refund records.
- Relevant timestamps.
- Merchant correspondence.

Collect only evidence relevant to the case and handle it through approved secure channels.

### 15.4 Dispute ownership

The merchant generally owns the underlying commercial relationship and evidence of the service or subscription terms.

DOKU and relevant payment partners may have responsibilities for payment processing, dispute routing, evidence requirements, or formal submission depending on the agreement and payment method.

Confirm the actual contractual process before assigning ownership or promising an outcome.

## 16. Customer communication standards

Every communication should be:

- Clear.
- Accurate.
- Respectful.
- Specific to the actual issue.
- Consistent with the confirmed payment status.
- Free of unnecessary technical jargon.
- Clear about who owns the next action.

### Example: Pending payment

"Your payment is still being verified. We are checking the transaction status to avoid asking you to pay twice. We will update you when the final status is confirmed."

### Example: Failed payment

"We could not complete the payment for this billing. Please review the payment method or follow the merchant's approved payment instructions. If you need help, contact the merchant support team."

### Example: Successful payment not reflected

"Our records show a successful payment transaction. We are checking the billing update with the relevant team so that the payment is reflected correctly."

### Example: Billing clarification

"The billing amount is being checked against the merchant's plan and billing details. The merchant will confirm the applicable amount and any relevant adjustment."

These are illustrative templates. Adapt them to merchant identity, local language, customer consent, and approved communication policies.

## 17. Support SLA and service measurement

The following are proposed measurement dimensions, not contractual commitments.

| Measure | Definition |
|---|---|
| First response time | Case creation to first meaningful response |
| Resolution time | Case creation to confirmed resolution |
| First contact resolution | Cases resolved without transfer or repeat contact / eligible cases |
| Reopen rate | Closed cases reopened / eligible closed cases |
| Escalation rate | Cases escalated to specialist teams / eligible cases |
| Complaint rate | Relevant complaints / defined customer or transaction population |
| Duplicate payment complaint rate | Duplicate payment complaints / eligible successful payment transactions |
| Dispute rate | Formal disputes / eligible successful transactions |
| Customer satisfaction | Survey-based customer feedback using a defined method |

Segment reporting by market, merchant, category, priority, and integration model.

Do not combine ID and MY results without considering differences in volume, product configuration, and operating rules.

## 18. Escalation matrix

| Case type | First owner | Specialist escalation |
|---|---|---|
| Billing amount or schedule | Merchant Support | Merchant / Product |
| Payment status | Support / Operations | Payment Operations / Engineering |
| Duplicate collection | Operations | Finance / Merchant / Risk as applicable |
| Refund or reversal | Merchant / Support | Finance / Payment Operations |
| Subscription lifecycle | Merchant Support | Product / Integration |
| Portal or Member Center | Support | Product / Engineering |
| API / webhook | Merchant technical support | Integration / Engineering |
| Settlement mismatch | Finance Support | Finance / Operations |
| Formal dispute / chargeback | Authorized dispute team | Risk / Payment Partner |
| Security or privacy concern | Approved security process | Security / Privacy / Legal as applicable |

Insert actual DOKU team names, support channels, escalation contacts, and contractual response targets from approved internal sources.

## 19. Support dashboard

Recommended reporting:

### Case volume
- Total cases.
- Open cases.
- New cases.
- Resolved cases.
- Reopened cases.
- Cases by priority and category.

### Customer impact
- Billing inquiries.
- Payment inquiries.
- Duplicate payment complaints.
- Subscription complaints.
- Refund inquiries.
- Formal disputes.

### Operational performance
- First response time.
- Resolution time.
- Escalation rate.
- First contact resolution.
- Backlog aging.
- Cases exceeding approved SLA.

### Root-cause insight
- Payment failure reasons.
- Billing configuration issues.
- Portal and Member Center issues.
- Integration errors.
- Notification issues.
- Repeated merchant-specific problems.

### Financial indicators
- Billing value under inquiry.
- Duplicate payment value under investigation.
- Refund value under review.
- Disputed transaction value.
- Reconciliation exceptions.

Do not publish customer-level personal information in general management dashboards.

## 20. Continuous improvement

Use support and dispute data to identify recurring product and operational issues.

| Support insight | Potential improvement |
|---|---|
| Repeated billing confusion | Improve invoice and billing explanations |
| Pending payment complaints | Improve status inquiry and communication |
| Duplicate collection complaints | Strengthen idempotency and retry controls |
| Subscription cancellation complaints | Clarify merchant cancellation journey |
| Credential update failures | Improve supported payment update UX |
| Portal access issues | Improve link, authentication, and access handling |
| Repeated integration cases | Improve documentation and integration diagnostics |
| High dispute concentration | Review merchant terms, customer consent, and evidence quality |

Review recurring issues with Product, Engineering, Operations, Merchant Success, and Finance.

## 21. Operational readiness checklist

- [ ] Support ownership documented.
- [ ] Customer and merchant intake routes defined.
- [ ] Case taxonomy and priority model approved.
- [ ] Identity verification process available.
- [ ] Sensitive-data handling rules communicated.
- [ ] Billing and transaction references accessible.
- [ ] Pending payment investigation process defined.
- [ ] Duplicate collection escalation established.
- [ ] Refund and reversal ownership confirmed.
- [ ] Dispute evidence process documented.
- [ ] ID and MY support rules validated separately.
- [ ] Merchant communication templates approved.
- [ ] Escalation contacts and actual SLAs inserted.
- [ ] Support dashboard and reporting owner assigned.

## 22. Final principles

1. Investigate the billing obligation and payment transaction together.
2. Do not treat pending status as confirmed failure.
3. Never request sensitive payment credentials.
4. Separate customer complaints from formal payment disputes.
5. Protect customers from duplicate collection.
6. Keep merchant commercial and subscription rules authoritative.
7. Validate refund, reversal, and chargeback ownership.
8. Preserve traceable evidence and timestamps.
9. Communicate confirmed facts and clear next actions.
10. Use support data to improve FlexiBill product and operational quality.

**The objective is to turn every support interaction into a reliable resolution, a protected customer experience, and a source of actionable product and operational insight.**
