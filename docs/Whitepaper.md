# PAIX — Private AI eXchange (Whitepaper)

**A Simple but Powerful (Email) Protocol for the Agentic Internet**

---

## Executive Summary

The internet was not designed for personal AIs to act on your behalf. Today, when an AI tries to interact with services, it either:

- **Scrapes browsers** → fragile, error-prone, duplicative of human work
- **Uses APIs** → rare in consumer services, costly to build and maintain, inconsistent across providers

Neither path scales. Both consume massive resources, invite errors and attacks, and fail to prepare services or individuals for the age of agentic AI.

**PAIX is a simple but very powerful open standard protocol that turns standard email into a Private AI eXchange** — a shared universal interface for individuals, their personal AIs, services, and providers.

- It builds on email, the universal channel every service already supports
- It works as "just email" when nothing else is supported
- It enables gradual adoption: individuals, services, and providers can progress independently
- It bridges today's infrastructure with tomorrow's AI-to-AI agentic internet

## Why Email?

**Scale** → There are ~4.6 billion email users globally (56% of humanity), managing ~7.9 billion email accounts. Each user averages almost 2 accounts. This makes email the largest open digital identity system in the world.

**Ubiquity** → Every online service already uses email — to sign up, verify, update, and notify.

**Persistence** → Email is often the first credential in a service relationship, and usually the last that remains after accounts close.

**Resilience** → Unlike proprietary APIs or apps, email is an open standard, universally interoperable, and not controlled by any one platform.

👉 **For many smaller services, email will remain the only channel they ever use.**

👉 **With PAIX, email is no longer just a notification tool — it becomes the universal interface for individuals and their AIs.**

## The PAIX Solution

PAIX redefines email as an open standard protocol for the agentic internet:

- **Universal** → works anywhere email works
- **Gradual adoption** → individuals, services, and providers can progress independently
- **Agent-ready** → designed so personal AIs can act within user-defined boundaries
- **Shared interface** → a universal channel between service ↔ individual ↔ personal AI ↔ peer AIs, anchored by providers

## The Golden Model

**Example:**
```
u7fw9s.k_3PZ9Q4F7G2@paix.provider.com
```

**One PAIX address =**

- **Unique Identifier** → per user + per service, no cross-tracking
- **Verified Email** → provider guarantees authenticity (not fake)
- **Passwordless login** → works with OTP/magic link flows
- **Shared Communication** → inbox accessible to both user and AI
- **API key** → embedded connect key (ECK) for structured interactions
- **AI interface** → bootstrap to secure API connections with user's AI twin
- **Optional Verifiable Credentials** → provider can attest "verified adult," residency, or identity confirmed without revealing raw data

👉 **At minimum, it's just email. At maximum, it's ID + login + comms + API key + AI interface + credentials — all in one.**

## The Four Dimensions of PAIX

### 1. Individual ↔ Service

- Start now by using a PAIX address instead of personal email
- Services treat it like any other email, gaining cleaner onboarding and fewer fakes
- Users and their AIs gain shared communication and easier logins

### 2. Service AI ↔ Personal AI

- If a customer has a PAIX address, the service can assume an AI twin exists
- Enables automation: subscription updates, billing, address confirmation, proactive notifications
- Reduces cost and error while improving experience

### 3. Personal AI ↔ Personal AI (Peer-to-Peer)

- Two individuals' AIs can communicate directly
- Schedule meetings, coordinate tasks, exchange knowledge, or negotiate — with both owners in control
- Creates a social fabric for AIs: just like people once exchanged emails or messenger invites, AIs can now "friend" each other safely

### 4. Providers ↔ Ecosystem

- Providers decide which features are technically supported (verified credentials, API key, AI interface)
- Users decide per-address which features to enable when sharing a PAIX email with a service
- Services can query an address in a standard way (via special-format email) to check what's available and active
- Providers anchor trust by signing messages, enforcing hygiene, and exposing supported capabilities

## Adoption Path

1. **Do nothing** → PAIX works as plain email
2. **Recognize PAIX** → detect domains, reduce fakes
3. **Use verified attributes** → "verified adult" without storing raw data
4. **Enable automation** → AI-to-AI structured communication
5. **Escalate to APIs** → embedded keys enable secure, scoped HTTPS connections when ready

## Trust & Control

- **Always works as email** → no breakage, no lock-in
- **User-controlled** → rotate, revoke, or move addresses anytime
- **Service-controlled** → decide which providers to trust
- **Provider-anchored** → verification and features are offered by providers
- **Human-in-the-loop** → critical actions always confirmed by the owner

## Technical Architecture

### Address Format
```
<uid>[.k_<eck>][+tag]@paix.<provider-domain>
```

- `uid` is a short, privacy-preserving identifier, unique per service
- Optional `.k_<eck>` is an Embedded Connect Key (ECK), a compact, scoped token
- Optional `+tag` for user/routing preferences

### Core Components

**ECK (Embedded Connect Key)**
- Email→HTTPS escalation with scoped, short-lived capabilities
- Enables secure API access when email isn't sufficient

**AT-EP (Authenticated Email Actions)**
- Signed email actions (JWS + canonical body hash)
- Cryptographic verification of AI-initiated actions

**PCP (Provider Capability Protocol)**
- Capability query to learn supported/enabled features
- Standard way for services to discover PAIX capabilities

**OTP (One-Time Password)**
- Non-bypassable human-in-loop for sensitive actions
- Preserves user agency and oversight

**Delivery Models**
- Shared IMAP (owner + AI) and/or forwarding to verified real email
- User controls per-address delivery preferences

## Security & Privacy

**Built on Email Standards**
- DKIM/SPF/DMARC hygiene; JWS signatures; nonce; exp/nbf; replay cache
- Leverages decades of email security evolution

**Privacy by Design**
- Selective disclosure (attributes without underlying PII)
- No service names in addresses to prevent cross-tracking
- User-controlled feature enablement

**Audit Trail**
- Append-only audit (user-visible)
- Complete transparency of AI actions
- Human oversight for sensitive operations

## Extensibility Framework

Optional prefix namespace (e.g., `vc-`) reserved for future patterns:
- Core spec remains minimal
- Registry governs prefixes by consensus
- Backwards compatibility guaranteed

**Example Extensions:**
- `vc-` for verifiable credentials
- `pgp-` for OpenPGP integration
- `org-` for organizational addresses

## Ecosystem Roles

**Individuals** → Control their PAIX addresses and AI permissions

**Services** → Choose level of PAIX support to offer

**Providers** → Issue addresses, anchor trust, enable capabilities

**Toolmakers** → Build extensions, SDKs, and integrations

**Governance** → Community-driven protocol evolution

## Comparison with Alternatives

| Solution | Universal | User Control | Service Effort | AI-Ready |
|----------|-----------|--------------|----------------|----------|
| **PAIX** | ✅ Email-based | ✅ Full control | ✅ Gradual | ✅ Built-in |
| Big Tech SSO | ❌ Platform lock-in | ❌ Limited | ✅ Easy | ❌ Not designed |
| Custom APIs | ❌ Per-service | ❌ Service-controlled | ❌ High cost | ⚠️ Possible |
| Web Scraping | ✅ Universal | ✅ User-driven | ✅ No change | ❌ Fragile |

## Implementation Status

- **PAIX is live** — first provider: [Prifina](https://www.prifina.com)
- **Reference application:** Passcase (manages PAIX addresses)
- **Open specification** available for implementation
- **Community contributions** welcomed

## Conclusion

PAIX is a simple but powerful open standard protocol that turns email into a Private AI eXchange.

- **Every service already supports it** — only the level of support varies
- **It empowers individuals**, improves services, and enables providers
- **It bridges today's email infrastructure** with tomorrow's agentic AI world
- **It's open, gradual, universal, and user-owned**
- **It works today** — with Prifina as the first provider — and scales naturally into the future

**PAIX is the on-ramp to the agentic internet — starting with the 4.6 billion people who already use email.**

---

## References

- [PAIX Technical Specification](Spec_v0.1.md)
- [Emma's Journey: Real-world Scenario](Journey_Emma.md)
- [Developer Quickstart Guide](Developer_Quickstart.md)
- [Security & Privacy Considerations](Security_Privacy.md)

**License:** MIT  
**Created by:** Valto Loikkanen & Tero Ahola, with the Prifina team  
**Status:** v0.1 Draft