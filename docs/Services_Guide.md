# PAIX for Services

**A Shared Smart Email Protocol for Your Customers and Their AIs**

---

## What is PAIX?

PAIX makes email smarter and shared — between a customer and their personal AI.

- Every service already uses email. It's how you sign users up, send notifications, confirm identities, and close accounts
- There are 4.6 billion people using email globally, across 7.9 billion addresses

👉 **PAIX doesn't replace email. It upgrades it into a shared universal interface — used by both the customer and their AI, on their side.**

## Why it matters for services

The internet wasn't built for your customers' AIs.

- **APIs are expensive to build**, inconsistent, and not available for every feature
- **Browsers are designed for humans**, not agents

PAIX fixes this by letting you use the same email channel you already rely on — but now shared with your customers' AIs.

- Always works as plain email
- Smarter when you recognize PAIX addresses
- Lets your service communicate with the customer and their AI through a single, shared channel

## The Golden Model

A PAIX address looks like this:
```
u7fw9s.k_3PZ9Q4F7G2@paix.provider.com
```

For you as a service, this single address can serve as:

- **Unique ID** (no cross-tracking issues)
- **Verified email** (not a fake signup)
- **Passwordless login credential** (works with OTP/magic links)
- **Shared inbox** (customer + AI receive it together)
- **Scoped API key** (embedded connect key for structured automation)
- **AI interface** (so your service AI can talk directly with theirs)
- **Optional verified credentials** (age, residency, or "identity confirmed," without exposing raw data)

👉 **At minimum, it's just an email address. At maximum, it's a complete customer channel: ID + login + comms + automation + verification, in one.**

## What you can do with PAIX

### 1. Customer ↔ Service

- Customers use PAIX addresses instead of personal emails
- **Cleaner onboarding:** fewer fakes, fewer dead accounts
- You treat it as email — no new infra needed

### 2. Customer AI ↔ Service

- If a customer has a PAIX address, you can assume they also have a personal AI
- Your service can automate directly with their AI: update details, confirm renewals, send receipts, or notify of changes
- Their AI can handle routine requests without your support team

### 3. Service AI ↔ Customer AI

Your AI and the customer's AI can connect directly through PAIX.

**Examples:**
- Request updated payment or billing info
- Confirm address changes
- Proactively notify of new features or contract terms
- Verify KYC attributes without exposing raw data

**Result:** Faster, cheaper, and less error-prone than human email or UI support.

### 4. Providers & Features

- Each PAIX address comes from a provider
- Providers decide which features are technically supported (verified credentials, API key, AI interface)
- Users decide per-address which of those features to enable when they share a PAIX email with your service
- You can query an address in a standard way (via a special-format email) to learn what features are available and active for that address
- This ensures transparency: you know exactly what you can rely on, without guessing or storing unnecessary data

## Business Benefits

### Reduced Support Costs
- AI-to-AI communication handles routine requests
- Fewer human support tickets
- Automated account updates and confirmations

### Improved Data Quality
- Verified email addresses reduce fake signups
- Provider authentication guarantees real users
- Cleaner customer database

### Enhanced Customer Experience
- Faster response times through AI automation
- Proactive notifications and updates
- Seamless account management

### Future-Proof Infrastructure
- Built on email standards you already use
- Gradual adoption with no breaking changes
- AI-ready from day one

## Why this is safe

- **Always works as email** → zero breakage, zero risk in trying
- **Customer remains in control** → AI only acts within their rules
- **Human-in-the-loop** → critical actions always need user confirmation
- **You choose the level of support** → from treating it as plain email, to enabling structured AI-to-AI automation
- **Provider trust** → you can decide which providers you recognize, ensuring messages come from reliable sources

## Adoption path

### Level 0: Do Nothing
**Effort:** Zero  
**Benefit:** PAIX addresses work like regular email

Your existing email infrastructure handles PAIX addresses automatically.

### Level 1: Recognition
**Effort:** 5 minutes  
**Benefit:** Reduce fake signups, improve data quality

```python
def is_paix_address(email):
    return email.count('@') == 1 and '@paix.' in email

if is_paix_address(customer_email):
    # Apply premium routing or verification
    handle_verified_customer(customer_email)
```

### Level 2: Capability Discovery
**Effort:** 30 minutes  
**Benefit:** Know what features are available

Send a capability query email to discover what the customer's PAIX address supports.

### Level 3: Automation
**Effort:** 2-4 hours  
**Benefit:** Enable AI-to-AI communication

Process structured action requests from customer AIs with appropriate security measures.

### Level 4: Full Integration
**Effort:** Days  
**Benefit:** Complete AI-service collaboration

Enable bi-directional AI communication with escalation to secure APIs when needed.

## Implementation Examples

### E-commerce Platform
```python
def handle_order_update(customer_paix_address, order_id, status):
    if supports_ai_interface(customer_paix_address):
        # Send structured update to customer's AI
        send_structured_notification(customer_paix_address, {
            "type": "order_update",
            "order_id": order_id,
            "status": status,
            "tracking_url": get_tracking_url(order_id)
        })
    else:
        # Fall back to regular email
        send_regular_email_notification(customer_paix_address, order_id, status)
```

> **💡 Complete Example**: See [E-commerce Integration](https://github.com/privateaiexchange/paix-examples/tree/main/integrations/ecommerce) for a full implementation.

### SaaS Application
```python
def process_subscription_change(customer_paix_address, new_plan):
    if requires_user_confirmation(new_plan):
        # Send OTP challenge
        send_otp_challenge(customer_paix_address, {
            "action": "upgrade_subscription",
            "new_plan": new_plan,
            "price_change": calculate_price_change(new_plan)
        })
    else:
        # Process automatically
        update_subscription(customer_paix_address, new_plan)
```

> **💡 Complete Example**: See [SaaS Platform Integration](https://github.com/privateaiexchange/paix-examples/tree/main/integrations/saas) for production patterns.

### Customer Support
```python
def handle_support_request(customer_paix_address, request):
    if can_automate_response(request):
        # Let AIs handle common requests
        send_ai_response(customer_paix_address, generate_response(request))
    else:
        # Route to human agent with PAIX context
        route_to_human_support(customer_paix_address, request, paix_context=True)
```

> **💡 Complete Example**: See [Customer Support Integration](https://github.com/privateaiexchange/paix-examples/tree/main/integrations/support) for AI-human handoff patterns.

## Security Considerations

### Authentication
- Verify PAIX signatures for structured actions
- Check provider trust status
- Validate embedded connect keys (ECK)

### Authorization
- Respect user-defined AI permissions
- Require OTP for sensitive operations
- Maintain audit trails

### Privacy
- Handle verified credentials properly
- Don't store unnecessary customer data
- Respect selective disclosure preferences

> **💡 Security Guide**: See [Security Implementation Examples](https://github.com/privateaiexchange/paix-examples/tree/main/security) for production-ready patterns.

## Getting Started

1. **Start Simple:** Recognize PAIX addresses in your existing email flow
2. **Add Discovery:** Query PAIX capabilities to understand available features
3. **Enable Automation:** Process structured AI requests with proper security
4. **Scale Gradually:** Expand PAIX support based on customer adoption

## Implementation Resources

### Quick Start
- **[Developer Quickstart](Developer_Quickstart.md)** - Technical integration guide with code examples
- **[Address Validation](https://github.com/privateaiexchange/paix-examples/tree/main/tools/address-parser)** - Production-ready parsers
- **[Capability Discovery](https://github.com/privateaiexchange/paix-examples/tree/main/tools/capability-client)** - Query implementation patterns

### Platform Examples
- **[E-commerce Platforms](https://github.com/privateaiexchange/paix-examples/tree/main/integrations/ecommerce)** - Order management, returns, support
- **[SaaS Applications](https://github.com/privateaiexchange/paix-examples/tree/main/integrations/saas)** - Subscription management, feature access
- **[Customer Support](https://github.com/privateaiexchange/paix-examples/tree/main/integrations/support)** - AI-human collaboration patterns
- **[Email Providers](https://github.com/privateaiexchange/paix-examples/tree/main/integrations/email-providers)** - Provider implementation examples

### Security & Best Practices
- **[Security Guide](Security_Privacy.md)** - Comprehensive security model
- **[Signature Verification](https://github.com/privateaiexchange/paix-examples/tree/main/security/signature-verify)** - Production verification patterns
- **[OTP Handling](https://github.com/privateaiexchange/paix-examples/tree/main/security/otp-handlers)** - Human-in-the-loop implementations
- **[Rate Limiting](https://github.com/privateaiexchange/paix-examples/tree/main/security/rate-limiting)** - API protection patterns

### Business Case
- **[Value Stack](PAIX_Value_Stack.md)** - Executive summary and ROI analysis
- **[Real-World Scenario](Journey_Emma.md)** - See PAIX in action through Emma's journey
- **[Comparison Analysis](Comparison_Appendix.md)** - PAIX vs alternatives

## Community & Support

### Community Examples
- **[Community Contributions](https://github.com/privateaiexchange/paix-examples/tree/main/community)** - Real-world implementations from users
- **[Integration Showcases](https://github.com/privateaiexchange/paix-examples/tree/main/showcases)** - Featured implementations

### Get Help
- **[GitHub Discussions](https://github.com/privateaiexchange/paix-spec/discussions)** - Community Q&A and ideas
- **[Technical Issues](https://github.com/privateaiexchange/paix-spec/issues)** - Bug reports and feature requests
- **[Contributing Guide](../CONTRIBUTING.md)** - How to contribute back to the ecosystem

### Share Your Implementation
Have you built a PAIX integration? We'd love to feature it:
- **[Submit Your Example](https://github.com/privateaiexchange/paix-examples/tree/main/community)** - Share with the community
- **[Case Study Program](https://github.com/privateaiexchange/paix-spec/discussions/categories/show-and-tell)** - Tell your success story

## In short

PAIX is a shared smart email protocol for your customers and their AIs.

- **Every service already supports it.** Only the level of support varies
- **Works as email today,** and as structured AI-to-AI comms tomorrow
- **Reduces fraud,** cuts support costs, and improves customer experience
- **Open, gradual, and safe:** you adopt at your own pace

**With PAIX, you're not just emailing a customer — you're connected to both the customer and their AI, through one shared universal interface.**

---

## 🧭 Navigation

**Getting Started**: [Primer](Primer_Cover.md) → [Whitepaper](Whitepaper.md) → [Developer Quickstart](Developer_Quickstart.md)

**By Role**:
- **End Users**: [Individuals Guide](Individuals_Guide.md)
- **Developers**: [Developer Quickstart](Developer_Quickstart.md) | [Examples Repo](https://github.com/privateaiexchange/paix-examples)
- **Providers**: [Providers Guide](Providers_Guide.md)

**Technical**: [Specification](Spec_v0.1.md) | [Security](Security_Privacy.md) | [Extensibility](Extensibility_Registry.md)

---

*Ready to upgrade your customer communication? Start by recognizing PAIX addresses and grow from there.*