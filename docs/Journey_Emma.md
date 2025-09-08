# Living with PAIX: Emma's Journey

**A scenario-based, standalone introduction to PAIX**

---

## Cover & Credits

**Protocol:** PAIX — Private AI eXchange, an open standard that upgrades email into a shared universal interface for individuals and their personal AIs.

**Creators:** Valto Loikkanen & Tero Ahola, with the Prifina team and input from industry experts.

**Demo provider domain used in this document:** paix.prifina.com

**License:** MIT (open standard, open for community contributions).

---

## Executive Summary

This document tells a single, concrete story: how one person—Emma in Helsinki—adopts PAIX and shifts routine online work into the background where her personal AI can safely help. The journey starts with email that works everywhere today and evolves, without breaking anything, toward structured AI-to-AI interactions where both services and personal AIs act responsibly under user control. 

PAIX does not replace email; it makes email more useful. Every service already supports PAIX at the baseline, because every service already uses email. The only thing that changes is the level of support a service chooses to provide and the features a user enables for a given address.

---

## PAIX in Brief

PAIX is a simple but powerful open standard that treats email as a shared universal interface for a person and their personal AI. A single PAIX address can be just email on day one; later, the same address can also serve as a login, a verified communication channel, a scoped API key, and an AI interface—without requiring the user or the service to adopt new infrastructure all at once. The protocol aligns with how the web already works and adds structured, verifiable affordances over time.

### Canonical PAIX address format

```
<uid>[.k_<eck>]@paix.<provider-domain>
```

- `uid` is a short, privacy-preserving identifier, unique per service
- Optional `.k_<eck>` is an Embedded Connect Key (ECK), a compact, scoped token that lets the email workflow escalate to secure HTTPS calls when supported
- **Example used in this narrative:** `k9hm4q.k_AB12CD34@paix.prifina.com`

The address never needs to reveal the service name. In user interfaces, the service name appears only as a label; the address itself stays neutral to preserve privacy and prevent cross-tracking.

---

## PAIX Address Management

PAIX addresses are managed through provider applications that handle address creation, delivery preferences, and feature controls. These are the only addresses Emma shares with services. Her existing "real" email addresses (e.g., Gmail) are kept private and used only as forwarding targets.

For each PAIX address, Emma can choose its delivery model. She may enable a shared IMAP mailbox so both she and her personal AI read and act from the same PAIX inbox; she may also enable forwarding to one of her verified real emails for convenience. She can change these preferences at any time.

PAIX reflects a clear trust model: providers decide which capabilities they technically support (e.g., OTP login, signed actions, verified attributes, the AI interface). Users then decide, per address, which of those supported features to enable. Services can discover what's supported and enabled for a given address by sending a standard capability query via email and can act accordingly.

---

## Chapter 1 — Persona and Setup

Emma is 32 and lives in Helsinki. She adopts PAIX because she wants her personal AI to handle routine online chores—sign-ups, renewals, address updates, receipts—while leaving sensitive actions under her explicit control. 

During onboarding she learns the basic model: PAIX addresses are for the outside world; her real email is private and used only as a forwarding destination. She creates her first PAIX address, `p8t2ka.k_3PZ9Q4F7G2@paix.prifina.com`, adds `emma@gmail.com` as a verified forwarding address, and turns both delivery modes on: shared IMAP (so her AI can help) and forwarding (so copies land in Gmail). 

From this moment, her PAIX management interface becomes her "case of cards"; each address can be offered to a different service, and each carries clear settings and guardrails.

---

## Chapter 2 — First Contact with a Service

One evening Emma visits a newspaper website. Her browser extension recognizes she's on a domain that doesn't yet have a PAIX address. It offers to create one. With a tap, her provider issues a new PAIX address, `k9hm4q.k_AB12CD34@paix.prifina.com`. The site treats it as a normal email address. In her management interface, Emma labels the address "Newspaper.com" and sees it listed as Guest. Later, when she subscribes, she changes the status to Customer. 

Nothing breaks if the newspaper knows nothing about PAIX; it's still just email.

---

## Chapter 3 — The Service Evolves

Weeks pass. The newspaper adopts PAIX features. Emma receives a human-readable message: "We now support PAIX: you can update your details without logging in, manage your subscription, and allow your AI to assist you under your approval." 

Her PAIX management interface shows a banner on the newspaper's service page inviting Emma to review features. She sees the provider's supported capabilities and toggles on the AI interface for routine actions while keeping OTP required for payments and plan changes. Behind the scenes, the service can discover what Emma has enabled by sending a PAIX capability query email to her address; from then on, the service knows exactly what it can rely on.

---

## Chapter 4 — Background Help, Human in the Loop

A renewal reminder arrives in Emma's PAIX inbox. Because shared IMAP is on, her AI reads the message and asks a simple question: "Renew at €10/month, cancel, or negotiate?" Emma chooses to negotiate. The AI sends a signed action over email (using PAIX's signed-action envelope). The newspaper replies with a better price. Emma approves with a one-time code. The action completes at the new rate. 

Her PAIX interface keeps a clear, auditable record: what came in, what the AI proposed, what Emma approved, and what went out.

---

## Chapter 5 — AI-Initiated Relationships

On Saturday, Emma asks her AI to find a good, free cooking newsletter and subscribe. The AI discovers a candidate and issues a new PAIX address, `u3df7n.k_XY7LMN90@paix.prifina.com`. For this address the AI turns shared IMAP ON (so it can summarize issues) and forwarding OFF (so Emma's Gmail stays uncluttered). 

The new address appears in her management interface under Recently Added with a note "Created by AI." Emma reviews and approves it as Guest. Every weekly issue now lands in the shared IMAP inbox; the AI writes a short summary, and Emma reads only the highlights.

---

## Chapter 6 — Two AIs, One Plan

Emma's friend Alex also uses PAIX. Their AIs swap a couple of structured emails to settle on a dinner date. Emma's scheduling address is `u7fw9s.k_SCHED123@paix.prifina.com`; Alex's is `a9zk5x.k_SCHED456@paix.prifina.com`. Neither address reveals a service name; both are labeled in their respective management interfaces for clarity. 

The AIs propose times, confirm a booking, and notify their owners. No human needed until it matters—if a deposit were required, the system would prompt Emma for a one-time code.

---

## Chapter 7 — Daily Life at Scale

Over the next months Emma accumulates PAIX addresses for many relationships:
- `x2jl9m.k_QWERT123@paix.prifina.com` for the gym
- `p8kq7d.k_HG56JK89@paix.prifina.com` for electricity  
- `m9s7hy.k_8D3K2P9Q@paix.prifina.com` for streaming

The addresses are labeled in her management interface, but the addresses themselves remain neutral. Her AI cancels subscriptions she no longer uses, updates her address in multiple places when she moves, pulls receipts for bookkeeping, and answers "contact us" emails with structured, signed actions where supported. 

Emma only sees what matters: brief summaries and the occasional request to approve a sensitive step with an OTP. If she changes her mind about delivery, she can switch an address from forwarding to shared IMAP (or vice versa). If an address leaks or she wants to retire it, she can rotate its ECK or delete the address entirely. If she ever wants more ownership, she can move providers or bring her own domain; PAIX is an open standard, not a silo.

---

## Trust, Safety, and Roles

Throughout Emma's journey, three rules are visible in the interface and reinforced by the protocol. 

**First**, everything always works as plain email; nothing breaks if a service stays at the baseline. 

**Second**, the provider advertises capabilities, but the user enables them per address; services never have to guess because they can query capabilities when needed. 

**Third**, sensitive actions require Emma's explicit approval; the AI is bounded by design and cannot bypass the one-time code for important operations.

PAIX was designed to match how people, services, and providers already operate, and to let each party move at their own pace. Services that never expose APIs can still support structured actions by email. Small organizations with only a "contact us" address become reachable by AIs without scraping browsers. Individuals gain privacy and leverage without sacrificing control. Providers anchor trust without creating a new central gatekeeper.

---

## Example Artifacts

### Capability query (service → PAIX address)

```
To: k9hm4q.k_AB12CD34@paix.prifina.com
Subject: PAIX-CAPABILITIES ?
X-PAIX-Query: capabilities
X-PAIX-From-Origin: https://newspaper.com
```

### Provider response (application/paix+json)

```json
{
  "address": "k9hm4q.k_AB12CD34@paix.prifina.com",
  "provider": "prifina.com",
  "features_supported": [
    "email_verified","otp_login","eck_escalation","signed_actions",
    "ai_interface","vc_age_over_18","vc_residency_eu","vc_identity_confirmed"
  ],
  "features_enabled": [
    "email_verified","otp_login","eck_escalation","signed_actions","ai_interface"
  ],
  "twin_endpoint": "https://twin.emma.ai/inbox",
  "jwks": "https://twin.emma.ai/.well-known/jwks.json",
  "policy": {"human_in_loop": true, "otp_required_for_sensitive": true},
  "ttl_seconds": 3600
}
```

### Signed action (Emma's AI → service)

```
Subject: ACTION UpdateAddress
X-PAIX-Preamble: v1 eyJhbGciOiJFZERTQSIsInR5cCI6IkpXVCJ9...<sig>
X-PAIX-BodyHash: sha256:8d0fb6b1e1...

{
  "account_id": "12345",
  "new_address": "Example St 1, 00100 Helsinki, FI",
  "effective_date": "2025-09-05"
}
```

### Service upgrade notice (human-readable)

```
Subject: We now support PAIX for your account

We can now communicate with your PAIX address directly. With your 
permission, your AI can update account details, manage your 
subscription, and handle routine support. Sensitive actions always 
require your confirmation (one-time code).
```

---

## Conclusion

Emma's experience demonstrates PAIX's core idea: start with email that works everywhere, then grow into structured, verifiable, AI-ready interactions—without forcing anyone to rebuild their world. The protocol aligns with the grain of the internet, lets each side adopt at its own pace, and preserves human control where it matters most. 

**Leave the browsers to humans and let agents get to work in the background.**

---

## Related Resources

- [PAIX Whitepaper](Whitepaper.md) - Complete protocol overview
- [Technical Specification](Spec_v0.1.md) - Implementation details
- [Developer Quickstart](Developer_Quickstart.md) - Integration guide
- [Security & Privacy](Security_Privacy.md) - Security considerations