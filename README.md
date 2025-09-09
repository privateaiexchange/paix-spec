# PAIX — Private AI eXchange

*An open email protocol that turns your inbox into a shared universal interface for you (or your org) and your AI to interact with services.*

## Why PAIX?

Browsers are for humans. Agents scale when they act in the background—async, parallel, and verifiable. Email already connects everyone (people, services, and even small orgs with only "contact@"). PAIX upgrades email so one address can be: **ID, verified email, login (OTP), comms, API key (ECK), and AI interface**—with human approval for sensitive actions.

## Address format (spec-correct):

```
<uid>[.k_<eck>][+tag]@paix.<provider-domain>
```

## Core elements

- **ECK** — Embedded Connect Key for secure email→HTTPS escalation
- **AT-EP** — Signed email actions (JWS + body hash binding)
- **PCP** — Capability query so services see what's supported & enabled
- **OTP guardrail** — Human-in-loop for sensitive actions (non-bypassable)
- **Delivery** — Shared IMAP (owner + AI) and/or forwarding to a verified real email
- **Providers** — Advertise capabilities; users enable per Keycard
- **Extensibility** — Optional prefix namespace for future consensus patterns

## Start here

### Quick Introduction
- **Primer**: [/docs/Primer_Cover.md](docs/Primer_Cover.md) — Fast introduction to PAIX
- **Whitepaper**: [/docs/Whitepaper.md](docs/Whitepaper.md) — Complete protocol overview
- **Real-world scenario**: [/docs/Journey_Emma.md](docs/Journey_Emma.md) — See PAIX in action

### By Your Role
- **Developers**: [Developer Quickstart](docs/Developer_Quickstart.md) → [Examples & SDKs](https://github.com/privateaiexchange/paix-examples)
- **Services**: [Services Guide](docs/Services_Guide.md) — Business benefits and integration
- **Providers**: [Providers Guide](docs/Providers_Guide.md) — Email provider implementation
- **End Users**: [Individuals Guide](docs/Individuals_Guide.md) — How to get and use PAIX

### Technical Reference
- **Spec v0.1 (draft)**: [/docs/Spec_v0.1.md](docs/Spec_v0.1.md) — Complete technical specification
- **Address examples**: [/examples/addresses.md](examples/addresses.md) — Validation and parsing
- **Email examples**: [/examples/emails](examples/emails) — Message format samples

## Related Repositories

- **[paix-examples](https://github.com/privateaiexchange/paix-examples)** — SDK libraries, integration examples, and reference implementations
- **[Organization Overview](https://github.com/privateaiexchange)** — Complete PAIX ecosystem and community information

## Who's behind PAIX?

Created by **Valto Loikkanen** & **Tero Ahola** with the Prifina team. MIT-licensed open standard. We invite contributions and open discussion.

## Contribute & discuss

- **Read**: [CONTRIBUTING.md](CONTRIBUTING.md), [GOVERNANCE.md](GOVERNANCE.md)  
- **Open an Issue** (spec/doc/extension) or start a **Discussion** (Announcements, Q&A, Proposals, Show & Tell)
- **Build Examples**: Contribute to [paix-examples](https://github.com/privateaiexchange/paix-examples) with SDKs and integrations

---

**Tagline:** *Leave the browsers to humans and let agents get to work in the background.*