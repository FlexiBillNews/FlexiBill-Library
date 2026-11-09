# FlexiBill Operating Model and RACI

**Document type:** Operations playbook  
**Audience:** Product, Engineering, Operations, Finance, Customer Support, Business Development, Implementation, and merchants  
**Markets:** Indonesia (ID) and Malaysia (MY)  
**Status:** Internal operating reference — validate against actual team structure and approved country procedures

---

## 1. Purpose

This playbook defines the operating model required to run FlexiBill as a billing and payment orchestration product.

It establishes:

- Functional ownership across the FlexiBill lifecycle
- Decision-making responsibilities
- Cross-team handoffs
- Merchant and DOKU responsibilities
- Operational escalation paths
- Governance for product changes and incidents

The objective is to avoid unclear ownership when a billing, payment, integration, settlement, or customer issue occurs.

**Operating principle:** Every critical activity must have one clearly accountable owner, even when several teams contribute.

## 2. Operating model overview

FlexiBill operations span six connected domains.

| Domain | Primary responsibility |
|---|---|
| Product governance | Product vision, capability definition, prioritization, roadmap, and release decisions |
| Merchant implementation | Merchant onboarding, configuration, integration, UAT, and go-live coordination |
| Platform operations | Monitoring, operational execution, exception handling, and incident coordination |
| Engineering and technology | Platform reliability, APIs, integrations, defect resolution, and technical changes |
| Finance and reconciliation | Payment, settlement, fee, refund, and financial reconciliation |
| Customer and merchant support | Case intake, communication, investigation coordination, and resolution updates |

These domains are functional responsibilities. They do not prescribe a specific DOKU organizational structure.

## 3. Lifecycle ownership

| Lifecycle stage | Primary owner | Supporting teams | Expected output |
|---|---|---|---|
| Product discovery | Product | Business Development, Engineering, Operations | Validated requirement |
| Capability assessment | Product | Engineering, Implementation | Capability and gap assessment |
| Merchant onboarding | Implementation / Business Development | Product, Operations | Approved onboarding scope |
| Solution design | Solution Architecture / Engineering | Product, Implementation, Merchant IT | Approved design |
| Configuration | Implementation / authorized operator | Product, Merchant | Validated configuration |
| Integration | Engineering / Merchant IT | Implementation, Product | Working integration |
| UAT and certification | Implementation / Merchant | Product, Engineering, Operations | Signed-off test evidence |
| Go-live | Implementation / Operations | Engineering, Product, Merchant | Controlled production launch |
| Daily monitoring | Operations | Engineering, Finance, Merchant | Operational visibility |
| Payment investigation | Operations | Engineering, Payment Operations, Merchant | Resolved or escalated case |
| Reconciliation | Finance / Reconciliation | Operations, Merchant Finance | Reconciled records |
| Product improvement | Product | All relevant teams | Prioritized improvement |

The actual accountable role must be assigned for each merchant and market.

## 4. RACI definitions

| Code | Meaning | Responsibility |
|---|---|---|
| R | Responsible | Performs the work |
| A | Accountable | Owns the result and final decision |
| C | Consulted | Provides input before the decision or action |
| I | Informed | Receives relevant updates |

Every activity should have one Accountable role. Multiple Responsible roles may be appropriate.

## 5. Functional role definitions

### 5.1 Product Management

Owns the product definition and evolution of FlexiBill.

Responsibilities:

- Product vision and strategy
- Product capability definition
- Prioritization and roadmap
- Requirement clarification
- Product acceptance criteria
- Capability-gap assessment
- Product release communication
- Product performance review
- Alignment of ID and MY scope

Product must distinguish released capabilities from conditional capabilities, gaps, and future concepts.

### 5.2 Engineering and Technology

Owns technical delivery and platform reliability.

Responsibilities:

- Architecture and technical design
- API and webhook implementation
- Platform performance and availability
- Integration troubleshooting
- Defect investigation and resolution
- Security and technical controls
- Deployment and release execution
- Technical monitoring and observability

Engineering should not independently make unapproved commercial or product commitments.

### 5.3 Implementation and Solution Architecture

Owns merchant solution readiness and implementation coordination.

Responsibilities:

- Merchant requirement discovery
- Integration model selection
- Configuration and mapping
- Technical coordination
- Test planning and execution coordination
- UAT readiness
- Go-live checklist
- Merchant handover to operations

Implementation must verify that the proposed merchant journey is supported by the approved capability set.

### 5.4 Operations

Owns operational monitoring and execution within its assigned scope.

Responsibilities:

- Daily billing and payment monitoring
- Exception identification
- Operational investigation
- Case coordination
- Escalation management
- Recovery process monitoring
- Operational reporting
- Incident communication coordination

Operations must distinguish a confirmed failure from a pending or unknown payment outcome.

### 5.5 Finance and Reconciliation

Owns financial validation and reconciliation within its assigned scope.

Responsibilities:

- Payment-to-settlement reconciliation
- Fee and net settlement validation
- Refund and adjustment reconciliation
- Unmatched transaction investigation
- Financial reporting
- Merchant finance coordination
- Period-end control support

Finance must distinguish transaction success from settlement completion.

### 5.6 Customer and Merchant Support

Owns case intake, communication, and customer or merchant updates.

Responsibilities:

- Receive and classify inquiries
- Capture the required references and evidence
- Communicate known status accurately
- Coordinate investigations with the owning team
- Track case progress and closure
- Identify recurring complaint themes

Support must not promise a payment reversal, refund, retry, or billing adjustment without authorization from the relevant owner.

### 5.7 Business Development / Account Management

Owns commercial coordination and merchant relationship management.

Responsibilities:

- Merchant requirement and expectation management
- Commercial scope coordination
- Stakeholder alignment
- Merchant communication
- Escalation of business impact
- Coordination of expansion opportunities

Commercial teams must use Product-approved capability statements.

### 5.8 Merchant responsibilities

The merchant remains responsible for its own business rules and systems, including:

- Customer and payer data
- Product, policy, contract, or service entitlement
- Pricing and commercial rules unless explicitly assigned elsewhere
- Customer consent and communication
- Merchant-side integration
- Customer eligibility
- Business decisions such as suspension, reinstatement, and cancellation
- Merchant accounting and customer-level allocation

FlexiBill payment status must not automatically be treated as the source of truth for every merchant business decision.

---

## 6. RACI matrix

The following is a proposed functional RACI. Replace role names with the actual accountable DOKU team or role before operational adoption.

**Roles**

- PM: Product Management
- ENG: Engineering / Technology
- IMP: Implementation / Solution Architecture
- OPS: Operations
- FIN: Finance / Reconciliation
- CS: Customer / Merchant Support
- BD: Business Development / Account Management
- M: Merchant

| Activity | PM | ENG | IMP | OPS | FIN | CS | BD | M |
|---|---|---|---|---|---|---|---|---|
| Product strategy | A/R | C | C | C | I | I | C | I |
| Product requirement | A/R | C | C | C | I | I | C | C |
| Technical architecture | C | A/R | R | C | I | I | I | C |
| Merchant discovery | C | C | R | C | I | I | A/R | C |
| Capability validation | A | R | R | C | I | I | C | C |
| Merchant configuration | C | C | A/R | C | I | I | I | R |
| Merchant integration | I | A/R | R | C | I | I | I | R |
| UAT coordination | C | R | A/R | C | C | I | I | R |
| Go-live approval | C | R | A/R | R | C | I | C | R |
| Daily billing monitoring | I | C | C | A/R | I | I | I | R |
| Payment investigation | I | R | C | A/R | C | R | I | C |
| Technical incident resolution | I | A/R | C | R | I | I | I | C |
| Reconciliation | I | C | C | R | A/R | I | I | R |
| Customer communication | I | C | C | C | I | A/R | C | R |
| Merchant business-rule decision | I | I | C | C | I | I | C | A/R |
| Product enhancement prioritization | A/R | C | C | C | C | C | C | C |
| Commercial commitment | C | I | C | I | C | I | A/R | C |

**RACI governance notes**

1. The table is a starting point, not a substitute for formal DOKU delegation of authority.
2. For a production incident, the designated incident commander may coordinate teams without replacing the technical or business decision owner.
3. Merchant responsibilities must be documented in the integration agreement and operating procedure.
4. Where a function is not performed by a named team, assign an explicit role rather than leaving ownership blank.

## 7. Operational handoff model

### 7.1 Implementation to Operations

Before go-live handover, Implementation should provide:

- Merchant and country details
- Integration model
- Approved solution design
- Product configuration summary
- Payment methods and authorization approach
- Merchant technical contacts
- Billing and payment reference mapping
- Expected transaction volumes
- Monitoring requirements
- Known limitations and dependencies
- UAT evidence and sign-off
- Escalation contacts
- Go-live date and hypercare period

Operations should acknowledge handover readiness before the merchant is treated as operationally live.

### 7.2 Operations to Engineering

Escalation should include:

- Merchant ID or approved merchant reference
- Country and environment
- Billing or invoice reference
- Payment transaction reference, if available
- Timestamp and timezone
- Request / response or event reference
- Observed versus expected behavior
- Error information
- Business impact
- Reproduction steps
- Investigation already performed

Do not send unnecessary customer-sensitive data through unapproved channels.

### 7.3 Operations to Finance

Finance escalation should include:

- Merchant reference
- Payment transaction reference
- Billing or invoice reference
- Transaction amount and currency
- Transaction date
- Settlement date, if available
- Applicable fee information
- Expected and actual settlement values
- Nature of the mismatch
- Supporting approved evidence

### 7.4 Support to owning team

Support should capture the issue, classify it, and route it to the appropriate owner.

A support case is not considered resolved merely because it has been forwarded. The case owner must track investigation, communication, and closure.

---

## 8. Escalation ownership

| Issue category | First coordination owner | Resolution owner | Supporting roles |
|---|---|---|---|
| Incorrect product configuration | Implementation / Operations | Authorized configuration owner | Product, merchant |
| Billing not generated | Operations | Product / Engineering according to root cause | Implementation, merchant |
| API integration error | Engineering coordination | Engineering or merchant IT according to source | Implementation |
| Webhook not received | Operations / Engineering | Engineering or merchant IT | Merchant |
| Payment pending / unknown | Operations | Payment Operations / Engineering according to process | Merchant, Support |
| Payment decline | Operations | Relevant payment / issuer investigation path | Merchant, Support |
| Settlement mismatch | Finance | Finance / Reconciliation | Operations, merchant finance |
| Customer complaint | Customer Support | Relevant business or operational owner | Merchant, Operations |
| Product capability gap | Product | Product decision process | Engineering, Implementation, BD |
| Security incident | Designated security incident process | Authorized Security / Engineering owner | Relevant stakeholders |

Actual severity levels, service-level targets, and escalation contacts must be defined in the approved operating procedure.

## 9. Decision rights

| Decision | Decision owner |
|---|---|
| Product roadmap priority | Product governance |
| Product capability classification | Product with Engineering validation |
| Technical architecture | Engineering / Solution Architecture |
| Merchant business rule | Merchant |
| Merchant billing configuration | Authorized configuration owner |
| Production deployment | Authorized release governance |
| Operational recovery action | Authorized Operations / Payment Operations role |
| Financial adjustment | Authorized Finance role |
| Customer communication | Support / merchant according to agreement |
| Country-specific launch readiness | Relevant country and functional owners |
| Security incident response | Designated security incident authority |

A commercial request does not automatically authorize a technical or operational change.

## 10. Operating cadence

The following is a proposed cadence. Teams should agree the actual frequency based on transaction volume, merchant criticality, and operational coverage.

| Cadence | Meeting / activity | Participants | Expected output |
|---|---|---|---|
| Daily | Operational health review | Operations, Engineering as needed | Exceptions and priority incidents |
| Daily / agreed frequency | Payment and settlement exception review | Finance, Operations | Unresolved financial items |
| Weekly | Merchant performance review | Product, Operations, BD, Implementation | Merchant risks and improvement actions |
| Weekly | Product and engineering issue review | Product, Engineering | Defect and capability decisions |
| Monthly | FlexiBill business review | Product, BD, Finance, Operations | Performance, leakage, adoption |
| Monthly | Country review | ID / MY stakeholders | Country-specific issues and readiness |
| Quarterly | Product strategy and roadmap review | Product leadership and relevant stakeholders | Roadmap and investment decisions |

## 11. Operating KPIs

The operating model should report a balanced set of measures.

| KPI | Purpose | Primary owner |
|---|---|---|
| Billing generation success | Measure billing execution | Operations |
| Payment transaction success | Measure payment execution | Operations |
| Billing-level success | Measure successful collection of expected bills | Product / Operations |
| Failed billing value | Quantify value at risk | Product / Operations |
| Recovery rate | Measure recovered failed billing | Operations |
| Time to recovery | Measure recovery speed | Operations |
| Reconciliation exception rate | Measure financial control health | Finance |
| API error rate | Measure integration health | Engineering |
| Webhook processing success | Measure event processing | Engineering |
| Merchant activation | Measure implementation outcomes | Implementation / BD |
| Subscriber renewal / persistency | Measure subscription continuity | Product / Analytics |
| Support resolution time | Measure case handling | Customer Support |

Definitions and calculation rules must follow the KPI and Metric Dictionary.

## 12. Governance controls

The following controls should be maintained:

- Approved product capability reference
- Merchant solution design and integration agreement
- Country-specific operating procedures
- Production access and configuration authorization
- Change and release approval
- Incident and escalation records
- Reconciliation evidence
- Support case history
- UAT and go-live sign-off
- Operational dashboard ownership
- Periodic review of unresolved risks and capability gaps

## 13. Operating readiness checklist

### Ownership
- [ ] Each operational activity has an accountable owner.
- [ ] Merchant responsibilities are documented.
- [ ] Escalation contacts are available.
- [ ] Decision rights are clear.

### Implementation handover
- [ ] Solution design is approved.
- [ ] Configuration and integration details are documented.
- [ ] UAT evidence is available.
- [ ] Known limitations are communicated.
- [ ] Operations has accepted the handover.

### Daily operations
- [ ] Monitoring ownership is assigned.
- [ ] Pending and failed outcomes have investigation procedures.
- [ ] Recovery actions are controlled.
- [ ] Reconciliation exceptions have owners.
- [ ] Support routing is defined.

### Governance
- [ ] Country-specific validation is complete.
- [ ] Product claims are approved.
- [ ] Security and access controls are reviewed.
- [ ] Reporting definitions are consistent.
- [ ] Operating cadence is agreed.

---

## 14. Final operating principle

FlexiBill is successful when billing, payment, operational execution, and financial outcomes work together.

Product defines what the platform should do. Engineering ensures the technology works. Implementation makes the merchant solution operational. Operations monitors and coordinates execution. Finance validates financial outcomes. Support manages communication. The merchant remains accountable for its own business rules and customer obligations.

**One activity, one accountable owner, clear handoffs, measurable outcomes.**
