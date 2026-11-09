# 01 — Collection Management

## 1. Overview

Collection Management is the starting point for organising customers and billing relationships in FlexiBill.

A Collection provides a logical grouping structure for managing customers or members who are associated with a particular billing programme, product, service, or business arrangement.

It forms part of the broader configuration flow:

**Collection → Plan → Pricing → Customer / Member → Billing → Payment**

## 2. Business Purpose

Merchants use Collections to:

- Organise customers into billing programmes.
- Separate different products, services, or customer segments.
- Establish the structure for subsequent plan and pricing configuration.
- Support subscription and recurring billing operations.
- Manage billing populations in a more structured way.

## 3. Where Collection Fits

A typical FlexiBill configuration follows this sequence:

1. Create a Collection.
2. Define the relevant Plan.
3. Configure the Plan's pricing and billing rules.
4. Associate customers or members.
5. Set up the appropriate billing and payment journey.
6. Monitor billing execution and payment outcomes.

## 4. Merchant Use Cases

| Merchant | Example Collection |
|---|---|
| Insurance | Health Insurance Policyholders |
| Education | Monthly Tuition Members |
| Fitness | Gym Membership |
| SaaS | Business Software Subscribers |
| Retail | VIP Membership Programme |
| Travel | Annual Travel Membership |
| Lending | Monthly Repayment Customers |

## 5. Recommended Collection Design

Collections should reflect meaningful business or operational distinctions.

Examples:

- Product-based: Basic Membership, Premium Membership.
- Segment-based: SME, Enterprise.
- Programme-based: Corporate Insurance, Individual Insurance.
- Country-based: Indonesia, Malaysia, where separate configuration is required.

Avoid creating unnecessary duplicate Collections for customers who can be managed under the same billing programme.

## 6. Configuration Workflow

Use the following operational sequence:

1. Access the FlexiBill merchant dashboard.
2. Navigate to the Collection management area.
3. Create a new Collection.
4. Enter the required Collection information.
5. Save and verify the Collection.
6. Proceed to Plan configuration.
7. Validate the relationship between the Collection, Plan, and intended customer group.

**Important:** Exact field names, mandatory inputs, editing rules, and dashboard navigation must be validated against the current Indonesia and Malaysia merchant interfaces before publication as a definitive UI guide.

## 7. Example Configuration

**Scenario:** A fitness merchant offers two membership programmes.

| Configuration | Collection A | Collection B |
|---|---|---|
| Name | Standard Membership | Premium Membership |
| Target customers | Standard gym members | Premium gym members |
| Billing model | Recurring | Recurring |
| Next step | Configure Standard Plan | Configure Premium Plan |

The merchant can organise the two programmes separately and configure their respective plans and pricing.

## 8. Dependencies

Collection Management should be understood together with:

- Plan and Pricing Configuration
- Member Center
- Pricing Table
- Billing Portal
- Subscription Lifecycle
- Payment Management

## 9. Common Risks and Checks

| Risk | Recommended check |
|---|---|
| Duplicate Collections | Agree naming and grouping conventions |
| Wrong customer grouping | Validate the intended merchant programme |
| Incorrect Plan association | Check Collection-to-Plan relationships |
| Country assumptions | Validate ID and MY availability separately |
| Unclear lifecycle ownership | Define which team manages customer and billing changes |

## 10. KPIs and Operational Monitoring

Collection-level monitoring can help merchants and internal teams understand:

- Number of customers or members.
- Number of active subscriptions.
- Billing volume.
- Successful and failed payment volume.
- Collection success rate.
- Outstanding billing amount.
- Renewal and churn performance.

These are recommended monitoring dimensions; availability of native Collection-level reporting must be validated.

## 11. Related Playbooks

1. [Plan & Pricing Configuration](02-plan-and-pricing-configuration.md)
2. [Member Center](04-member-center.md)
3. [Pricing Table](03-pricing-table.md)
4. [Billing Portal](05-billing-portal.md)
5. [Subscription Lifecycle](07-subscription-lifecycle.md)

## 12. Country and Capability Validation

| Scope | Status |
|---|---|
| Indonesia | Validate against current merchant dashboard and product documentation |
| Malaysia | Validate against current merchant dashboard and product documentation |
| Cross-country parity | Do not assume without confirmation |

## 13. Document Governance

- Document: Collection Management
- Product: DOKU FlexiBill
- Category: Product Configuration
- Country scope: Indonesia and Malaysia
- Status: Working playbook — validation required
- Owner: FlexiBill Product
- Last reviewed: 9 November 2026

---

*Internal DOKU knowledge base. Refer to the latest approved product and technical documentation before merchant implementation.*
