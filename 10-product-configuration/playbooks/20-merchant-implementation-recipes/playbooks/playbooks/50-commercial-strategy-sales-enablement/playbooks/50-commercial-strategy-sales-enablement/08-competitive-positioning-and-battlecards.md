# Competitive Positioning and Battlecards

**Playbook:** Commercial Strategy & Sales Enablement  
**Document:** 08 — Competitive Positioning and Battlecards  
**Audience:** DOKU Sales, Presales, Product, Partnership, and Management  
**Status:** Internal working playbook — competitor capabilities and commercial positioning must be validated before external use

---

## 1. Purpose

This playbook helps DOKU teams position FlexiBill against alternative billing, subscription management, recurring payment, and payment orchestration solutions.

It provides:

1. A competitive landscape framework.
2. A clear FlexiBill positioning statement.
3. Competitor comparison dimensions.
4. Practical battlecards.
5. Discovery questions for competitive opportunities.
6. Objection-handling guidance.
7. Win/loss intelligence requirements.
8. Competitive response guardrails.

**Core principle:**

> Do not try to prove FlexiBill is better at everything. Identify where FlexiBill provides the strongest fit for the merchant's actual billing and payment requirements.

Competitor capabilities, pricing, integrations, and regional availability change. Validate current information before using any comparison externally.

---

## 2. Define the competitive landscape

FlexiBill competes across several overlapping categories. Not every alternative is a direct competitor.

| Category | What it typically provides | Merchant alternative |
|---|---|---|
| Subscription billing platforms | Subscription lifecycle, plans, invoices, recurring billing | Dedicated subscription software |
| Billing automation platforms | Billing schedules, invoice generation, payment workflows | Billing management software |
| Payment gateways / processors | Payment acceptance and transaction processing | Payment provider with recurring features |
| Merchant-built billing systems | Custom billing logic and internal workflows | In-house engineering |
| Vertical SaaS platforms | Industry-specific customer and billing workflows | Industry software with payment integrations |
| Bank recurring payment solutions | Recurring collection through specific bank or payment arrangements | Bank-led collection |
| Manual processes | Spreadsheets, file uploads, email, and manual follow-up | Existing operational process |

### Competitive assessment question

What is the merchant actually replacing?

- A payment provider?
- A billing engine?
- A subscription management system?
- An internal application?
- A manual billing process?
- Several disconnected systems?

This distinction determines the relevant competitor set.

---

## 3. FlexiBill positioning

### Recommended positioning statement

**FlexiBill is a payment-connected billing orchestration solution that helps merchants structure billing workflows and connect them with supported DOKU payment collection capabilities.**

It can support different implementation approaches depending on merchant needs:

- DOKU-hosted Billing Automation.
- API / Host-to-Host integration.
- Hybrid workflows.
- Eligible batch-based processes.
- Merchant Hosted Scheduler for the documented eligible scope, subject to country validation.

### Positioning pillars

| Pillar | Merchant problem | FlexiBill proposition |
|---|---|---|
| Billing structure | Billing logic is fragmented or manual | Configure supported billing structures |
| Payment connection | Billing and payment are disconnected | Connect billing workflows to supported DOKU payment capabilities |
| Integration flexibility | Different merchants have different technology models | Select an appropriate hosted, API, Hybrid, or batch pattern |
| Operational visibility | Limited visibility into billing and payment outcomes | Establish more structured billing and payment monitoring |
| Merchant growth | Billing workload grows with customer base | Support repeatable billing workflows |

### What FlexiBill should not claim without validation

Do not position FlexiBill as having:
- Complete enterprise subscription lifecycle management.
- Universal plan changes and proration APIs.
- Native real-time metering and usage aggregation.
- Full wallet and entitlement management.
- Complete revenue recognition and accounting.
- Universal global tax and currency handling.
- Multi-product hierarchy and consolidated invoicing.
- Universal cross-merchant bill payment or one-VA capability.

These are not to be represented as generally available native capabilities without explicit product confirmation.

---

## 4. Competitive comparison framework

Compare competitors using the same dimensions.

| Dimension | Assessment question |
|---|---|
| Billing model | Does it support the merchant's billing structure? |
| Pricing | Which pricing models are supported? |
| Recurring collection | Which recurring payment mechanisms are supported? |
| Payment methods | Which methods are available in the target country? |
| Authorization | How is recurring payment authorization managed? |
| Subscription lifecycle | Which customer lifecycle actions are supported? |
| Customer experience | Which customer-facing interfaces are available? |
| Merchant experience | How are configuration and operations managed? |
| Integration | API, webhook, hosted, batch, or other methods? |
| Monitoring | What billing and payment visibility is provided? |
| Recovery | What failed-payment handling is supported? |
| Reconciliation | How are billing and payment records matched? |
| Localization | Which markets and local payment methods are supported? |
| Commercial model | Transaction, subscription, usage, setup, or other fees? |
| Implementation | How much merchant engineering is required? |
| Extensibility | How easily can merchant-specific workflows be supported? |

### Comparison scoring

Use a 1–5 scale:

| Score | Meaning |
|---:|---|
| 1 | Materially insufficient |
| 2 | Limited |
| 3 | Adequate for the use case |
| 4 | Strong |
| 5 | Excellent / well matched |

Add a separate evidence confidence:

- Verified.
- Public documentation.
- Demonstrated.
- Merchant-reported.
- Unverified.

Never give a competitor a low score simply because the capability is not visible in a sales demo.

---

## 5. Competitive landscape: reference providers

The following providers are useful reference points for competitive research. Their inclusion does not imply a verified current feature-by-feature comparison.

### A. Stripe Billing

<Entity category="software" value="Stripe Billing" disambig="Subscription and recurring billing software"/> 

**Competitive category:** Subscription billing and payment ecosystem.

Typical evaluation areas:
- Subscription lifecycle.
- Recurring payments.
- Invoicing and billing.
- Payment recovery.
- API and developer experience.
- International payment operations.

**FlexiBill comparison angle:**

Evaluate whether the merchant needs a broad subscription software stack or a billing and payment orchestration solution aligned with DOKU's supported payment ecosystem.

**Discovery questions:**
- Does the merchant use Stripe for billing, payments, or both?
- Which subscription lifecycle capabilities are essential?
- Which local payment methods are required?
- Does the merchant need a different local payment and operating model?

### B. Chargebee

<Entity category="software" value="Chargebee" disambig="Subscription management and recurring billing platform"/>

**Competitive category:** Subscription management and revenue operations.

Typical evaluation areas:
- Subscription management.
- Pricing and plan management.
- Invoicing.
- Dunning and recovery.
- Revenue operations.
- Integrations.

**FlexiBill comparison angle:**

Understand whether the merchant's primary requirement is advanced subscription lifecycle management or a payment-connected billing workflow.

**Discovery questions:**
- Which subscription lifecycle actions are actively used?
- Is complex plan change and proration essential?
- Which payment providers and methods are connected?
- Which system owns customer and subscription data?

### C. Paddle

<Entity category="software" value="Paddle" disambig="Software payments and merchant-of-record platform"/>

**Competitive category:** Software commerce and merchant-of-record services.

Typical evaluation areas:
- Software subscription commerce.
- Payment acceptance.
- Tax and compliance services.
- Checkout and customer operations.
- Global digital commerce.

**FlexiBill comparison angle:**

Determine whether the merchant needs a billing and payment integration or a merchant-of-record model with broader commercial and tax responsibilities.

**Discovery questions:**
- Who is the legal seller of record?
- Who owns tax and compliance obligations?
- Which countries are targeted?
- Does the merchant require software commerce services beyond billing and payment collection?

### D. HitPay

<Entity category="brand" value="HitPay" disambig="Payment gateway and payment acceptance platform"/>

**Competitive category:** Payment acceptance with business payment tools.

Typical evaluation areas:
- Local payment methods.
- Payment links and checkout.
- Recurring payment support.
- Merchant experience.
- Regional payment coverage.

**FlexiBill comparison angle:**

Compare the merchant's complete billing workflow, recurring collection requirements, payment methods, and operational needs rather than comparing only checkout features.

**Discovery questions:**
- Is the current provider used only for payment acceptance?
- How are billing obligations created?
- Does the merchant need subscription or membership management?
- Which payment methods are essential in each country?

### E. Metronome

<Entity category="software" value="Metronome" disambig="Usage-based billing and monetization platform"/>

**Competitive category:** Usage-based billing and monetization.

Typical evaluation areas:
- Usage event ingestion.
- Metering.
- Rating and pricing.
- Usage-based invoicing.
- Enterprise billing workflows.

**FlexiBill comparison angle:**

Identify whether the merchant needs native usage metering and real-time rating or whether merchant-calculated billing amounts can be submitted through an appropriate supported workflow.

Do not present Meter-Lite or merchant-calculated bill generation as equivalent to a full native metering platform.

**Discovery questions:**
- Where is usage calculated?
- Is real-time metering required?
- Are usage events aggregated by FlexiBill or the merchant?
- Is rating performed before billing?
- How are adjustments and corrections handled?

---

## 6. Battlecard — Dedicated subscription platform

**Competitor type:** Subscription management software.

### Typical merchant situation

The merchant already uses a dedicated subscription platform and is considering whether to retain it, replace it, or connect a different payment provider.

### Merchant priorities
- Subscription lifecycle management.
- Pricing and plan flexibility.
- Payment collection.
- Failed-payment recovery.
- Customer self-service.
- Reporting and integrations.

### FlexiBill conversation

Do not argue that FlexiBill replaces every subscription platform function.

Instead:
1. Identify which subscription functions the merchant actually uses.
2. Identify the current payment provider.
3. Determine which billing responsibilities belong to the subscription platform.
4. Validate the payment methods and recurring collection requirements.
5. Evaluate whether FlexiBill can serve the required billing and payment workflow.
6. Identify any lifecycle features that would remain in the merchant's existing system.

### Potential differentiation

- Alignment with DOKU payment capabilities.
- Flexible implementation patterns.
- Merchant-specific integration design.
- Structured billing and collection workflows.

### Risks to acknowledge

If advanced subscription lifecycle functions are mandatory and unavailable in the validated FlexiBill scope, do not claim full replacement capability.

### Winning scenario

The merchant has a subscription platform requirement that can be satisfied by a supported FlexiBill workflow, or the merchant wants to retain its subscription system while changing the billing and payment integration.

---

## 7. Battlecard — Payment gateway with recurring features

**Competitor type:** Payment gateway or payment processor.

### Typical merchant situation

The merchant already accepts payments through another provider and wants to improve recurring billing or payment collection.

### Merchant priorities
- Payment success.
- Local payment method coverage.
- Recurring authorization.
- Transaction pricing.
- Settlement.
- Payment reporting.
- Integration effort.

### FlexiBill conversation

Explore the complete billing process:
- Who generates billing obligations?
- Who schedules recurring collection?
- Who manages customer authorization?
- Who tracks failed billing?
- Who reconciles payment results?
- What customer-facing experience is required?

### Potential differentiation

Position FlexiBill around the connection between billing structure and DOKU payment capabilities, not simply as another payment gateway.

### Winning scenario

The merchant has fragmented billing and payment operations and needs a more structured workflow supported by validated FlexiBill capabilities.

---

## 8. Battlecard — In-house billing system

**Competitor type:** Merchant-built billing application.

### Typical merchant situation

The merchant has its own application and billing logic but relies on internal teams to maintain payment and billing operations.

### Merchant priorities
- Full control over business logic.
- Custom workflows.
- Developer flexibility.
- Cost of ownership.
- Reliability.
- Time to market.

### FlexiBill conversation

Understand what the merchant wants to retain and what it wants to outsource or simplify.

Potential design:
- Merchant retains customer and business logic.
- FlexiBill supports validated billing or payment workflows.
- API / H2H or Hybrid integration connects the systems.
- Merchant retains agreed system-of-record responsibilities.

### Potential differentiation

- Reduce the need to build every payment-connected billing workflow internally.
- Use supported DOKU payment infrastructure.
- Retain merchant control where required.

### Risks to acknowledge

Do not assume FlexiBill removes the need for merchant engineering. API integration, data ownership, exception handling, and customer lifecycle logic may remain merchant responsibilities.

### Winning scenario

The merchant wants to retain its core system while reducing the complexity of payment-connected billing operations.

---

## 9. Battlecard — Manual billing and spreadsheets

**Competitor type:** Existing manual process.

### Typical merchant situation

Billing is managed through spreadsheets, messaging applications, manual payment links, bank statements, or staff follow-up.

### Merchant priorities
- Lower operational workload.
- Better billing visibility.
- Fewer manual errors.
- Faster payment confirmation.
- More consistent customer experience.

### FlexiBill conversation

Map the current workflow and quantify:
- Manual billing hours.
- Number of billing records.
- Payment-status follow-up workload.
- Unmatched transactions.
- Failed and overdue billing.
- Reconciliation effort.

### Potential differentiation

Introduce a more structured billing and payment workflow using validated FlexiBill capabilities.

### Winning scenario

The merchant has a measurable manual billing problem and a supported solution can reduce operational friction.

---

## 10. Competitive discovery questions

Use these questions before creating a battlecard for a specific opportunity.

### Current provider and system
- Which billing platform do you currently use?
- Which payment provider is connected?
- Which functions are handled internally?
- What is the most difficult part of the current setup?

### Billing requirements
- How are billing obligations generated?
- Which pricing models are required?
- Which billing frequencies are used?
- Are plan changes, proration, or usage-based billing mandatory?

### Payment requirements
- Which payment methods are required?
- Is recurring authorization needed?
- How are failed payments managed?
- What are the settlement and reconciliation requirements?

### Customer experience
- How do customers register?
- How do customers view bills?
- How do they update payment information?
- Which lifecycle actions must be self-service?

### Commercial
- What is the current fee structure?
- What other platform or integration costs exist?
- What is the total cost of operating the current solution?
- What would trigger a provider change?

---

## 11. Competitive objection handling

### "Our current provider already supports recurring payments."

Response:

"That's useful. Let's understand whether your challenge is recurring payment execution or the broader billing workflow. We should compare how billing obligations are generated, authorized, collected, monitored, recovered, and reconciled."

### "The competitor has more features."

Response:

"That may be the case for certain subscription or billing functions. Let's prioritize the capabilities you actually need and distinguish mandatory requirements from future enhancements. We should choose the solution that best fits your operating model."

### "We do not want to rebuild our current system."

Response:

"We should first identify which parts of your existing system should remain. An API or Hybrid approach may be appropriate if the required FlexiBill capabilities and integration interfaces are validated."

### "The competitor is cheaper."

Response:

"Let's compare the full commercial model using the same transaction volume, payment methods, fee basis, and service scope. We should also consider implementation and operating costs."

### "We need advanced usage-based billing."

Response:

"We should map your usage calculation and rating requirements carefully. FlexiBill may support certain merchant-calculated billing workflows, but native real-time metering and advanced usage aggregation require separate validation."

### "We need global subscription management."

Response:

"Let's separate the global subscription management requirement from the local payment collection requirement. We can assess whether a hybrid architecture is appropriate, while validating each country and payment method separately."

---

## 12. Competitive win/loss framework

Record every significant competitive opportunity.

| Field | Required information |
|---|---|
| Merchant | Name and segment |
| Country | ID / MY / Other |
| Vertical | Industry |
| Competitor | Provider or alternative |
| Current solution | Existing operating model |
| Required capabilities | Mandatory merchant needs |
| FlexiBill fit | Available / Conditional / Gap |
| Main advantage | Evidence-based |
| Main weakness | Evidence-based |
| Commercial outcome | Won / Lost / Stalled |
| Reason | Documented reason |
| Follow-up | Product, commercial, or GTM action |

### Win/loss analysis questions

1. Which capabilities influenced the decision?
2. Was pricing the primary factor?
3. Did local payment coverage matter?
4. Did integration complexity matter?
5. Did the competitor provide a capability FlexiBill did not?
6. Was the opportunity lost because of product fit or sales execution?
7. What should change in product, pricing, or positioning?

Do not treat a single merchant's preference as proof of market-wide competitive advantage.

---

## 13. Competitive intelligence governance

All competitive material must have:
- Named owner.
- Source and evidence.
- Last-verified date.
- Country and market scope.
- Product version or relevant release context.
- Confidence level.
- Internal or external usage classification.

### Evidence standards

| Evidence type | Confidence treatment |
|---|---|
| Official product documentation | Strong evidence for documented capability |
| Official pricing page | Evidence for publicly stated pricing, subject to conditions |
| Product demonstration | Evidence of demonstrated workflow |
| Merchant feedback | Useful but requires corroboration |
| Third-party review | Contextual evidence, not definitive proof |
| Sales assumption | Unverified until validated |

Do not circulate outdated screenshots or competitor claims without checking their current relevance.

---

## 14. Competitive response matrix

| Merchant requirement | FlexiBill response |
|---|---|
| Local payment collection | Validate supported DOKU payment methods |
| Recurring billing | Map to supported billing and authorization workflow |
| Merchant-owned system | Evaluate API / H2H or Hybrid pattern |
| Bulk billing | Validate applicable batch or upload workflow |
| Customer registration | Validate Member Center API and frontend separately |
| Plan and pricing configuration | Validate supported pricing models |
| Advanced plan changes | Confirm current API and lifecycle support |
| Real-time usage billing | Identify merchant-side calculation or product gap |
| Failed-payment recovery | Define supported workflow and ownership |
| Cross-country operations | Validate each country independently |

---

## 15. Battlecard preparation checklist

Before using a battlecard in a merchant meeting:

- [ ] Competitor category is correctly identified.
- [ ] Merchant's actual use case is understood.
- [ ] Competitor capabilities have current evidence.
- [ ] Comparison uses equivalent requirements.
- [ ] FlexiBill capabilities have been validated.
- [ ] Product gaps are disclosed internally.
- [ ] Country scope is confirmed.
- [ ] Pricing is not speculative.
- [ ] External claims are approved.
- [ ] Follow-up questions are prepared.

---

## 16. Final principle

Competitive positioning should help DOKU make better decisions, not encourage unsupported claims.

**Understand the merchant's current solution → Identify the real problem → Compare equivalent requirements → Validate FlexiBill fit → Explain differentiated value → Disclose limitations → Build a credible proposal.**

FlexiBill wins when its validated capabilities, payment ecosystem, implementation approach, and commercial model fit the merchant's real business needs.

---

**End of Playbook 08**
