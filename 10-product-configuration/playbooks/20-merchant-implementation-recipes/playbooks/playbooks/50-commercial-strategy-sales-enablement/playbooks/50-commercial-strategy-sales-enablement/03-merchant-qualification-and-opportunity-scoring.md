# Merchant Qualification and Opportunity Scoring

**Playbook:** Commercial Strategy & Sales Enablement  
**Document:** 03 — Merchant Qualification and Opportunity Scoring  
**Audience:** DOKU Sales, Business Development, Presales, Product, Partnership, and Merchant Success  
**Status:** Internal working playbook — proposed qualification framework

---

## 1. Purpose

This playbook establishes a consistent method to qualify FlexiBill opportunities.

It helps DOKU teams determine:

- Whether a merchant has a real billing and collection problem.
- Whether FlexiBill is a suitable solution.
- Whether the opportunity has sufficient commercial value.
- Whether the merchant is technically and operationally ready.
- Whether the solution can be delivered with currently validated capabilities.
- Whether the opportunity should proceed, be redesigned, or be disqualified.

The goal is to improve opportunity quality, reduce wasted presales effort, and increase conversion from prospecting to production.

**Core principle:**

> A large merchant is not automatically a good FlexiBill opportunity. A qualified opportunity has a real billing problem, measurable value, feasible solution, and a credible path to implementation.

---

## 2. Qualification framework

Evaluate every opportunity across six dimensions.

| Dimension | What we assess | Key question |
|---|---|---|
| Business fit | Billing model and business need | Does the merchant have recurring or scheduled billing requirements? |
| Commercial potential | Volume, value, and revenue opportunity | Is there meaningful payment and billing potential? |
| Collection pain | Failed payments and operational inefficiency | Is there a problem worth solving? |
| Product fit | Alignment with validated capabilities | Can FlexiBill support the required workflow? |
| Technical readiness | Integration and system readiness | Can the merchant implement the solution? |
| Strategic value | Vertical, ecosystem, and expansion potential | Does the opportunity create broader strategic value? |

Each dimension is scored from 1 to 5.

---

## 3. Qualification scoring model

### Score definitions

| Score | Classification | Interpretation |
|---:|---|---|
| 1 | Very weak | Little or no fit; substantial unresolved obstacles |
| 2 | Weak | Limited fit; major conditions or gaps |
| 3 | Moderate | Potential fit; several items require validation |
| 4 | Strong | Good fit; manageable dependencies |
| 5 | Very strong | Clear fit with validated requirements and strong evidence |

### Weighted scoring

Not all dimensions have equal importance.

| Dimension | Weight |
|---|---:|
| Business fit | 20% |
| Commercial potential | 20% |
| Collection pain | 15% |
| Product fit | 20% |
| Technical readiness | 15% |
| Strategic value | 10% |
| **Total** | **100%** |

### Calculation

\[
\text{Weighted Score} =
\sum_{i=1}^{6}
\left(\frac{\text{Score}_i}{5}\times \text{Weight}_i\right)
\]

The result is a score out of 100.

### Opportunity classification

| Weighted score | Classification | Recommended action |
|---:|---|---|
| 80–100 | Priority A | Progress to detailed solution design |
| 65–79 | Priority B | Progress with defined validation actions |
| 50–64 | Priority C | Discovery or feasibility assessment |
| Below 50 | Low priority | Defer, redesign, or disqualify |

**Important:** The score is a proposed internal prioritization model, not an approved DOKU commercial policy. It must not override mandatory product, risk, regulatory, technical, or country-level checks.

---

## 4. Dimension 1 — Business fit

Assess whether the merchant has a billing model that aligns with FlexiBill.

### Evaluation criteria

| Score | Evidence |
|---:|---|
| 1 | Primarily one-off transactions with no meaningful scheduled billing |
| 2 | Limited repeat billing; mostly manual or ad hoc |
| 3 | Some recurring or scheduled billing use cases |
| 4 | Established recurring or periodic billing model |
| 5 | Core business depends on recurring or scheduled customer obligations |

### Discovery questions

1. What products or services does the merchant bill?
2. Is billing one-off, recurring, installment-based, or usage-based?
3. How frequently are customers billed?
4. Are billing amounts fixed or variable?
5. Are there multiple customer plans or pricing structures?
6. What events start, change, or stop billing?
7. How many active billing relationships exist?

### Evidence to collect

- Billing process documentation.
- Sample invoices or billing records, with sensitive data removed.
- Billing frequency.
- Number of unique customers or subscribers.
- Current billing system.
- Existing subscription or contract model.

---

## 5. Dimension 2 — Commercial potential

Assess the opportunity's scale and economic relevance.

### Core inputs

| Metric | Definition |
|---|---|
| Active billing customers | Unique customers with active billing obligations under the agreed definition |
| Monthly billing count | Number of unique billing obligations raised per month |
| Average billing amount | Average value per unique billing obligation |
| Monthly billing value | Total value of billing obligations raised in the month |
| Payment volume potential | Expected value processed through relevant DOKU payment flows |
| Expected transaction count | Expected successful and attempted payment transactions, defined consistently |
| Expected merchant growth | Expected increase in customers, billing count, or value |

### Calculation examples

Monthly billing value:

\[
\text{Monthly Billing Value}
=
\text{Monthly Billing Count}
\times
\text{Average Billing Amount}
\]

Illustrative example:

- 8,000 unique monthly billing obligations.
- Average billing amount: Rp400,000.

\[
8,000 \times Rp400,000 = Rp3.2\text{ billion}
\]

This is an illustrative billing value, not a guaranteed DOKU TPV or revenue figure.

### Commercial qualification questions

- What is the current monthly billing value?
- How much of that value is expected to flow through DOKU?
- Which payment methods are relevant?
- What is the expected adoption or migration rate?
- Is the opportunity new business, migration, or expansion?
- Are there other business lines that could use the solution?

### Commercial discipline

Separate these measures:

1. Total merchant billing value.
2. Billing value eligible for the proposed solution.
3. Value expected to be processed through DOKU.
4. Successfully collected payment value.
5. DOKU revenue under the approved commercial arrangement.

Never present total merchant billing value as guaranteed DOKU TPV or revenue.

For Indonesia and Malaysia, calculate and report currency separately unless an explicit FX methodology is approved.

---

## 6. Dimension 3 — Collection pain

A good opportunity should solve a meaningful operational or payment problem.

### Evaluation criteria

| Score | Evidence |
|---:|---|
| 1 | No identified collection problem |
| 2 | Minor manual work or limited payment failure |
| 3 | Visible collection inefficiency or failed payment issues |
| 4 | Material failed collection, manual follow-up, or reconciliation burden |
| 5 | Significant and measurable revenue leakage or operational inefficiency |

### Discovery questions

- What percentage of billing obligations are successfully collected?
- Is success measured by transaction attempts or unique billing obligations?
- How many payment attempts are made per billing obligation?
- What happens after a failed transaction?
- Is there a structured retry or recovery process?
- How much billing value remains uncollected?
- How long does recovery take?
- How many staff members manage the process?

### Evidence to collect

- Billing-level payment outcomes.
- Attempt-level transaction data.
- Failed billing value.
- Recovery records.
- Overdue and aging reports.
- Operational workload estimates.
- Reconciliation exception reports.

### Avoid misleading metrics

A payment-attempt success rate is not the same as a billing-level collection success rate.

For example, a single billing obligation may generate several payment attempts. Count the unique billing obligation once when calculating billing-level collection performance.

---

## 7. Dimension 4 — Product fit

Product fit is a mandatory qualification dimension.

A high commercial score cannot compensate for an unsupported product requirement.

### Product-fit checklist

| Requirement | Validation |
|---|---|
| Billing structure | Can the billing obligation be represented with available configuration? |
| Pricing model | Is the required pricing method supported? |
| Billing schedule | Is the required frequency and schedule supported? |
| Customer management | Is the required membership/customer workflow available? |
| Customer payment journey | Can the required customer flow be delivered? |
| Payment method | Is the required method supported for the proposed flow? |
| Auto-debit | Is recurring authorization and collection supported for the method and country? |
| Lifecycle | Are required cancellation, pause, resume, or plan-change actions available? |
| Failure handling | Can the expected recovery process be supported? |
| Reporting | Can the merchant obtain the required billing and payment visibility? |
| Country | Is the capability available in the target market? |

### Product-fit classification

| Classification | Meaning | Sales treatment |
|---|---|---|
| Available | Confirmed capability in the relevant scope | May be proposed accurately |
| Conditional | Requires configuration, integration, or other dependencies | Disclose conditions |
| Validation required | Availability or behavior is not confirmed | Obtain internal confirmation |
| Gap | Required capability is not currently available | Do not promise delivery |
| Future / Strategic | Roadmap or concept | Do not position as released |

### Mandatory escalation triggers

Escalate to Product or Solution Engineering when the merchant requires:

- Native real-time metering or usage aggregation.
- Complex plan changes or proration.
- Multi-product and add-on orchestration.
- Customer or account hierarchy.
- Consolidated invoicing.
- Wallet or entitlement management.
- Global tax or multi-currency billing logic.
- Revenue recognition.
- Cross-merchant bill payment or one-VA functionality.
- Unsupported payment methods or country coverage.

### Known product-specific cautions

- PayChat's confirmed FlexiBill connection for bulk-upload billing does not establish full Pricing Table or WhatsApp seller frontend functionality.
- Pricing Table WhatsApp seller UI/UX is not confirmed.
- Digital Catalog integration with Subscription / Pricing Table is not confirmed.
- Member Center API readiness does not establish customer-facing frontend readiness.
- Merchant Hosted Scheduler is documented for Indonesian Business Account; Malaysia availability requires validation.
- Cross-merchant Bill Connector and one-VA concepts are strategic, not generally available.

---

## 8. Dimension 5 — Technical readiness

Assess whether the merchant can implement the proposed solution.

### Evaluation criteria

| Score | Evidence |
|---:|---|
| 1 | No technical owner, unclear requirements, or no viable integration path |
| 2 | Major system or resource constraints |
| 3 | Integration path exists but several dependencies remain |
| 4 | Technical owner and integration path identified |
| 5 | Requirements, ownership, architecture, and delivery resources are confirmed |

### Technical discovery questions

- Does the merchant have an internal engineering team?
- Which system owns customer records?
- Which system calculates billing amounts?
- Which system owns subscription status?
- Does the merchant require API, hosted, batch, or hybrid integration?
- Can the merchant receive and process payment events?
- How will payment status be reconciled?
- Is there a test environment?
- Who will own production support?

### Technical readiness evidence

- System architecture diagram.
- API and webhook requirements.
- Data mapping.
- Authentication and security requirements.
- Integration owner.
- Test and certification plan.
- Deployment timeline.
- Production support model.

### Technical disqualification signals

- No system owner and no willingness to appoint one.
- Required integration is unsupported.
- Merchant cannot meet essential security requirements.
- No agreed system of record for billing or payment status.
- No operational owner for production exceptions.

---

## 9. Dimension 6 — Strategic value

Assess whether the opportunity creates value beyond its immediate transaction potential.

### Evaluation criteria

| Score | Evidence |
|---:|---|
| 1 | Limited strategic relevance and no meaningful expansion |
| 2 | Small standalone opportunity |
| 3 | Relevant vertical use case with some repeatability |
| 4 | Strong reference merchant or ecosystem opportunity |
| 5 | Significant distribution, partnership, or multi-market opportunity |

### Strategic indicators

- Strong reference merchant potential.
- Repeatable vertical use case.
- Access to a broader merchant network.
- Partnership distribution opportunity.
- Potential for multiple merchant integrations.
- Expansion across business units or countries.
- Strong alignment with DOKU's payment strategy.

Strategic value must not be used to bypass product readiness or risk approval.

---

## 10. Opportunity scoring worksheet

Use the following template during qualification.

| Dimension | Weight | Score (1–5) | Weighted result | Evidence / notes |
|---|---:|---:|---:|---|
| Business fit | 20% |  |  |  |
| Commercial potential | 20% |  |  |  |
| Collection pain | 15% |  |  |  |
| Product fit | 20% |  |  |  |
| Technical readiness | 15% |  |  |  |
| Strategic value | 10% |  |  |  |
| **Total** | **100%** |  | **/100** |  |

Formula:

\[
\text{Weighted Result}
=
\frac{\text{Score}}{5}
\times
\text{Weight}
\]

Sum the weighted results to obtain the overall score.

### Example

| Dimension | Weight | Score | Weighted result |
|---|---:|---:|---:|
| Business fit | 20% | 5 | 20 |
| Commercial potential | 20% | 4 | 16 |
| Collection pain | 15% | 5 | 15 |
| Product fit | 20% | 4 | 16 |
| Technical readiness | 15% | 3 | 9 |
| Strategic value | 10% | 4 | 8 |
| **Total** | **100%** |  | **84/100** |

**Illustrative classification:** Priority A.

The score indicates strong qualification, but the opportunity must still pass all mandatory feasibility and approval checks.

---

## 11. Mandatory qualification gates

Apply these gates regardless of the weighted score.

### Gate 1 — Business need

There must be a defined billing or collection problem.

If no meaningful problem exists, reconsider the opportunity.

### Gate 2 — Product feasibility

The proposed solution must align with confirmed or conditionally validated product capabilities.

An unsupported mandatory requirement prevents a production commitment.

### Gate 3 — Country and payment eligibility

Validate the merchant country, payment methods, recurring eligibility, authorization requirements, and applicable operating model.

### Gate 4 — Risk and compliance

Required risk, legal, compliance, and data protection checks must be completed.

### Gate 5 — Technical ownership

The merchant and DOKU must identify accountable technical and operational owners.

### Gate 6 — Commercial viability

The expected business value must justify implementation, support, and ongoing operating costs.

---

## 12. Qualification decision matrix

| Score | Mandatory gates | Decision |
|---|---|---|
| Priority A | All passed | Progress to solution design |
| Priority A | One or more unresolved | Hold commitment; close validation actions |
| Priority B | All passed | Progress with defined conditions |
| Priority B | Major gap | Conduct feasibility assessment |
| Priority C | All passed | Continue discovery or limited pilot assessment |
| Priority C | Major gap | Defer or redesign |
| Low priority | Any | Usually deprioritize unless there is a documented strategic reason |

A high score never overrides a failed mandatory gate.

---

## 13. Opportunity funnel and stage exit criteria

| Stage | Required output | Exit criteria |
|---|---|---|
| 1. Prospect identified | Prospect record | Merchant and contact identified |
| 2. Initial qualification | Qualification notes | Billing need and basic fit established |
| 3. Discovery completed | Discovery record | Billing, payment, technology, and commercial requirements documented |
| 4. Opportunity scored | Scoring worksheet | Weighted score and mandatory gates assessed |
| 5. Solution feasibility | Product and technical validation | Feasible solution pattern identified |
| 6. Solution design | Solution blueprint | Merchant workflow, architecture, and dependencies documented |
| 7. Commercial proposal | Commercial proposal | Scope, assumptions, pricing, and expected value approved |
| 8. Pilot / implementation | Delivery plan | Owners, milestones, and success criteria agreed |
| 9. Production activation | Go-live approval | Operational readiness and acceptance confirmed |
| 10. Growth and expansion | Adoption review | Performance and expansion opportunities assessed |

---

## 14. Red flags and disqualification criteria

| Red flag | Why it matters | Recommended action |
|---|---|---|
| Merchant only needs one-off payment processing | Weak billing fit | Refer to relevant DOKU payment proposition |
| Required feature is a confirmed product gap | Delivery risk | Redesign or document roadmap dependency |
| Merchant assumes all payment methods support auto-debit | Authorization and product risk | Validate each method |
| Billing and payment records cannot be matched | Reconciliation risk | Define data mapping and identifiers |
| Merchant has no technical owner | Implementation risk | Appoint accountable owner before progression |
| Merchant cannot define billing obligations | Solution ambiguity | Return to discovery |
| Expected TPV is unsupported by evidence | Commercial forecast risk | Rebuild forecast with assumptions |
| Merchant expects guaranteed recovery improvement | Performance risk | Establish pilot baseline and measurable targets |
| Country availability is assumed | Delivery risk | Obtain country-level validation |
| Regulatory or risk review is incomplete | Approval risk | Hold commitment pending review |

---

## 15. Required qualification record

Every opportunity should have a documented record containing:

### Merchant information
- Merchant name.
- Country and legal entity.
- Industry and business model.
- Business owner and decision maker.
- Sales and account owner.

### Billing information
- Billing model.
- Billing frequency.
- Customer or subscriber count.
- Monthly billing count.
- Average billing amount.
- Monthly billing value.
- Pricing model.
- Billing lifecycle requirements.

### Collection information
- Current payment methods.
- Recurring payment requirements.
- Current success rate and denominator.
- Failed billing value.
- Recovery rate and observation window.
- Current collection operations.

### Technical information
- System of record.
- Integration approach.
- API / webhook / batch requirements.
- Customer-facing experience.
- Technical owner.
- Testing and deployment dependencies.

### Commercial information
- Expected DOKU payment volume.
- Expected transaction count.
- Revenue assumptions.
- Commercial model.
- Implementation effort.
- Strategic value.

### Validation and decision
- Product-fit classification.
- Country validation.
- Risk and compliance status.
- Weighted score.
- Mandatory gate outcomes.
- Open issues.
- Decision and next action.

---

## 16. Sales-to-Presales handover

A qualified opportunity should not be handed to Presales with only a merchant name and a broad request.

The handover must include:

1. Merchant business context.
2. Confirmed billing problem.
3. Current-state workflow.
4. Target-state workflow.
5. Billing and payment volumes.
6. Required customer experience.
7. Integration requirements.
8. Required product capabilities.
9. Known product gaps and assumptions.
10. Commercial opportunity.
11. Stakeholders and decision makers.
12. Expected timeline.
13. Open questions and owners.

Presales should return the opportunity for further discovery if essential information is missing.

---

## 17. Governance and ownership

| Activity | Sales / BD | Presales | Product | Engineering | Risk / Compliance |
|---|---|---|---|---|---|
| Prospect identification | Accountable | Consulted | Informed | Informed | — |
| Initial qualification | Accountable | Consulted | Consulted | — | — |
| Commercial assessment | Accountable | Consulted | Consulted | — | — |
| Product feasibility | Consulted | Responsible | Accountable | Consulted | — |
| Technical solution | Consulted | Responsible | Consulted | Accountable for technical delivery | Consulted |
| Country and payment validation | Responsible for coordination | Consulted | Consulted | Consulted | Consulted |
| Risk and compliance approval | Informed | Consulted | Consulted | Consulted | Accountable |
| Commercial proposal | Accountable | Responsible for solution input | Consulted | Consulted | Consulted |
| Production readiness | Informed | Responsible for solution acceptance | Consulted | Responsible for technical readiness | Required approval where applicable |

This is a proposed working model. Confirm actual DOKU role ownership and approval authority.

---

## 18. Success measures

| KPI | Purpose |
|---|---|
| Qualified opportunity rate | Measures prospecting quality |
| Opportunity-to-discovery conversion | Measures initial engagement effectiveness |
| Discovery-to-solution-design conversion | Measures quality of requirements and product fit |
| Product-fit rejection rate | Identifies gaps in qualification or product readiness |
| Technical feasibility pass rate | Measures implementation suitability |
| Proposal-to-win conversion | Measures commercial effectiveness |
| Time in qualification stage | Identifies pipeline delays |
| Pilot-to-production conversion | Measures delivery and solution success |
| Activated merchant billing value | Measures realized business adoption |
| Forecast accuracy | Measures reliability of commercial assumptions |

---

## 19. Final qualification checklist

Before marking an opportunity as qualified:

- [ ] A real billing or collection problem is documented.
- [ ] The merchant's billing model is understood.
- [ ] Commercial potential is quantified with explicit assumptions.
- [ ] Collection pain is supported by evidence.
- [ ] Product fit is validated.
- [ ] Country and payment-method eligibility are checked.
- [ ] Technical readiness is assessed.
- [ ] Risk and compliance requirements are identified.
- [ ] Technical and operational owners are known.
- [ ] Mandatory qualification gates are passed or have named actions.
- [ ] Weighted score and opportunity classification are recorded.
- [ ] Sales-to-Presales handover information is complete.

---

## 20. Final principle

**Qualify the problem before qualifying the merchant.**

A strong FlexiBill opportunity is one where:

**Real billing need + measurable collection pain + validated product fit + technical readiness + commercial viability = qualified opportunity.**

---

**End of Playbook 03**
