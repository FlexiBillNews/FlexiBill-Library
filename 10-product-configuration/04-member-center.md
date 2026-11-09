# 04 — Member Center

## 1. Overview

Member Center is the customer membership and identification component within the FlexiBill ecosystem.

It supports the organisation of customer membership information and the relationship between a merchant, its customers, and the relevant billing arrangements.

It should be understood as part of the broader subscription operating model, rather than simply a payment page.

**Typical relationship:**

Merchant → Collection → Plan → Member → Billing → Payment

The exact functions available depend on the enabled product configuration and integration method.

## 2. Business Purpose

Member Center helps merchants establish and manage customer membership relationships.

Business objectives include:

- Identify customers participating in a merchant's programme.
- Organise membership information.
- Connect customers with relevant billing arrangements.
- Support membership registration workflows.
- Provide a foundation for subscription and recurring billing operations.
- Support customer identification across relevant merchant journeys.

## 3. Where Member Center Fits in FlexiBill

| FlexiBill component | Responsibility |
|---|---|
| Collection | Organises the billing programme |
| Plan | Defines the merchant's offering |
| Pricing | Defines the commercial and billing rules |
| Pricing Table | Presents offerings to prospective customers |
| Member Center | Supports customer membership information and identification |
| Billing Portal | Supports customer billing and subscription self-service, where enabled |
| Billing engine | Executes configured billing workflows |
| Payment | Processes the applicable payment transaction |

Member Center is relevant when the merchant needs an identifiable customer or member relationship as part of the billing model.

## 4. Typical Merchant Use Cases

| Industry | Member Center use case |
|---|---|
| Fitness | Identify gym members and their membership arrangements |
| Insurance | Associate policyholders with billing relationships |
| Education | Organise student and parent billing records |
| SaaS | Associate business customers with subscription arrangements |
| Retail | Manage customer membership programmes |
| Travel | Identify recurring travel membership customers |
| Professional services | Associate clients with recurring service arrangements |

## 5. Membership Information

A merchant should define the customer information required for its operating model.

Potential information categories include:

| Category | Example |
|---|---|
| Customer identity | Name |
| Contact information | Email address, mobile number |
| Customer reference | Merchant customer ID |
| Membership reference | Member ID |
| Billing relationship | Associated Collection or Plan |
| Status | Membership or subscription status, where available |

This is a conceptual information model, not a definitive list of native Member Center fields.

Validate actual mandatory fields, editable fields, unique identifiers, and available status values against the current product documentation.

## 6. Customer Registration Journey

A typical customer registration journey can be designed as follows:

1. Merchant creates the Collection and Plan.
2. Merchant configures the customer acquisition journey.
3. Customer receives a Pricing Table link or another supported registration entry point.
4. Customer enters the required registration information.
5. Customer completes applicable verification and consent steps.
6. Customer proceeds through the configured payment or subscription authorisation process.
7. The merchant verifies the resulting membership and billing relationship.

The actual sequence depends on the enabled registration and payment flow.

Do not assume that all merchants use the same registration interface or that every registration channel automatically creates a Member Center record.

## 7. Membership and Subscription Are Different

A member record and a subscription should not be treated as identical concepts.

| Member | Subscription |
|---|---|
| Represents the customer relationship | Represents a billing or service agreement |
| Identifies a customer in the merchant programme | Defines the recurring commercial relationship |
| May exist before a paid subscription | Has its own lifecycle and payment outcomes |
| Can be associated with merchant membership information | Can be active, failed, cancelled, or otherwise transitioned according to supported rules |

Example:

A customer registers as a gym member but has not completed the initial payment.

The membership registration and the subscription payment outcome must be tracked as separate business events where the product supports that distinction.

## 8. Member Center and Pricing Table

Pricing Table and Member Center serve complementary purposes.

| Pricing Table | Member Center |
|---|---|
| Presents merchant products and Plans | Supports membership information |
| Helps customers discover offerings | Helps identify registered members |
| Supports acquisition journeys | Supports customer relationship workflows |
| Focuses on product and pricing presentation | Focuses on member information |

Example journey:

1. Customer opens the gym's Pricing Table.
2. Customer selects Premium Membership.
3. Customer enters registration information.
4. The configured registration process creates or associates the relevant membership record.
5. Customer completes the payment journey.
6. Merchant verifies membership and subscription status.

Validate the exact technical connection between these components before promising a specific automated flow.

## 9. Member Center and Billing Portal

Member Center and Billing Portal should also be distinguished.

| Member Center | Billing Portal |
|---|---|
| Membership and customer information | Customer-facing billing and subscription interface |
| Customer identification | Billing self-service |
| Membership relationship | Billing and subscription management, where supported |
| Merchant membership operations | Customer billing experience |

They can work together as part of an integrated customer experience, subject to available functionality.

## 10. API and Integration Considerations

Member Center functionality must be evaluated separately across dashboard and API experiences.

Key questions for implementation:

- Can a merchant create or register a member through an API?
- Can an existing member be retrieved?
- How is membership uniquely identified?
- Can a member be associated with a Collection or Plan through an API?
- What fields are mandatory?
- How are duplicate registrations handled?
- What events or webhooks are available?
- How is customer information updated?

**Known implementation consideration:** Member Center API readiness and customer-facing frontend readiness are separate matters. API availability must not be interpreted as confirmation that a complete merchant-facing or customer-facing frontend is available.

Validate the current API contract, endpoint availability, permissions, and country scope before implementation.

## 11. Customer Data and Operational Governance

Merchants should establish clear ownership of customer information.

Recommended controls:

- Define a consistent customer identifier.
- Avoid duplicate member records.
- Validate email and mobile number formats.
- Define customer-data update ownership.
- Apply appropriate consent and privacy requirements.
- Restrict access to authorised merchant users.
- Establish retention and deletion procedures.
- Reconcile member records with billing and payment records.

Only collect personal information that is necessary for the merchant's legitimate operating requirements.

## 12. Example: Fitness Membership

**Business scenario**

A fitness merchant offers Basic and Premium memberships.

| Configuration | Basic | Premium |
|---|---|---|
| Collection | Gym Membership | Gym Membership |
| Plan | Basic Plan | Premium Plan |
| Monthly price | Rp250,000 | Rp500,000 |
| Member | Registered customer | Registered customer |
| Billing | Monthly | Monthly |

Illustrative customer journey:

1. Customer discovers the Pricing Table.
2. Customer selects a membership.
3. Customer registers.
4. Merchant establishes the member relationship through the configured workflow.
5. Customer completes the payment authorisation.
6. The subscription and subsequent billing follow the configured rules.
7. Merchant monitors the membership and payment outcomes.

## 13. Troubleshooting

| Issue | Investigation |
|---|---|
| Duplicate member | Check customer identifiers and registration logic |
| Member not associated with Plan | Verify the configured relationship and registration flow |
| Registration incomplete | Check required fields and verification steps |
| API registration failure | Review request validation and API response |
| Payment succeeded but membership not updated | Investigate integration events and status synchronisation |
| Member exists but subscription is inactive | Check subscription lifecycle and payment outcome |
| Customer cannot access billing information | Validate Billing Portal eligibility and access flow |

## 14. KPIs and Monitoring

Recommended business monitoring:

| KPI | Purpose |
|---|---|
| Total registered members | Measure membership population |
| New members | Track acquisition |
| Active members | Measure active customer relationships |
| Members with active subscriptions | Understand paid membership penetration |
| Member-to-paid conversion | Measure registration conversion |
| Duplicate member rate | Monitor data quality |
| Registration completion rate | Identify onboarding friction |
| Member churn | Understand customer attrition |
| Member billing success rate | Measure payment performance |

These are recommended metrics. Confirm which are available as native reports and which require merchant-side analytics.

## 15. Indonesia
