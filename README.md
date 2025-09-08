# PAIX — Private AI eXchange

**An open email protocol that turns your inbox into a shared universal interface for you and your AI to interact with services.**

## Why PAIX?

Browsers are for humans. AIs scale when they act in the background—async, parallel, and verifiable. Email already connects everyone (people, services, and small orgs with only "contact@"). PAIX upgrades email so one address can be: ID, verified email, login (OTP), comms, API key (ECK), and AI interface—with human approval for sensitive actions.

## What's in v0.1 (draft)

**Address format:**
```
<uid>[.k_<eck>][+tag]@paix.<provider-domain>
```

**Core elements:**

* **ECK**: Embedded Connect Key for secure email→HTTPS escalation
* **AT-EP**: Signed email actions (JWS + body hash binding)
* **PCP**: Capability query so services see what's supported & enabled
* **OTP guardrail**: Human-in-loop for sensitive actions (non-bypassable)
* **Delivery**: Shared IMAP (owner + AI) and/or forwarding to a verified real email
* **Providers**: Advertise capabilities; users enable per Keycard
* **Extensibility**: Optional prefix namespace for future consensus patterns

## Start here

* Read the [Primer](/docs/Primer_Cover.md) and [Whitepaper](/docs/Whitepaper.md)
* See the [Spec v0.1](/docs/Spec_v0.1.md)
* Try the [Examples](/examples/emails/)
* Explore [Emma's Journey](/docs/Journey_Emma.md) to see PAIX in daily life

## Who's behind PAIX?

Created by Valto Loikkanen & Tero Ahola with the Prifina team. MIT-licensed open standard. We invite contributions and open discussion.

## Contribute & discuss

* Open a proposal in [Issues](https://github.com/privateaiexchange/paix-spec/issues) or start a thread in [Discussions](https://github.com/privateaiexchange/paix-spec/discussions)
* See [CONTRIBUTING.md](CONTRIBUTING.md), [GOVERNANCE.md](GOVERNANCE.md), and the [Extensibility Registry](/docs/Extensibility_Registry.md)

---

**Tagline: Leave the browsers to humans and let agents get to work in the background.**