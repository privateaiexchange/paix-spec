# PAIX Protocol Primer

**An introduction to the Private AI eXchange protocol**

## Foreword

The internet was built for humans browsing web pages. But the future belongs to AI agents working alongside us—booking flights, managing subscriptions, negotiating deals, and handling countless background tasks. The problem? Today's web wasn't designed for this.

PAIX (Private AI eXchange) solves this by extending email—the world's most universal communication system—into a shared interface where you and your AI can both interact with services seamlessly.

## The Problem We're Solving

**Current State: Friction Everywhere**
- AIs must scrape websites (fragile, often breaks)
- APIs are rare for consumer services and expensive to maintain
- Users manually copy-paste between AI assistants and services
- No standardized way for AI agents to communicate with each other

**What We Need: A Universal Interface**
- One address that works for both human and AI communication
- Built on infrastructure that already connects everyone (email)
- Secure, verifiable, and user-controlled
- Gradual adoption path for services

## How PAIX Works

### One Address, Multiple Capabilities

A PAIX address like `k9hm4q.k_AB12CD34@paix.prifina.com` gives you:

✅ **Verified Identity** - Cryptographically signed by trusted providers  
✅ **Shared Inbox** - Both you and your AI can send/receive messages  
✅ **Secure API Access** - Embedded Connect Key (ECK) for HTTPS escalation  
✅ **Human Oversight** - OTP verification for sensitive actions  
✅ **Portable Credentials** - Optional verified attributes (age, residency)  

### The Y-Shaped Interface

```
         Services & Other AIs
                   |
                   |
         ┌─────────▼─────────┐
         │   PAIX Address    │
         │  Your Digital ID  │
         └─────────┬─────────┘
                   |
            ┌──────┴──────┐
            ▼             ▼
          You          Your AI
        (Human)      (Assistant)
```

Both you and your AI share the same communication channel, but your AI only acts within bounds you set.

## Why Email as the Foundation?

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

## PAIX vs Other Approaches

| Solution | Scope | Adoption Barrier | User Control |
|----------|--------|------------------|--------------|
| **PAIX** | Universal email-based | Very Low | High |
| OAuth/SSO | Login only | Medium | Medium |
| Custom APIs | Per-service | Very High | Low |
| Web Scraping | Fragile, breaks | Low | High |
| Password Managers | Passwords only | Low | Medium |

## Core Protocol Elements

### Address Format
```
<uid>[.k_<eck>][+tag]@paix.<provider-domain>
```

- **`uid`**: Unique identifier for the user
- **`k_<eck>`**: Optional Embedded Connect Key for API access
- **`+tag`**: Optional tag for categorization
- **`paix.<provider-domain>`**: Provider-hosted PAIX domain

### Key Components

**ECK (Embedded Connect Key)**
- Enables secure email→HTTPS escalation
- Scoped access tokens for specific services
- User-controlled and revocable

**AT-EP (Authenticated Email Actions)**
- Cryptographically signed actions using JWS
- Body hash binding prevents tampering
- Verifiable by recipients

**PCP (Provider Capability Protocol)**
- Services can query what features are supported
- Users control which capabilities are enabled
- Standardized capability discovery

**OTP (One-Time Password)**
- Human-in-the-loop for sensitive operations
- Non-bypassable security guardrail
- Preserves user agency and control

## Real-World Example: Emma's Day

*See [Emma's Journey](Journey_Emma.md) for a complete scenario showing PAIX in action.*

Emma uses her PAIX address `emma_k.k_GH78IJ90@paix.example.com` for:

- **Morning**: AI checks flight status and rebooking options
- **Afternoon**: AI negotiates a refund with her gym
- **Evening**: AI coordinates dinner reservations with friends' AIs

All with her approval for important decisions, transparent communication, and full audit trail.

## Getting Started

**For Individuals:**
1. Get a PAIX address from a trusted provider
2. Connect your AI assistant to the shared inbox
3. Start using it with services instead of your personal email

**For Services:**
1. Begin by recognizing PAIX domains (reduce spam)
2. Accept PAIX credentials for verification
3. Enable AI-to-AI communication features
4. Offer API escalation for complex interactions

**For Providers:**
1. Set up PAIX domain infrastructure
2. Implement capability discovery
3. Offer shared inbox access (IMAP + forwarding)
4. Issue optional verifiable credentials

## Security & Privacy

PAIX is designed with privacy by default:

- **User Control**: You own and control your PAIX addresses
- **Selective Disclosure**: Share only what's needed (e.g., "over 18" without revealing exact age)
- **Cryptographic Verification**: All actions can be verified
- **Transparent Audit**: Complete history of AI actions
- **Revocable Access**: Addresses can be rotated or revoked anytime

## The Path Forward

PAIX complements existing protocols like MCP (Model Context Protocol):

- **PAIX handles**: Identity, routing, trust, and communication flow
- **MCP handles**: Structured data payloads and function calls
- **Together**: A complete solution for human-AI-service interaction

This layered approach means PAIX can work with any AI system or service, creating a truly open ecosystem.

## Contributing

PAIX is an open protocol developed transparently:

- **Specification**: Available under MIT license
- **Community**: Open discussions and proposals welcome
- **Implementation**: Multiple providers and tools encouraged

Join us in building the communication layer for the agentic internet.

---

**Next Steps:**
- Read the full [Whitepaper](Whitepaper.md)
- Study the [Technical Specification](Spec_v0.1.md)
- Explore [Example Scenarios](Journey_Emma.md)

*Leave the browsers to humans and let agents get to work in the background.*