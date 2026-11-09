# Discovery and Use-Case Assessment

**Playbook:** Commercial Strategy & Sales Enablement  
**Document:** 04 — Discovery and Use-Case Assessment  
**Audience:** DOKU Sales, Business Development, Presales, Product, Partnership, and Merchant Success  
**Status:** Internal working playbook — capability and country validation required

---

## 1. Purpose

This playbook standardizes how DOKU teams discover, document, and assess merchant billing and payment requirements.

The objective is to move beyond a general product presentation and understand the merchant's actual business process.

A successful discovery should establish:

1. How the merchant sells and delivers its products or services.
2. How billing obligations are created and calculated.
3. How customers are notified and make payments.
4. How recurring collections and payment failures are handled.
5. How billing and payment outcomes are monitored and reconciled.
6. What the merchant wants to improve.
7. Whether FlexiBill can support the target workflow.
8. What product, technical, operational, commercial, and country validations remain.

**Core principle:**

> Discover the merchant's business process before designing the FlexiBill solution.

---

## 2. Discovery methodology

Use a six-step discovery process.

| Step | Activity | Expected output |
|---|---|---|
| 1 | Understand the business model | Merchant business profile |
| 2 | Map the current billing process | Current-state process map |
| 3 | Diagnose collection and operational pain | Problem and impact assessment |
| 4 | Define the desired customer and merchant journey | Target-state workflow |
| 5 | Assess product and technical feasibility | Capability and integration assessment |
| 6 | Quantify the opportunity and agree next steps | Business case and discovery report |

Do not move directly from Step 1 to a product demo. A demo should reflect the merchant's actual requirements.

---

## 3. Step 1 — Understand the merchant's business model

### A. Business profile

Collect the following information:

| Information | Discovery question |
|---|---|
| Industry | What industry and business segment does the merchant operate in? |
| Business model | What products or services does the merchant sell? |
| Customer type | B2C, B2B, B2B2C, membership, or platform? |
| Customer base | How many active customers, members, or accounts exist? |
| Geography | Which countries and markets are served? |
| Distribution | Direct sales, branches, agents, partners, online, or hybrid? |
| Technology | What core systems support the business? |
| Growth | What customer or transaction growth is expected? |

### B. Billing model classification

Identify the merchant's primary and secondary billing models.

| Billing model | Description | Example |
|---|---|---|
| One-off | A single payment obligation | Product purchase |
| Fixed recurring | Same amount at regular intervals | Monthly membership |
| Variable recurring | Amount changes between billing periods | Variable service fees |
| Installment | Total obligation split into scheduled payments | Education fees |
| Contractual recurring | Repeated charges under an agreement | B2B retainer |
| Usage-based | Charge depends on measured consumption | API usage |
| Tiered / volume-based | Charge depends on pricing thresholds | SaaS plans |
| Event-triggered | Billing follows a defined business event | Service completion |

A merchant may combine several billing models.

### C. Billing maturity

| Maturity | Characteristics |
|---|---|
| Level 1 — Manual | Spreadsheet, manual invoice, manual follow-up |
| Level 2 — Semi-automated | Billing system exists but collection and reconciliation remain fragmented |
| Level 3 — Integrated | Billing and payment systems exchange data |
| Level 4 — Orchestrated | Billing, payment, recovery, and monitoring are connected |
| Level 5 — Optimized | Data-driven billing and collection operations with continuous improvement |

This is a proposed discovery framework, not an official industry maturity certification.

---

## 4. Step 2 — Map the current-state billing process

Understand what happens from the moment a customer becomes liable to pay until the merchant closes the billing obligation.

### Current-state process

```text
Customer / Contract / Order
          |
          v
Billing obligation created
          |
          v
Amount and due date calculated
          |
          v
Invoice / payment request generated
          |
          v
Customer notified
          |
          v
Customer initiates or authorizes payment
          |
          v
Payment processed
          |
          v
Payment result received
          |
          v
Billing status updated
          |
          v
Reconciliation and reporting
          |
          v
Outstanding billing follow-up
```

The diagram is a discovery template. Actual merchant flows may differ.

### Process discovery questions

**Customer onboarding**
- How does a new customer register?
- Is customer verification required?
- Is payment authorization collected during registration?
- Which system creates the customer record?

**Billing creation**
- What triggers a billing obligation?
- Who calculates the amount?
- How are billing dates determined?
- Are amounts fixed or variable?
- Can billing be generated in bulk?

**Payment request**
- How does the customer receive the payment request?
- Is the payment link generated automatically?
- Does the customer need to log in?
- Which channels are used for notifications?

**Payment execution**
- Does the customer initiate payment or is payment collected automatically?
- Which payment methods are available?
- Is recurring authorization required?
- What happens when the payment method is no longer valid?

**Payment outcome**
- How does the merchant receive payment status?
- How are pending transactions handled?
- How are duplicate notifications prevented?
- How does the merchant update its billing record?

**Reconciliation**
- How are billing records matched with payment transactions?
- Which reference identifiers are used?
- How are settlement and accounting handled?
- Who investigates unmatched records?

---

## 5. Step 3 — Diagnose collection and operational pain

Discovery must quantify the problem wherever data is available.

### A. Billing and collection baseline

Request the most recent representative reporting period. Ideally, obtain enough history to understand seasonality and renewal patterns.

| Metric | Required information |
|---|---|
| Unique billing obligations | Count of billing records raised |
| Monthly billing value | Total value of billing obligations |
| Average billing amount | Average value per unique billing record |
| Initial collection success | Success at the first defined payment attempt |
| Final collection success | Success by an agreed observation cutoff |
| Failed billing count | Unique billing obligations still unsuccessful |
| Failed billing value | Value of eligible unsuccessful obligations |
| Recovered billing value | Value recovered after initial failure |
| Recovery time | Time from initial failure to successful collection |
| Overdue population | Unique billing obligations past due |
| Manual follow-up | Number of cases requiring human intervention |

### B. Operational pain assessment

| Problem area | Discovery question | Potential impact |
|---|---|---|
| Billing preparation | How much time is spent preparing billing records? | Operational cost |
| Payment follow-up | How many customers require manual reminders? | Staff workload |
| Failed collection | What happens after a failed payment? | Revenue leakage |
| Payment status | How quickly is status reflected in the merchant system? | Customer service burden |
| Reconciliation | How many records remain unmatched? | Finance workload |
| Customer administration | How are changes and cancellations managed? | Administrative complexity |
| Reporting | How long does it take to produce collection reports? | Decision latency |

### C. Revenue leakage assessment

Use a consistent billing-level definition.

\[
\text{Initial Failure Rate}
=
\frac{\text{Unique Initially Failed Billing Obligations}}
{\text{Eligible Unique Billing Obligations}}
\]

\[
\text{Recovery Rate}
=
\frac{\text{Initially Failed Value Subsequently Recovered}}
{\text{Eligible Initially Failed Value}}
\]

\[
\text{Net Unrecovered Value}
=
\text{Eligible Initially Failed Value}
-
\text{Recovered Value}
\]

These formulas require:
- An explicit reporting period.
- A defined unique billing identifier.
- A consistent initial-failure definition.
- A defined recovery observation window.
- Separate treatment of pending and unknown outcomes.
- Consistent gross or net value basis.

Do not equate all initially failed value with permanently lost revenue.

---

## 6. Step 4 — Define the desired customer journey

The customer journey should be discovered separately from the merchant's back-office process.

### Customer journey stages

| Stage | Customer experience | Discovery question |
|---|---|---|
| Discover | Finds a product or service | Where does the customer start? |
| Register | Provides required information | What information and consent are needed? |
| Select | Chooses a plan or service | Are there different plans or prices? |
| Authorize | Provides payment authorization where applicable | How is consent collected and recorded? |
| Pay | Completes the initial payment | Which payment methods are available? |
| Receive | Gets confirmation and relevant billing information | Which communication channels are used? |
| Continue | Receives subsequent billing requests or collection | How does the next billing cycle work? |
| Manage | Requests changes or updates payment details | Which lifecycle actions are required? |
| Recover | Resolves a failed or overdue payment | What recovery experience is expected? |
| Exit | Cancels or completes the service | What happens to future billing obligations? |

### Questions about the customer interface

- Does the customer use a merchant website or application?
- Is a hosted payment or billing page acceptable?
- Does the merchant need an embedded experience?
- Is a mobile-friendly journey required?
- Does the customer need to view invoices and receipts?
- Can the customer update a payment method?
- Does the customer need to manage a subscription
