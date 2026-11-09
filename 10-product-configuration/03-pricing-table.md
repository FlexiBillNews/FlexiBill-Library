# 03 — Pricing Table

## 1. Overview

Pricing Table is a customer-facing presentation and acquisition capability that allows merchants to present their products, plans, and prices through a shareable digital experience.

It connects the merchant's commercial offering with the customer's subscription or payment journey.

**Configuration flow:**

Collection → Plan → Pricing → Pricing Table → Customer → Registration / Payment → Billing

Pricing Table helps merchants move from manually communicating prices to a more structured digital product-purchase experience.

## 2. Business Objectives

Pricing Table supports merchants who want to:

- Present products and subscription plans digitally.
- Make pricing information easier to understand.
- Acquire customers through shareable links.
- Support product launches and promotional campaigns.
- Reduce manual price communication.
- Connect product discovery with payment or subscription registration.
- Improve conversion from customer interest to payment.

## 3. Where Pricing Table Fits in FlexiBill

Pricing Table is one of the customer acquisition interfaces in the broader FlexiBill ecosystem.

| Component | Responsibility |
|---|---|
| Collection | Organises the billing programme |
| Plan | Defines the merchant offering |
| Pricing | Defines commercial and billing rules |
| Pricing Table | Presents the offering to customers |
| Member Center | Supports membership and customer registration workflows |
| Payment journey | Enables the configured payment process |
| Billing engine | Supports subsequent billing according to configuration |

The exact customer journey depends on the merchant's selected configuration and enabled capabilities.

## 4. Merchant Use Cases

| Industry | Example |
|---|---|
| Fitness | Compare monthly and annual gym plans |
| Education | Present tuition packages |
| Insurance | Present premium packages |
| SaaS | Compare Starter, Business, and Enterprise plans |
| Retail | Promote VIP membership |
| Travel | Offer annual travel membership |
| Professional services | Present monthly service packages |

## 5. Pricing Table Design Principles

A good Pricing Table should answer five customer questions:

1. What am I buying?
2. What benefits do I receive?
3. How much do I pay?
4. How frequently will I be charged?
5. What happens after I register or pay?

Recommended information architecture:

- Merchant identity and product name.
- Plan name.
- Plan description.
- Key benefits.
- Price and currency.
- Billing frequency.
- Applicable promotional information.
- Terms and conditions.
- Clear customer action.

Avoid presenting too many plans in a single table. Make the recommended plan easy to identify without hiding important conditions.

## 6. Merchant Configuration Workflow

Use this sequence as the implementation guide:

1. Confirm the Collection exists.
2. Confirm the relevant Plan has been configured.
3. Validate pricing and billing frequency.
4. Identify which Plans should be presented to customers.
5. Access Pricing Table management.
6. Create or configure the relevant Pricing Table.
7. Select the appropriate offering and presentation settings.
8. Review the displayed product and pricing information.
9. Validate the customer registration and payment journey.
10. Publish or share the configured Pricing Table through the supported channel.
11. Test the complete journey before distributing the link.

**UI validation:** Confirm the current dashboard navigation, available settings, mandatory fields, publication method, and supported plan associations with the latest product documentation.

## 7. Customer Acquisition Channels

Pricing Table links can form part of a merchant's digital acquisition strategy.

| Channel | Example |
|---|---|
| Website | Subscription page |
| Social media | Instagram or Facebook profile |
| WhatsApp | Sales representative shares a plan link |
| Email | Membership campaign |
| Digital advertising | Campaign landing destination |
| Merchant app | Embedded or linked offering |
| QR code | Printed promotion or physical store |

Channel availability and embedding options must be validated individually. A shareable URL does not automatically mean that every channel supports a native integration.

## 8. Example: Fitness Membership

A gym offers three membership packages.

| Plan | Price | Billing |
|---|---:|---|
| Basic | Rp250,000 | Monthly |
| Premium | Rp500,000 | Monthly |
| Annual | Rp3,000,000 | Annually |

Recommended customer-facing presentation:

**Basic**
- Gym access under standard membership conditions.
- Monthly payment.

**Premium**
- Enhanced membership benefits.
- Monthly payment.

**Annual**
- Annual membership arrangement.
- One annual billing period, subject to the configured payment rules.

Customer journey:

1. Customer receives the Pricing Table link.
2. Customer reviews the available plans.
3. Customer selects a preferred offering.
4. Customer proceeds through the configured registration process.
5. Customer completes the required payment or authorization.
6. The resulting membership and billing relationship follows the enabled FlexiBill workflow.

## 9. Pricing Table and Member Center

Pricing Table and Member Center serve different purposes.

| Pricing Table | Member Center |
|---|---|
| Presents merchant offerings | Supports customer membership functions |
| Helps customers choose a Plan | Supports membership identification and related workflows |
| Supports acquisition | Supports the customer relationship |
| Commercial presentation | Membership and customer management |

A merchant may use both as parts of a broader subscription acquisition journey.

Important: Do not assume that every Pricing Table flow automatically invokes every Member Center function. Validate the exact integration and registration sequence.

## 10. Pricing Table and Billing Portal

Pricing Table is primarily associated with presenting and acquiring an offering.

Billing Portal is intended for customer billing and subscription self-service workflows.

| Customer requirement | Relevant interface |
|---|---|
| Discover a merchant's Plans | Pricing Table |
| Compare available prices | Pricing Table |
| Start a subscription | Configured acquisition journey |
| Access billing information | Billing Portal, where enabled |
| Manage subscription | Billing Portal, where supported |
| Review payment-related information | Relevant customer billing/payment interface |

## 11. Campaign and Promotion Use Cases

Pricing Table can be incorporated into merchant campaigns, subject to supported discount and pricing functionality.

Examples:

**New customer campaign**
- Promote a new subscription offering.
- Share the Pricing Table through digital channels.

**Annual subscription campaign**
- Present annual and monthly alternatives.
- Explain the commercial difference clearly.

**Membership acquisition**
- Promote different membership tiers.
- Direct customers to the appropriate registration journey.

**Seasonal campaign**
- Communicate a promotional offering.
- Validate coupon eligibility, validity, and calculation before publication.

## 12. Conversion Measurement

Recommended funnel:

Impression → Pricing Table Visit → Plan Selection → Registration → Payment Authorization → Successful First Payment → Active Subscription

Recommended KPIs:

| KPI | Definition |
|---|---|
| Table visits | Number of visits to the Pricing Table |
| Plan selection rate | Plan selections / visits |
| Registration conversion | Completed registrations / plan selections |
| Payment conversion | Successful first payments / payment attempts |
| Acquisition conversion | New paid subscribers / visits |
| Average ticket | Average successful payment amount |
| Plan mix | Subscriber distribution by Plan |
| Campaign conversion | Paid subscribers attributed to a campaign |

These are recommended measurement definitions. Confirm which events and reports are natively available and which require merchant-side analytics.

## 13. Risks and Validation Checklist

| Risk | Control |
|---|---|
| Incorrect displayed price | Reconcile with Plan configuration |
| Incorrect billing frequency | Validate the Plan settings |
| Outdated promotion | Confirm campaign validity |
| Broken customer journey | Test the complete registration and payment flow |
| Incorrect membership creation | Validate Member Center integration |
| Unsupported channel assumption | Test channel-specific behaviour |
| Inconsistent customer terms | Review published descriptions and terms |
| Country availability difference | Validate Indonesia and Malaysia separately |

## 14. Country Scope: Indonesia and Malaysia

| Area | Validation requirement |
|---|---|
| Pricing Table availability | Confirm in each country |
| Supported Plan types | Confirm country-specific behaviour |
| Payment methods | Validate available channels |
| Member Center integration | Confirm enabled workflow |
| Coupons and tax | Validate applicable configuration |
| WhatsApp experience | Do not assume a native seller-facing UI is available |
| Digital Catalog integration | Do not assume native Subscription integration |
| API | Confirm current API support and limitations |

**Important product boundary:** PayChat's documented bulk-upload billing integration should not be interpreted as confirmation of a complete WhatsApp-based Pricing Table seller experience. Digital Catalog integration with Subscription/Pricing Table must also be validated separately.

## 15. Go-Live Checklist

- [ ] Collection is correctly configured.
- [ ] Plan and pricing are approved.
- [ ] Pricing Table content is accurate.
- [ ] Currency and billing frequency are correct.
- [ ] Customer registration journey is tested.
- [ ] Payment journey is tested.
- [ ] Membership outcome is verified.
- [ ] Applicable promotion and terms are validated.
- [ ] Country-specific availability is confirmed.
- [ ] Campaign links and QR codes are tested.

## 16. Related Playbooks

1. [Collection Management](01-collection-management.md)
2. [Plan & Pricing Configuration](02-plan-and-pricing-configuration.md)
3. [Member Center](04-member-center.md)
4. [Billing Portal](05-billing-portal.md)
5. [Subscription Lifecycle](07-subscription-lifecycle.md)
6. [Payment Management](08-payment-management.md)

## 17. Document Governance

- Document: Pricing Table
- Product: DOKU FlexiBill
- Category: Product Configuration
- Country scope: Indonesia and Malaysia
- Status: Working playbook — product behaviour and country validation required
- Owner: FlexiBill Product
- Last reviewed: 9 November 2026

---

*Internal DOKU knowledge base. Refer to approved product and technical documentation before merchant implementation.*
