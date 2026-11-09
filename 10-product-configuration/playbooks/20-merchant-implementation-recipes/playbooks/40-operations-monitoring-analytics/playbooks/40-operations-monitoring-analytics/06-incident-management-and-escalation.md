# FlexiBill Incident Management & Escalation

**Document type:** Operational Incident Management Playbook  
**Audience:** Product, Engineering, Operations, Merchant Success, Finance, Customer Support, Risk  
**Markets:** Indonesia (ID) and Malaysia (MY)  
**Status:** Proposed operational framework — confirm actual DOKU incident policies, service ownership, and contractual SLAs before adoption

---

## 1. Purpose

This playbook defines how incidents affecting FlexiBill are identified, classified, escalated, investigated, resolved, and reviewed.

FlexiBill incidents may affect:
- Billing generation.
- Subscription schedules.
- Payment authorization and collection.
- Transaction status and inquiry.
- Webhook delivery and processing.
- Customer notifications.
- Billing Portal and Member Center journeys.
- Merchant integrations.
- Reconciliation and settlement visibility.
- Customer and merchant reporting.

The objective is to protect customers and merchants, minimize financial and operational impact, restore service safely, and prevent recurrence.

**Core principle:** An incident is not resolved merely because a technical component is available again. The team must also establish the impact on billing obligations, payment outcomes, customer experience, and financial records.

## 2. Scope and incident definition

An incident is an unplanned interruption, degradation, or integrity issue that affects a FlexiBill service, integration, operational process, or customer/merchant outcome.

Examples include:
- Billing jobs not executing as expected.
- Duplicate billing generation.
- Payment collection failures beyond normal patterns.
- Incorrect or delayed payment status.
- Webhook delivery interruption.
- Incorrect subscription-state transitions.
- Customer payment update journey unavailable.
- Billing Portal access problems.
- Incorrect billing amount or schedule.
- Reconciliation mismatches.
- Data exposure or suspected security compromise.

A single customer issue may be a support case rather than a platform incident. Multiple related cases or evidence of a systemic problem may require incident escalation.

## 3. Incident management principles

1. Protect customers and prevent duplicate or unauthorized collection.
2. Establish the scope and severity using evidence.
3. Assign one incident owner.
4. Separate technical diagnosis from business-impact assessment.
5. Preserve transaction and billing traceability.
6. Communicate facts, uncertainty, and next update times.
7. Do not retry uncertain transactions without status resolution.
8. Validate financial and operational recovery.
9. Maintain an auditable incident record.
10. Complete a post-incident review for material incidents.

## 4. Incident categories

| Category | Examples | Potential impact |
|---|---|---|
| Billing | Billing generation delayed, missing, or duplicated | Incorrect or missed collection |
| Payment | Collection failure spike or payment processing issue | Merchant cash-flow impact |
| Transaction status | Incorrect, missing, or delayed final status | Duplicate payment risk or unresolved bills |
| Integration | API outage, authentication issue, webhook failure | Merchant workflow disruption |
| Subscription lifecycle | Incorrect activation, cancellation, pause, or expiry | Customer entitlement impact |
| Customer experience | Billing Portal or Member Center unavailable | Customer cannot complete an action |
| Notification | Reminder or payment confirmation not delivered | Customer confusion or delayed action |
| Finance | Settlement or reconciliation mismatch | Financial reporting uncertainty |
| Security / privacy | Suspected unauthorized access or data exposure | Customer, merchant, and regulatory risk |
| Data / reporting | Incorrect dashboard or export | Wrong operational decisions |

## 5. Severity classification

The following severity model is a proposed framework. It is not a statement of DOKU's existing incident severity policy or contractual SLA.

| Severity | Description | Example |
|---|---|---|
| SEV 1 — Critical | Widespread service failure, significant financial/customer impact, or serious security incident | Core collection unavailable across multiple merchants; suspected sensitive-data exposure |
| SEV 2 — High | Major merchant or market impact, significant degradation, or material billing/payment integrity issue | Large merchant collection disruption; duplicate billing affecting a customer population |
| SEV 3 — Medium | Limited scope or partial degradation with a workaround | One integration endpoint affected for a merchant |
| SEV 4 — Low | Minor issue with limited business impact | Non-critical reporting delay or cosmetic issue |

### 5.1 Severity assessment dimensions

Evaluate:
- Number of affected merchants.
- Number of affected customers or subscribers.
- Billing value and transaction value at risk.
- Payment or billing lifecycle stage.
- Duration and recurrence.
- Availability of a safe workaround.
- Customer impact.
- Data integrity and privacy impact.
- Financial and regulatory implications.
- Market scope: ID, MY, or both.

A low-volume issue may still be critical if it creates unauthorized collection or sensitive-data exposure.

### 5.2 Severity ownership

The incident lead should coordinate severity classification with the relevant technical and business owners.

Security, privacy, financial-integrity, or regulatory concerns should be escalated through the applicable specialist process even when the affected transaction volume is small.

## 6. Incident lifecycle

The standard incident lifecycle is:

1. Detect.
2. Record.
3. Triage.
4. Classify severity.
5. Assign incident owner.
6. Contain impact.
7. Investigate root cause.
8. Implement resolution or safe workaround.
9. Validate recovery.
10. Communicate closure.
11. Conduct post-incident review.
12. Track preventive actions.

Every material incident should have a unique incident reference and a traceable timeline.

## 7. Detection and alerting

Incidents may be detected through:

- Monitoring dashboards.
- Billing and payment exception reports.
- API availability and latency alerts.
- Webhook delivery monitoring.
- Merchant reports.
- Customer support cases.
- Finance and reconciliation exceptions.
- Engineering telemetry.
- Security monitoring.
- Partner or bank notifications.

### 7.1 Suggested detection signals

| Signal | Possible incident |
|---|---|
| Billing generation volume suddenly drops | Scheduler or billing-generation issue |
| Duplicate Billing IDs or duplicate obligations increase | Billing integrity issue |
| Payment success rate falls sharply | Payment route, issuer, or integration degradation |
| Pending transaction population grows | Status inquiry or processing issue |
| Webhook delivery drops | Event delivery disruption |
| API error rate rises | API or dependency degradation |
| Reconciliation mismatch increases | Transaction, settlement, or data integrity issue |
| Customer complaints spike | Customer-impacting service issue |
| Unexpected subscription-state changes | Lifecycle processing issue |

Alert thresholds should be calibrated to merchant volume, baseline behavior, and expected operating patterns.

Do not use one universal threshold for all merchants.

## 8. Initial triage checklist

When an incident is reported, capture:

| Field | Required information |
|---|---|
| Incident reference | Unique incident ID |
| Reported by | Person, team, merchant, or monitoring source |
| First observed time | Timestamp and timezone |
| Detection time | When the team became aware |
| Affected market | ID, MY, or both |
| Affected merchant | Merchant ID and name, where permitted |
| Affected service | Billing, payment, API, webhook, portal, etc. |
| Integration model | DOKU-hosted, API/H2H, Hybrid, or other validated model |
| Impacted period | Start and end or ongoing |
| Customer impact | Known or suspected impact |
| Billing impact | Count and value, if known |
| Payment impact | Count and value, if known |
| Evidence | Logs, transaction references, screenshots, reports |
| Current workaround | Available, unavailable, or under investigation |
| Initial severity | Proposed classification |
| Incident owner | Named accountable lead |

Use secure, approved channels for sensitive operational data. Do not paste full payment credentials or unnecessary personal data into incident records.

## 9. Immediate containment

Containment aims to stop additional impact while investigation continues.

Potential actions include:

- Pause an affected automated job when authorized.
- Stop duplicate or unsafe retry execution.
- Prevent repeated processing of the same event.
- Isolate a failing integration or dependency.
- Route affected cases into manual review.
- Notify affected merchants through approved channels.
- Preserve relevant logs and transaction references.
- Prevent incorrect subscription-state changes.
- Escalate suspected security or privacy events immediately.

Containment must be authorized by the appropriate service owner and follow established change and operational controls.

Do not disable an entire collection flow when a narrower safe containment action is available.

## 10. Investigation framework

Investigate across five layers.

### 10.1 Billing layer

Check:
- Was the billing created?
- Was the amount correct?
- Was the due date correct?
- Was the billing duplicated?
- Was the billing linked to the correct subscriber or subscription?
- Did the expected billing job execute?
- Was the billing cancelled or modified?

### 10.2 Payment layer

Check:
- Was a payment attempt initiated?
- Was it accepted by the relevant processing system?
- What was the final transaction status?
- Was the outcome pending or unknown?
- Was the transaction duplicated?
- Did the issuer, bank, or payment method return an error?
- Was a retry initiated correctly?

### 10.3 Integration layer

Check:
- API request and response.
- Authentication and authorization.
- Request identifiers and idempotency.
- Webhook delivery and acknowledgment.
- Event ordering and duplicate processing.
- Timeout and retry behavior.
- Dependency availability.

### 10.4 Subscription and customer layer

Check:
- Did the subscription state change correctly?
- Was the customer entitled to the service?
- Was a cancellation or pause action received?
- Did the customer receive the correct notification?
- Was a payment update action available?
- Did the incident create customer confusion or duplicate action?

### 10.5 Finance and reconciliation layer

Check:
- Did successful transactions appear in the expected financial records?
- Was settlement completed?
- Are there missing or duplicate settlement lines?
- Were fees, refunds, reversals, and adjustments applied correctly?
- Are there unresolved billing-to-transaction mismatches?

## 11. Incident-specific runbooks

### 11.1 Billing generation failure

**Symptoms**
- Expected billing records are missing.
- Billing volume is lower than forecast.
- Billing schedule execution is delayed.

**Investigation**
1. Identify affected merchants and billing periods.
2. Verify schedule and configuration.
3. Inspect job execution and error logs.
4. Compare expected and actual unique Billing IDs.
5. Check for partial execution or duplicate processing.

**Recovery**
- Restore the approved job or configuration.
- Validate the missing population.
- Generate only eligible missing obligations.
- Check for duplicates before reprocessing.
- Reconcile the final billing population.

### 11.2 Duplicate billing generation

**Symptoms**
- Multiple billing records represent the same obligation.
- Customer receives duplicate invoices or payment requests.

**Investigation**
1. Identify duplicate keys and affected customers.
2. Confirm whether multiple records are legitimate billing obligations.
3. Check job retries and idempotency behavior.
4. Determine whether any duplicate payment was collected.

**Recovery**
- Stop further duplicate generation.
- Identify the valid billing obligation.
- Follow merchant-authorized void or correction procedures.
- Investigate collected duplicate amounts.
- Confirm customer communication and financial resolution.

### 11.3 Payment collection degradation

**Symptoms**
- Payment success declines.
- Failure or pending rates increase.
- Merchant reports an unusual collection drop.

**Investigation**
1. Compare with the merchant's historical baseline.
2. Segment by payment method, issuer, amount, and failure reason.
3. Check payment route and dependency status.
4. Separate definitive declines from pending outcomes.
5. Verify whether the issue is merchant-specific or broader.

**Recovery**
- Apply an approved workaround if available.
- Avoid duplicate attempts for unresolved transactions.
- Monitor the affected segment after restoration.
- Measure recovered billings and remaining exposure.

### 11.4 Pending transaction accumulation

**Symptoms**
- Unresolved transaction count or value increases.
- Merchant cannot determine whether payments succeeded.

**Investigation**
1. Identify affected transactions.
2. Check transaction inquiry and status resolution.
3. Review callback and webhook delivery.
4. Compare processing and merchant records.
5. Identify any transactions at risk of duplicate collection.

**Recovery**
- Resolve final transaction outcomes.
- Update billing status through the approved process.
- Retry only transactions confirmed eligible for retry.
- Reconcile affected records.

### 11.5 Webhook delivery failure

**Symptoms**
- Merchant does not receive expected events.
- Webhook retries or failed deliveries increase.
- Merchant records differ from DOKU records.

**Investigation**
1. Identify affected event types and period.
2. Check destination endpoint availability.
3. Inspect delivery response and retry history.
4. Check event identifiers and duplicate handling.
5. Confirm merchant processing behavior.

**Recovery**
- Restore endpoint or configuration.
- Use the approved event recovery or reconciliation mechanism.
- Ensure duplicate events are handled safely.
- Validate business-state consistency after recovery.

### 11.6 Incorrect subscription state

**Symptoms**
- Customer is suspended despite successful payment.
- Cancelled subscriptions continue to be collected.
- Access does not match merchant rules.

**Investigation**
1. Compare billing, transaction, and subscription histories.
2. Identify the event that triggered the state transition.
3. Check event order and processing result.
4. Confirm the merchant's lifecycle policy.

**Recovery**
- Correct the state through the authorized process.
- Stop ineligible future collection where required.
- Validate customer access.
- Review affected subscribers for additional cases.

### 11.7 Settlement or reconciliation mismatch

**Symptoms**
- Successful transaction value differs from settlement records.
- Finance identifies missing or duplicate records.

**Investigation**
1. Define the affected settlement period.
2. Match transaction and settlement identifiers.
3. Compare amount, currency, fees, and status.
4. Identify timing differences, refunds, and reversals.
5. Determine whether the issue is data, timing, or financial processing.

**Recovery**
- Reconcile affected records.
- Escalate financial discrepancies to the relevant Finance owner.
- Correct reporting only through approved controls.
- Maintain a traceable adjustment record.

### 11.8 Security or privacy incident

**Symptoms**
- Suspected unauthorized access.
- Unexpected exposure or misuse of customer or merchant information.
- Compromised credentials or suspicious activity.

**Response**
1. Escalate immediately through the applicable Security and Privacy incident process.
2. Preserve evidence.
3. Restrict access or contain the affected component when authorized.
4. Avoid unnecessary sharing of sensitive data.
5. Follow approved investigation and notification procedures.
6. Do not independently determine regulatory notification obligations.

Security and Privacy teams must direct the response according to applicable internal policies and local requirements.

## 12. Escalation matrix

The following is a proposed functional escalation model.

| Incident area | First response | Specialist escalation | Business coordination |
|---|---|---|---|
| Billing generation | Operations / Engineering | Product / Integration | Merchant Success |
| Payment degradation | Operations | Payment Engineering / relevant partner team | Merchant Success |
| API / webhook | Integration support | Engineering | Merchant technical team |
| Subscription lifecycle | Product / Operations | Engineering | Merchant |
| Customer portal | Support / Operations | Product / Engineering | Merchant Success |
| Settlement / reconciliation | Finance Operations | Finance / Engineering | Merchant |
| Security / privacy | Security process | Security / Privacy / Legal as applicable | Authorized leadership |

Actual on-call ownership, escalation contacts, and authority must be inserted from approved DOKU internal directories.

## 13. Communication protocol

### 13.1 Internal incident communication

Share:
- Incident reference.
- Current severity.
- Affected service and market.
- Known impact.
- Current containment.
- Investigation owner.
- Outstanding risks.
- Next update time.

### 13.2 Merchant communication

A merchant update should include:

1. What happened.
2. Which service or process is affected.
3. Known impact and affected period.
4. Whether customer or billing data may be affected.
5. Current action.
6. Any required merchant action.
7. Next update time.
8. Closure and reconciliation status when available.

Do not speculate about root cause or provide unverified restoration commitments.

### 13.3 Customer communication

Customer-facing messages should be coordinated with the merchant and relevant DOKU teams.

Messages must reflect confirmed payment status. Never tell a customer that a payment failed when the status is still unknown, or that payment succeeded without evidence.

## 14. Incident timeline and evidence

Maintain a chronological record.

| Timestamp | Event | Owner | Evidence / reference |
|---|---|---|---|
| | First detection | | |
| | Incident declared | | |
| | Severity assigned | | |
| | Containment started | | |
| | Root cause identified | | |
| | Resolution implemented | | |
| | Service validated | | |
| | Merchant informed | | |
| | Incident closed | | |

Record timezone consistently and retain evidence in approved systems.

## 15. Recovery validation and closure

Before closure, confirm:

- [ ] Affected service is operating normally.
- [ ] Billing generation is correct.
- [ ] Payment statuses are resolved where possible.
- [ ] No unsafe retry or duplicate collection remains.
- [ ] Webhook and API processing is healthy.
- [ ] Subscription states are correct.
- [ ] Customer impact is understood.
- [ ] Settlement and reconciliation exceptions are addressed or assigned.
- [ ] Merchant communication is completed.
- [ ] Follow-up actions have accountable owners.

An incident may be technically resolved while financial reconciliation remains open. In that case, close the service-restoration phase but retain a separately tracked financial action.

## 16. Post-incident review

Material incidents should have a structured review.

### 16.1 Review questions

1. What happened?
2. When did it start and when was it detected?
3. What was the customer and merchant impact?
4. What billing and payment populations were affected?
5. What was the financial exposure?
6. What caused the incident?
7. Which controls worked?
8. Which controls failed or were missing?
9. How effective was communication?
10. What prevents recurrence?

### 16.2 Root-cause classification

Use categories such as:
- Software defect.
- Configuration error.
- Integration issue.
- Dependency or partner issue.
- Capacity or performance.
- Operational process failure.
- Data integrity.
- Human error.
- Security or privacy.
- Unknown / under investigation.

Avoid blame-oriented reporting. Focus on system and process improvements.

### 16.3 Corrective and preventive action register

| Action | Type | Owner | Priority | Due date | Evidence of completion |
|---|---|---|---|---|---|
| | Corrective | | | | |
| | Preventive | | | | |

## 17. Incident KPIs

| KPI | Definition |
|---|---|
| Incident count | Number of recorded incidents by period and severity |
| Time to detect | Detection time minus incident start time |
| Time to acknowledge | First accountable response minus report time |
| Time to contain | Containment time minus incident declaration time |
| Time to restore | Service restoration time minus incident start time |
| Repeat incident rate | Recurring incidents with the same root cause / eligible incidents |
| Merchant impact | Number of affected merchants |
| Customer impact | Number of affected customers or subscribers |
| Billing impact | Count and value of affected unique billings |
| Payment impact | Count and value of affected transactions |
| Reconciliation backlog | Number and value of unresolved financial exceptions |
| Action closure rate | Completed corrective actions / due corrective actions |

Define measurement start and end points consistently. Do not describe internal operational targets as contractual SLAs unless formally approved.

## 18. Market and integration considerations

### Indonesia and Malaysia

Maintain separate market incident records where local payment methods, banking partners, settlement arrangements, or merchant configurations differ.

Do not assume an incident in one market has the same scope or resolution in the other.

### Integration models

For each incident, establish the actual integration ownership:

- **DOKU-hosted Billing Automation:** Validate DOKU-side billing and collection processing.
- **API / H2H:** Include merchant-owned scheduling, request generation, and event processing where relevant.
- **Hybrid:** Identify the exact responsibility split and avoid competing recovery actions.
- **Merchant Hosted Scheduler:** Validate the merchant's scheduling and payment execution responsibility. Current product context identifies an Indonesian Business Account configuration; MY applicability requires confirmation.

## 19. Incident readiness checklist

- [ ] Incident severity framework approved.
- [ ] Service owners identified.
- [ ] On-call and escalation contacts available.
- [ ] Monitoring and alert thresholds configured.
- [ ] Merchant impact data accessible.
- [ ] Billing and transaction identifiers traceable.
- [ ] Safe containment actions documented.
- [ ] Pending transaction resolution process defined.
- [ ] Duplicate prevention controls understood.
- [ ] Security and privacy escalation path known.
- [ ] Merchant communication templates approved.
- [ ] Reconciliation and closure process defined.
- [ ] Post-incident review owner assigned.

## 20. Final principles

1. Protect customers before optimizing service restoration.
2. Establish incident scope using billing, transaction, subscriber, and merchant evidence.
3. Separate pending status from definitive payment failure.
4. Stop duplicate and unsafe collection before resuming normal processing.
5. Escalate security, privacy, and financial-integrity concerns through specialist channels.
6. Communicate verified facts and explicit uncertainties.
7. Validate both technical recovery and business outcomes.
8. Keep financial reconciliation open until properly resolved.
9. Assign corrective actions with owners and deadlines.
10. Use every material incident to improve product reliability and operational readiness.

**The objective is not simply to restore a service. It is to restore a trustworthy billing and payment outcome for merchants and customers.**
