# Solution Design and Commercial Proposal

**Playbook:** Commercial Strategy & Sales Enablement  
**Document:** 05 — Solution Design and Commercial Proposal  
**Audience:** DOKU Sales, Presales, Product, Engineering, Partnership, Merchant Success, and Management  
**Status:** Internal working playbook — proposed methodology; capability, country, risk, and commercial validation required

---

## 1. Purpose

This playbook standardizes how DOKU teams translate merchant discovery into a feasible FlexiBill solution design and commercial proposal.

The objective is to ensure that every proposal connects:

1. A clearly defined merchant business problem.
2. A documented current-state process.
3. A practical target-state solution.
4. Validated FlexiBill capabilities.
5. A defined technical and operating model.
6. A measurable business case.
7. An agreed implementation scope.
8. Transparent commercial assumptions and dependencies.

**Core principle:**

> A commercial proposal must sell a solution that can actually be delivered — not just a product concept that sounds attractive.

---

## 2. Solution design methodology

Use this eight-step process.

| Step | Activity | Required output |
|---|---|---|
| 1 | Consolidate discovery findings | Requirements baseline |
| 2 | Define target business outcome | Solution objectives |
| 3 | Select FlexiBill solution pattern | Solution approach |
| 4 | Map merchant and customer journeys | Target-state process |
| 5 | Define architecture and integration | Solution architecture |
| 6 | Assess capability gaps and dependencies | Feasibility assessment |
| 7 | Quantify expected business value | Business case |
| 8 | Prepare and approve proposal | Commercial proposal |

Do not finalize commercial commitments before completing the mandatory feasibility and approval checks.

---

## 3. Step 1 — Consolidate merchant requirements

Group requirements into six categories.

| Category | Examples |
|---|---|
| Business | Billing frequency, customer model, contract structure |
| Billing | Amount calculation, pricing, billing schedule, due date |
| Payment | Payment methods, recurring authorization, payment initiation |
| Customer experience | Registration, plan selection, payment, billing management |
| Operations | Failure handling, customer support, reconciliation |
| Technology | API, webhook, batch, system ownership, security |

### Requirements register

| ID | Requirement | Business priority | Mandatory? | Source | Owner |
|---|---|---|---|---|---|
| R-001 | Create recurring billing obligation | High | Yes | Discovery | Product |
| R-002 | Support selected payment method | High | Yes | Merchant | Payment / Product |
| R-003 | Return payment status to merchant | High | Yes | Technical discovery | Engineering |
| R-004 | Provide customer billing information | Medium | To confirm | Merchant | Product |
| R-005 | Support failed-payment recovery | High | To confirm | Operations | Product / Operations |

The table is illustrative. Replace it with actual merchant requirements.

### Requirement priority definitions

- **Must have:** Required for the agreed use case to operate.
- **Should have:** Important, but a viable initial implementation may exist without it.
- **Could have:** Desirable enhancement.
- **Future:** Strategic or roadmap-dependent requirement.

A mandatory requirement classified as a product gap must be resolved through redesign, approved roadmap commitment, or an explicit decision not to proceed.

---

## 4. Step 2 — Define the target business outcome

Start the solution design with measurable outcomes.

| Objective | Baseline | Target | Measurement |
|---|---:|---:|---|
| Reduce manual billing work | To establish | Agreed target | Staff hours per billing cycle |
| Improve collection success | To establish | Agreed target | Billing-level collection success |
| Improve recovery | To establish | Agreed target | Recovery rate |
| Reduce payment-status delay | To establish | Agreed target | Time from payment result to merchant update |
| Reduce reconciliation exceptions | To establish | Agreed target | Unmatched records |
| Improve customer experience | To establish | Agreed target | Defined customer experience measure |

Do not invent targets before understanding the baseline.

### Outcome definition

For each objective, record:
- Metric name.
- Baseline value.
- Target value.
- Measurement period.
- Data source.
- Calculation formula.
- Reporting owner.
- Exclusions and limitations.

---

## 5. Step 3 — Select the solution pattern

Choose the approach that best fits the merchant's operating model.

### Pattern A — DOKU-hosted Billing Automation

**Best suited to:** Merchants seeking a structured billing and collection workflow supported by DOKU-hosted capabilities.

Potential design elements:
- Merchant configuration of billing structures.
- Collection and plan setup.
- Pricing configuration.
- Customer and membership records.
- Billing generation.
- Supported payment collection.
- Customer payment entry points.
- Billing and payment monitoring.

**Key design questions:**
- Which billing logic is configured in FlexiBill?
- Which customer experience is used?
- How are billing obligations created?
- Which payment methods are supported?
- What operational processes remain with the merchant?

### Pattern B — API / Host-to-Host

**Best suited to:** Merchants that want their own applications and systems to drive the customer and billing experience.

Potential design elements:
- Merchant-owned customer interface.
- API-based billing and payment integration.
- Merchant-side business logic.
- Payment event processing.
- Billing status synchronization.
- Merchant-side reconciliation.

**Key design questions:**
- Which APIs are required?
- Which system creates the billing obligation?
- Which system owns the final billing status?
- How are payment events processed?
- How are duplicate events and timeouts handled?
- What is the merchant's retry and recovery responsibility?

### Pattern C — Hybrid

**Best suited to:** Merchants that want to retain selected internal processes while using DOKU-supported billing and payment capabilities.

Potential design elements:
- Merchant-owned customer or core business system.
- FlexiBill-supported billing or collection workflow.
- API or batch data exchange.
- DOKU-supported payment execution.
- Defined status and reconciliation exchange.

**Key design questions:**
- Which responsibilities belong to the merchant?
- Which responsibilities belong to DOKU?
- Where is billing logic executed?
- Where is customer data maintained?
- Who owns exception handling?

### Pattern D — Batch / File-based workflow

**Best suited to:** Merchants with periodic bulk billing or existing systems that exchange structured files.

Potential design elements:
- Merchant billing file generation.
- Agreed file format and validation.
- File submission and processing.
- Billing and payment status reporting.
- Exception handling and reconciliation.

Validate the exact file workflow, supported formats, frequency, and processing behavior before proposing.

### Pattern E — Merchant Hosted Scheduler

**Best suited to:** Eligible merchants operating their own billing schedule and integration logic.

The documented scope includes Indonesian Business Account. Malaysia availability must be validated independently.

Do not generalize this pattern to all merchants or markets.

---

## 6. Step 4 — Design the merchant journey

The merchant journey should define what the merchant does before, during, and after billing.

### Merchant operating journey

| Stage | Merchant activity | Design consideration |
|---|---|---|
| Configure | Establish collection and plan structures | Confirm supported configuration |
| Register | Create or maintain customer records | Define source of customer data |
| Prepare | Establish billing obligations | Define billing ownership |
| Initiate | Start payment or collection | Confirm payment flow |
| Monitor | Review billing and payment outcomes | Define status visibility |
| Recover | Handle failed or overdue obligations | Define supported recovery process |
| Reconcile | Match billing and payment records | Agree reference mapping |
| Report | Review business performance | Agree KPI definitions |

### Merchant role and system mapping

| Activity | Merchant | FlexiBill / DOKU | Other system |
|---|---|---|---|
| Customer acquisition | To define | To validate | To define |
| Customer registration | To define | To validate | To define |
| Billing calculation | To define | To validate | To define |
| Billing creation | To define | To validate | To define |
| Payment execution | To define | To validate | To define |
| Payment status | To define | To validate | To define |
| Retry and recovery | To define | To validate | To define |
| Reconciliation | To define | To validate | To define |
| Customer support | To define | To validate | To define |

Replace the placeholders with an agreed responsibility model for each merchant.

---

## 7. Step 5 — Design the customer journey

The customer experience should be simple, consistent, and appropriate for the merchant's business.

### Customer journey template

```text
Discover product / service
          |
          v
Register or identify customer
          |
          v
Select plan or billing option
          |
          v
Review billing terms
          |
          v
Authorize payment where applicable
          |
          v
Complete initial payment
          |
          v
Receive confirmation
          |
          v
Subsequent billing / payment cycle
          |
          v
Manage billing or payment issue
          |
          v
Renew, cancel, or complete service
```

### Customer experience design checklist

- Is the product or plan clearly described?
- Is the billing amount transparent?
- Is the billing frequency clear?
- Is the due date communicated?
- Is payment authorization explicit where required?
- Does the customer understand how recurring collection works?
- Is payment confirmation provided?
- Can the customer access relevant billing information?
- Is there a clear process for failed payment?
- Are cancellation and lifecycle terms communicated?

### FlexiBill interface selection

| Interface | Potential role | Required validation |
|---|---|---|
| Merchant Dashboard | Merchant administration | Available controls and roles |
| Pricing Table | Plan presentation and customer entry point | Pricing and payment-flow support |
| Member Center | Customer and membership-related interface | API and frontend readiness |
| Billing Portal | Customer billing access | Supported customer actions |
| Merchant application | Merchant-owned customer experience | API and integration scope |
| PayChat | Confirmed bulk-upload billing connection | Exact workflow and scope |

Do not represent a proposed customer experience as a released interface unless it has been validated.

---

## 8. Step 6 — Define the solution architecture

A solution architecture should show the major systems, data ownership, and communication paths.

### Example architecture — API / H2H pattern

```text
+---------------------------+
| Customer                  |
+-------------+-------------+
              |
              v
+---------------------------+
| Merchant Application      |
| Customer / Subscription   |
| Business Logic            |
+-------------+-------------+
              |
              | API request
              v
+---------------------------+
| FlexiBill / DOKU           |
| Billing / Collection      |
| Payment Orchestration     |
+-------------+-------------+
              |
              v
+---------------------------+
| DOKU Payment Infrastructure|
+-------------+-------------+
              |
              v
+---------------------------+
| Payment Method / Bank     |
+---------------------------+

Payment result / event
              |
              v
+---------------------------+
| Merchant Integration     |
| Status Update / Reconcile|
+---------------------------+
```

This is a conceptual architecture. Confirm actual service boundaries, endpoint availability, and event behavior in the relevant technical documentation.

### Architecture documentation requirements

Every solution blueprint should identify:

- Systems and applications.
- System of record for each data object.
- API and webhook interactions.
- Batch/file exchanges.
- Authentication and authorization.
- Customer and billing identifiers.
- Payment references.
- Status mapping.
- Retry and timeout handling.
- Reconciliation process.
- Security and data protection controls.
- Monitoring and support ownership.

### System-of-record matrix

| Data object | Proposed owner | Other systems using the data |
|---|---|---|
| Customer profile | To define | To define |
| Membership / subscription | To define | To define |
| Billing obligation | To define | To define |
| Billing amount | To define | To define |
| Payment authorization | To validate | To define |
| Payment transaction | To validate | To define |
| Final billing status | To define | To define |
| Settlement record | To validate | To define |

Avoid dual ownership of final billing status without a clear synchronization and conflict-resolution rule.

---

## 9. Step 7 — Assess capability feasibility

Map every mandatory requirement to a validated status.

| Requirement | Status | Evidence | Owner | Proposal treatment |
|---|---|---|---|---|
| Fixed recurring billing | Validation required | Product documentation / confirmation | Product | Confirm before commitment |
| Supported auto-debit | Validation required | Payment method and country scope | Product / Payment | Confirm eligibility |
| Pricing configuration | Validation required | Configuration scope | Product | Define supported model |
| Customer registration | Validation required | Member Center API and frontend | Product | Separate API from frontend |
| Payment status event | Validation required | Technical specification | Engineering | Confirm integration behavior |
| Recovery workflow | Conditional | Product and operational process | Product / Operations | Define responsibility |
| Customer billing portal | Validation required | Frontend capability | Product | Confirm actual functions |
| Merchant Hosted Scheduler | Conditional | Indonesian Business Account scope | Product | MY validation required |

Use the approved classifications:

- **Available**
- **Conditional**
- **Validation required**
- **Gap**
- **Future / Strategic**

### Known boundaries

Do not assume that FlexiBill currently provides:

- Native real-time metering and usage aggregation.
- Complete wallet and entitlement management.
- Full plan-change and proration lifecycle APIs.
- Multi-product and add-on orchestration.
- Customer hierarchy and consolidated invoicing.
- Global tax and currency management.
- Revenue recognition.
- Universal cross-merchant bill payment or one-VA functionality.

Other important cautions:
- PayChat bulk-upload billing does not establish full Pricing Table or WhatsApp seller frontend support.
- Pricing Table WhatsApp seller UI/UX is not confirmed.
- Digital Catalog integration with Subscription / Pricing Table is not confirmed.
- Member Center API readiness and customer-facing frontend readiness are separate.

A solution proposal must disclose material gaps and avoid roadmap commitments presented as existing functionality.

---

## 10. Step 8 — Build the business case

The business case should explain why the merchant should proceed.

### A. Baseline metrics

| Metric | Baseline | Source |
|---|---:|---|
| Unique billing obligations / month | To establish | Merchant |
| Monthly billing value | To establish | Merchant |
| Average billing amount | To establish | Merchant |
| Initial collection success | To establish | Merchant |
| Final collection success | To establish | Merchant |
| Failed billing value | To establish | Merchant |
| Recovered billing value | To establish | Merchant |
| Manual processing hours | To establish | Merchant |
| Reconciliation exceptions | To establish | Merchant |

### B. Potential value categories

1. Reduced manual billing effort.
2. Improved visibility into collection outcomes.
3. Better identification of failed and overdue billing.
4. More structured payment recovery operations.
5. Improved customer access to billing and payment information.
6. Scalable billing workflows.
7. Increased payment volume processed through DOKU, where adoption occurs.

### C. Illustrative scenario

Assume:

- 12,000 unique billing obligations per month.
- Average billing amount: Rp300,000.
- Initial collection success: 88%.

Monthly billing value:

\[
12,000 \times Rp300,000 = Rp3.6\text{ billion}
\]

Initially successful value:

\[
Rp3.6\text{ billion} \times 88\% = Rp3.168\text{ billion}
\]

Initially unsuccessful value:

\[
Rp3.6\text{ billion} \times 12\% = Rp432\text{ million}
\]

If an illustrative 25% of initially unsuccessful value is subsequently recovered:

\[
Rp432\text{ million} \times 25\% = Rp108\text{ million}
\]

This scenario demonstrates a calculation method only. It is not a product performance promise or a forecast of actual recovery.

### D. Business case discipline

Clearly separate:

- Total merchant billing value.
- Eligible billing value.
- Expected DOKU payment volume.
- Successfully collected value.
- Recovered value.
- Merchant operational savings.
- DOKU revenue.
- Implementation and operating cost.

Document assumptions, observation windows, currency, and data sources.

---

## 11. Step 9 — Define implementation scope

A commercial proposal must clearly state what is included and excluded.

### Scope matrix

| Workstream | Included scope | Excluded / separate scope |
|---|---|---|
| Product configuration | Agreed supported FlexiBill setup | Unsupported custom product development |
| Merchant integration | Agreed APIs, files, or hosted configuration | Unapproved third-party integrations |
| Customer experience | Agreed supported flow | Unvalidated frontend features |
| Payment methods | Agreed eligible methods | Unsupported payment methods |
| Testing | Agreed functional and integration tests | Unspecified merchant system testing |
| Reconciliation | Agreed references and reporting | Full accounting-system replacement |
| Training | Agreed operational handover | Unapproved custom training program |
| Support | Agreed operating model | Unapproved SLA or 24/7 commitment |

### Deliverable definition

For each deliverable, state:
- Description.
- Responsible party.
- Acceptance criteria.
- Dependencies.
- Target date.
- Required evidence.

---

## 12. Step 10 — Build the implementation roadmap

### Example delivery stages

| Stage | Activities | Exit criteria |
|---|---|---|
| 1. Alignment | Scope and business objectives | Scope agreed |
| 2. Solution design | Workflow and architecture | Design approved |
| 3. Configuration | Merchant and billing setup | Configuration validated |
| 4. Integration | API, webhook, or batch implementation | Integration tests pass |
| 5. Certification | Functional and payment-flow testing | Required tests accepted |
| 6. Pilot | Controlled production or agreed pilot environment | Pilot criteria met |
| 7. Go-live | Operational readiness and activation | Go-live approval |
| 8. Stabilization | Monitoring and issue resolution | Stability criteria met |
| 9. Growth | Adoption and performance review | Expansion actions agreed |

Actual dates and stage durations depend on the merchant, integration complexity, dependencies, and DOKU delivery capacity.

### Project governance

Identify:
- Executive sponsor.
- Merchant business owner.
- Merchant technical owner.
- DOKU account owner.
- Presales / solution owner.
- Product owner.
- Engineering owner.
- Operations owner.
- Risk / compliance stakeholders.

---

## 13. Commercial proposal structure

Use this structure for merchant-facing proposals.

### Section 1 — Executive summary

Include:
- Merchant business context.
- Main problem.
- Proposed solution.
- Expected outcome.
- Required decision.

### Section 2 — Current-state assessment

Show:
- Current billing process.
- Payment and collection process.
- Main pain points.
- Baseline metrics.

### Section 3 — Proposed solution

Explain:
- Selected FlexiBill solution pattern.
- Merchant journey.
- Customer journey.
- Supported capabilities.
- Integration approach.

### Section 4 — Architecture and operating model

Show:
- High-level architecture.
- Data ownership.
- API, webhook, or batch interactions.
- Roles and responsibilities.
- Operational support model.

### Section 5 — Commercial value

Show:
- Billing opportunity.
- Expected DOKU payment volume.
- Potential operational benefits.
- Assumptions and measurement method.

### Section 6 — Scope and implementation

Show:
- Included scope.
- Exclusions.
- Dependencies.
- Delivery stages.
- Acceptance criteria.

### Section 7 — Commercial terms

Show only approved:
- Pricing structure.
- Payment processing fees.
- Setup or implementation charges.
- Minimum commitments, if applicable.
- Contract terms.
- Billing and settlement arrangements.

### Section 8 — Risks and assumptions

Clearly disclose:
- Product conditions.
- Technical dependencies.
- Country limitations.
- Merchant responsibilities.
- Third-party dependencies.
- Open validation items.

### Section 9 — Next steps

Include:
- Required decisions.
- Owners.
- Target dates.
- Approval requirements.

---

## 14. Commercial proposal approval checklist

Before sending an external proposal, confirm:

### Business
- [ ] Merchant requirements are documented.
- [ ] Business problem is clearly stated.
- [ ] Expected outcome is measurable.
- [ ] Commercial opportunity has an evidence-based baseline.

### Product
- [ ] Every mandatory capability has been classified.
- [ ] Product gaps are disclosed.
- [ ] Roadmap items are not presented as released features.
- [ ] Country-specific availability is validated.

### Technical
- [ ] Integration pattern is agreed.
- [ ] API and webhook scope is confirmed.
- [ ] Data ownership is defined.
- [ ] Security requirements are reviewed.
- [ ] Testing and certification responsibilities are documented.

### Operations
- [ ] Billing and payment monitoring are addressed.
- [ ] Failure and recovery ownership is defined.
- [ ] Reconciliation responsibilities are documented.
- [ ] Customer support model is agreed.

### Commercial and governance
- [ ] Fees and pricing are approved.
- [ ] Forecast assumptions are documented.
- [ ] Implementation scope is clear.
- [ ] Exclusions are stated.
- [ ] Required internal approvals are complete.
- [ ] Contract and risk review requirements are identified.

---

## 15. Common solution-design mistakes

| Mistake | Consequence | Prevention |
|---|---|---|
| Designing before discovery | Incorrect scope | Complete discovery first |
| Selling features rather than outcomes | Weak commercial case | Link features to measurable value |
| Assuming all lifecycle actions are native | Delivery risk | Validate each action |
| Ignoring payment authorization | Collection failure or consent risk | Map authorization explicitly |
| No system-of-record definition | Inconsistent billing status | Define ownership |
| No reconciliation design | Finance exceptions | Agree identifiers and matching rules |
| Treating all failures as recoverable | Inflated business case | Use evidence-based recovery assumptions |
| Unclear scope boundaries | Scope disputes | Define inclusions and exclusions |
| Promising roadmap delivery | Commercial and reputational risk | Use approved commitments only |
| Omitting operational ownership | Post-launch service issues | Include support and escalation model |

---

## 16. Solution design acceptance criteria

A solution design is ready for proposal approval when:

1. The business problem is agreed.
2. Requirements are prioritized.
3. The target merchant workflow is documented.
4. The target customer journey is documented.
5. The solution pattern is selected.
6. Architecture and integration responsibilities are clear.
7. Mandatory product capabilities are validated.
8. Country and payment eligibility are confirmed.
9. Risks and dependencies are documented.
10. Business case assumptions are transparent.
11. Scope and exclusions are defined.
12. Implementation and operational owners are identified.

---

## 17. Final principle

A strong FlexiBill proposal is not just a product presentation or a fee quotation.

It is a delivery-backed business proposition:

**Merchant problem → Validated solution → Clear architecture → Defined scope → Measurable value → Approved commercial commitment.**

---

**End of Playbook 05**
