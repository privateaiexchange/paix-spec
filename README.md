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

- **Primer**: [/docs/Primer_Cover.md](docs/Primer_Cover.md)  
- **Whitepaper**: [/docs/Whitepaper.md](docs/Whitepaper.md)  
- **Spec v0.1 (draft)**: [/docs/Spec_v0.1.md](docs/Spec_v0.1.md)  
- **Examples**: [/examples/emails](examples/emails) and [/docs/Journey_Emma.md](docs/Journey_Emma.md)

## Who's behind PAIX?

Created by **Valto Loikkanen** & **Tero Ahola** with the Prifina team. MIT-licensed open standard. We invite contributions and open discussion.

## Contribute & discuss

- **Read**: [CONTRIBUTING.md](CONTRIBUTING.md), [GOVERNANCE.md](GOVERNANCE.md), [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)  
- **Open an Issue** (spec/doc/extension) or start a **Discussion** (Announcements, Q&A, Proposals, Show & Tell)

---

**Tagline:** *Leave the browsers to humans and let agents get to work in the background.*