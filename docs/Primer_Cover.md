# PAIX Primer — Cover

**PAIX (Private AI eXchange)**  
*A simple but powerful open standard protocol for the agentic internet.*

## Foreword

The true benefit of AI isn't watching it click screens. Scalability comes when agents work in the background—async, parallel, API-like. MCP gives agents an API interface, but not a universal channel. PAIX upgrades the channel we all share—**email**—into a **shared, structured interface** for individuals, services, and their AIs. Email already operates at global scale.

**Leave the browsers to humans and let agents get to work in the background.**

## About

- **License:** MIT  
- **Creators:** Valto Loikkanen & Tero Ahola, with the Prifina team  
- **Philosophy:** Simplicity, backwards compatibility, user control  
- **Contribute:** Open Issues/Discussions; PRs welcome

## The Golden Model

One address can be: **ID + verified email + login (OTP) + comms + API key (ECK) + AI interface** (+ optional verifiable credentials). Sensitive actions always require human approval.

## Address Format

```
<uid>[.k_<eck>][+tag]@paix.<provider-domain>
```

- `uid` unique per service; privacy-preserving  
- optional `.k_<eck>` Embedded Connect Key  
- optional `+tag` for user/routing

## Core Elements

- **ECK:** email→HTTPS escalation with scoped, short-lived capabilities  
- **AT-EP:** signed email actions (JWS + canonical body hash)  
- **PCP:** capability query to learn supported/enabled features  
- **OTP:** non-bypassable human-in-loop for sensitive actions  
- **Delivery:** shared IMAP and/or forwarding to a verified real email  
- **Providers:** advertise capabilities; users enable per Keycard

## Why Email as Foundation

**Universal Reach**
- Every service already has "contact@" email addresses
- 4+ billion people use email daily
- Works across all platforms and devices

**Battle-Tested Security**
- SPF, DKIM, DMARC provide strong authentication
- Decades of spam filtering and security improvements
- Well-understood by developers and security teams

**Gradual Adoption**
- Services can start by simply receiving PAIX emails
- No need to build new APIs or change existing systems
- Progressive enhancement as adoption grows

## Adoption Path

- **Day 0:** email works everywhere
- **Gradual:** signed actions, ECK, capability queries
- **Always reversible:** rotate/disable per address; bring your own domain

## Security & Privacy (overview)

- DKIM/SPF/DMARC hygiene; JWS signatures; nonce; exp/nbf; replay cache
- Selective disclosure (attributes without underlying PII)
- Append-only audit (user-visible)

## Extensibility

Optional prefix namespace (e.g., `vc-`) reserved for future patterns. Core spec remains minimal; registry governs prefixes by consensus.

## Ecosystem Roles

Individuals, services, providers (mail + policy + capabilities), toolmakers (extensions, SDKs), and governance.

## What PAIX Is Not

- A new content or context format
- An attempt to replace APIs
- A hard dependency on any specific infrastructure or AI system

Instead, **PAIX complements existing protocols and standards** — like using MCP inside a PAIX email message to define the payload, while PAIX handles identity, routing, access, and trust.

## Getting Started

**For Individuals:**
- Get a PAIX address from a trusted provider
- Connect your AI assistant to the shared inbox
- Start using it with services instead of your personal email

**For Services:**
- Begin by recognizing PAIX domains (reduce spam)
- Accept PAIX credentials for verification
- Enable AI-to-AI communication features
- Offer API escalation for complex interactions

**For Providers:**
- Set up PAIX domain infrastructure
- Implement capability discovery
- Offer shared inbox access (IMAP + forwarding)
- Issue optional verifiable credentials

## Next Steps

- Read the full [Whitepaper](Whitepaper.md)
- Study the [Technical Specification](Spec_v0.1.md)
- Explore [Example Scenarios](Journey_Emma.md)
- See [Developer Quickstart](Developer_Quickstart.md)

---

*Examples and scenario: see [/examples](../examples) and [/docs/Journey_Emma.md](Journey_Emma.md)*