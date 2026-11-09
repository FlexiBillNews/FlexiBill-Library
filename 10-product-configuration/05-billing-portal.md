# 05 — Billing Portal

## 1. Overview

Billing Portal is the customer-facing interface for accessing billing-related information and supported self-service functions within the FlexiBill ecosystem.

It helps merchants provide customers with a more transparent and convenient billing experience without requiring every interaction to be handled manually by merchant support teams.

**Strategic role:**

Billing Portal connects the merchant's billing operations with the customer's ongoing billing relationship.

Typical ecosystem:

**Merchant → Collection → Plan → Member → Billing Portal → Billing → Payment**

The actual customer experience depends on the portal configuration, merchant integration, and enabled product capabilities.

## 2. Business Objectives

Billing Portal can support merchants in:

- Giving customers access to billing information.
- Improving transparency around payment obligations.
- Reducing manual billing enquiries.
- Supporting subscription self-service.
- Improving customer retention through easier account management.
- Reducing operational workload.
- Providing a consistent digital billing experience.

## 3. Customer Experience: What Should the Portal Solve?

A customer should be able to understand five things:

1. What subscription or service do I have?
2. How much do I need to pay?
3. When is my next payment due?
4. What is the status of my billing and payment?
5. What actions can I take if my circumstances change?

The portal should make the customer's billing relationship understandable, accessible, and actionable.

## 4. Core Customer Journey

A typical customer journey:

1. Customer receives a merchant communication or portal access link.
2. Customer opens the Billing Portal.
3. Customer completes the required authentication or identification.
4. Customer accesses the relevant billing information.
5. Customer reviews outstanding or previous billing information.
6. Customer takes an available action.
7. The merchant's billing system processes the resulting request or payment.
8. Customer receives the relevant confirmation.

Exact authentication, access, and action flows must be validated against the current product implementation.

## 5. Customer-Facing Capability Areas

The following table distinguishes desired customer outcomes from functionality that must be validated.

| Capability area | Customer need | Validation |
|---|---|---|
| Billing overview | Understand billing status | Confirm current portal display |
| Invoice information | Review amount and due date | Confirm available invoice fields |
| Payment status | Check whether payment succeeded | Confirm status synchronisation |
| Payment method | Manage funding source | Validate supported methods |
| Subscription information | Understand current Plan | Confirm available details |
| Subscription changes | Change subscription | Validate available actions |
| Cancellation | Request cancellation | Confirm supported workflow |
| Billing history | Review past transactions | Validate history availability |
| Support information | Find assistance | Confirm merchant configuration |

Do not present every capability above as currently released or enabled.

## 6. Subscription Self-Service Vision

A mature subscription Billing Portal should progressively support the following customer actions.

### 6.1 Plan Upgrade

Customer moves from a lower-value Plan to a higher-value Plan.

Example:

Basic Membership → Premium Membership.

Questions to validate:
- When does the new Plan become effective?
- Is there a price difference?
- Is proration supported?
- Does the customer need to authorise a new payment?

### 6.2 Plan Downgrade

Customer moves from a higher-value Plan to a lower-value Plan.

Example:

Premium Membership → Basic Membership.

Questions to validate:
- Does the downgrade apply immediately or at renewal?
- How are existing entitlements handled?
- Is any price adjustment required?

### 6.3 Cancellation

Customer requests to stop a subscription.

Important distinctions:
- Cancellation request.
- Cancellation effective date.
- Final billing event.
- Service access termination.

These should not be treated as one identical event.

### 6.4 Pause and Resume

Customer temporarily suspends and later resumes a subscription.

Questions to validate:
- Is pause supported natively?
- Can the merchant define pause duration?
- What happens to the next billing date?
- Does resumption require customer action?

**Product boundary:** Upgrade, downgrade, proration, pause, resume, and cancellation are capability areas to validate individually. A desired customer journey is not proof that every action is currently available in the portal.

## 7. Payment Management Experience

A customer may need to manage how future billing is paid.

Potential customer requirements:

- View the current payment arrangement.
- Update a payment method.
- Replace an expired card.
- Add another funding source.
- Understand a failed payment.
- Retry or complete an outstanding payment.

The actual availability depends on the supported payment method, merchant configuration, and integration.

### Payment Experience Example

A customer has a monthly subscription of Rp500,000.

1. The customer receives a notification that payment failed.
2. The customer accesses the Billing Portal.
3. The customer reviews the outstanding billing.
4. The customer follows the available payment recovery action.
5. The payment result is reflected in the billing relationship.

Validate whether payment recovery is initiated through the portal, a payment link, merchant support, or another enabled channel.

## 8. Billing Portal and Pricing Table

These two interfaces serve different customer needs.

| Pricing Table | Billing Portal |
|---|---|
| Product discovery | Existing customer relationship |
| Plan comparison | Billing information |
| Subscription acquisition | Billing self-service |
| Commercial presentation | Ongoing account experience |

Example:

A prospective customer discovers a gym's Premium Plan through Pricing Table.

After registration, the customer uses the available Billing Portal journey to access billing information.

## 9. Billing Portal and Member Center

| Member Center | Billing Portal |
|---|---|
| Customer membership information | Customer-facing billing interface |
| Member identification | Billing self-service |
| Membership relationship | Billing and subscription information |
| Merchant membership operations | Customer account experience |

A customer may have a membership record and a billing relationship. The portal should present the relevant information consistently, subject to the available integration.

## 10. Merchant Configuration Workflow

Use this implementation sequence:

1. Confirm the Collection and Plan configuration.
2. Confirm the relevant customer or Member Center setup.
3. Identify the required customer self-service functions.
4. Review the available Billing Portal configuration.
5. Configure the supported access and customer journey.
6. Confirm which billing and payment information is displayed.
7. Validate available customer actions.
8. Test authentication and access controls.
9. Test billing status and payment status synchronisation.
10. Complete customer acceptance testing.
11. Publish or enable the portal according to the approved implementation process.

**UI validation requirement:** Confirm exact dashboard navigation, available configuration fields, portal URL generation, branding options, and customer access method against the current product version.

## 11. Example: Education Subscription

**Scenario:** A school collects monthly tuition from parents.

| Item | Example |
|---|---|
| Collection | Student Tuition |
| Plan | Monthly Tuition |
| Billing frequency | Monthly |
| Customer | Parent / Guardian |
| Billing amount | Rp1,500,000 |
| Payment | Configured payment method |

Illustrative customer experience:

1. Parent receives access to the billing experience.
2. Parent reviews the student's billing information.
3. Parent checks the due date and outstanding amount.
4. Parent completes payment through the supported payment journey.
5. Parent checks the resulting payment status.

Merchant benefits:
- Less manual billing communication.
- Better visibility for parents.
- More structured payment follow-up.
- Improved customer experience.

## 12. Example: Insurance Premium Billing

**Scenario:** An insurance company collects recurring premiums.

The portal should ideally help policyholders understand:

- Relevant billing amount.
- Premium due date.
- Payment status.
- Outstanding premium information.
- Available payment options.
- Appropriate support channels.

A successful payment experience can reduce customer confusion and unnecessary service enquiries.

Insurance-specific policy information and actions must be validated separately from standard subscription functionality.

## 13. Notifications and Customer Communication

Billing Portal should be considered together with the merchant's communication strategy.

Potential communication events:

| Event | Communication objective |
|---|---|
| Upcoming billing | Remind customer of an upcoming charge |
| Invoice issued | Notify customer of a new billing |
| Payment successful | Confirm completed payment |
| Payment failed | Explain unsuccessful payment |
| Overdue billing | Remind customer of outstanding obligations |
| Subscription change | Confirm requested changes |
| Cancellation | Confirm cancellation status |

Channels may include email, SMS, WhatsApp, or other merchant communication channels, subject to supported integrations.

Do not assume that every communication channel is natively connected to Billing Portal.

## 14. Security and Access Considerations

Customer-facing billing information must be protected.

Recommended controls:

- Authenticate customers appropriately.
- Avoid exposing billing records through predictable public identifiers.
- Validate customer-to-account ownership.
- Protect personal and payment-related information.
- Apply appropriate access permissions.
- Use secure communication channels.
- Maintain appropriate audit records.
- Validate session and access expiry behaviour.
- Follow applicable Indonesia and Malaysia privacy requirements.

Security controls must be
