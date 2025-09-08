# PAIX for Providers

**A Shared Smart Email Protocol Anchored in Trust**

---

## What is PAIX?

PAIX turns email into a shared universal interface — used by both an individual and their personal AI, on their side.

- Every service already supports email
- Every individual already uses it
- What's missing is trust and structure

👉 **This is where providers come in.**

Providers issue and host PAIX addresses, anchoring verification, security, and advanced features that make the shared interface reliable for individuals, services, and AIs.

## Why it matters for providers

Email is already the largest open identity system in the world:

- **4.6 billion users**
- **7.9 billion addresses**
- **1.8 accounts per person on average**

But email was never designed for:

- Verified credentials (age, residency, identity confirmed)
- AI-to-AI structured communication
- Scoped automation and backchannel APIs

**Providers extend email into PAIX, making it a trustworthy foundation for the agentic internet.**

## The Provider Role

As a PAIX provider, you:

### Issue PAIX addresses under your domain
```
u7fw9s.k_3PZ9Q4F7G2@paix.provider.com
```

### Anchor trust
- Sign and validate messages
- Enforce SPF/DKIM/DMARC hygiene
- Provide cryptographic verification
- Maintain revocation lists

### Offer verified credentials
- "Verified adult," residency, or identity confirmed without exposing raw data
- Selective disclosure capabilities
- Zero-knowledge proofs where applicable
- KYC-as-a-service functionality

### Bridge shared access

Providers ensure PAIX emails are accessible to both the individual and their AI twin — without breaking normal email use.

**Delivery models:**
- **Forwarding copy** → PAIX email is forwarded to the user's existing inbox
- **Shared inbox** → both user and AI access the same inbox, with labeling/routing to separate human- vs AI-handled mail

**Boundaries:**
- The user sets permissions on what their AI may act on
- Sensitive actions (e.g. logins, payments, subscriptions) always require explicit user confirmation (OTP or similar)
- The AI can help, but never override the human

**Feature scope:**
- The provider decides what features are supported (e.g. verified credentials, API key use, AI interface)
- The user decides per-address which features to enable when sharing a PAIX address with a service
- Services can query an address in a standard way (via special-format email) to learn which features are supported and active for that address

### Expose capabilities
- Publish what features are available for PAIX addresses you issue
- Interoperability ensures services can adapt dynamically
- Standard capability discovery protocol

### Enable portability
- Users can switch providers or bring their own domain for absolute control
- Migration tools and data export
- No vendor lock-in by design

## Technical Infrastructure Requirements

### Domain Setup
- Configure `paix.<your-domain>` subdomain
- Implement proper MX records
- Set up SPF, DKIM, and DMARC records
- Provide HTTPS endpoint for capability queries

### Mail System Integration
```
paix.provider.com
├── MX records pointing to mail servers
├── SPF record allowing mail servers
├── DKIM keys for message signing
├── DMARC policy (recommend reject/quarantine)
└── HTTPS endpoint at /.well-known/paix
```

### Cryptographic Infrastructure
- JWKS endpoint for public key distribution
- Key rotation procedures and schedules
- Revocation list management
- Secure key storage (HSM recommended)

### Capability Discovery
Implement PCP (Provider Capability Protocol) endpoint:

```json
{
  "paix_version": "0.1",
  "supported_features": [
    "email_verified",
    "otp_login", 
    "eck_escalation",
    "signed_actions",
    "ai_interface",
    "vc_age_over_18",
    "vc_residency_verified"
  ],
  "provider_info": {
    "name": "Your Provider Name",
    "paix_endpoint": "https://api.provider.com/paix",
    "documentation": "https://docs.provider.com/paix"
  }
}
```

## The Four Dimensions (Provider view)

### 1. Individual ↔ Service
- Providers guarantee the email is authentic (not fake)
- Make onboarding cleaner for services
- Reduce fraud and improve trust

### 2. Service AI ↔ Personal AI
- Providers enable structured handshakes so both sides can trust messages
- Reduce fraud and miscommunication
- Facilitate automated workflows

### 3. Personal AI ↔ Personal AI
- Providers ensure peer-to-peer AI comms happen under safe rules
- Verification and rate-limiting reduce abuse
- Enable social fabric for AI agents

### 4. Providers ↔ Ecosystem
- Providers publish trust signals for others
- Services can whitelist which providers they accept
- Inter-provider interoperability ensures global reach

## Security Responsibilities

### Message Authentication
- Implement DKIM signing for all outbound messages
- Verify SPF and DMARC for inbound messages
- Maintain strict email hygiene standards

### Key Management
- Secure generation and storage of signing keys
- Regular key rotation (recommended annually)
- Revocation list publication and maintenance
- Hardware security module (HSM) usage recommended

### User Authentication
- Strong user verification procedures
- Multi-factor authentication options
- Secure credential recovery processes

### AI Boundary Enforcement
- Ensure OTP requirements cannot be bypassed
- Implement rate limiting for AI actions
- Audit trail maintenance
- Suspicious activity detection

## Privacy & Compliance

### Data Minimization
- Collect only necessary user information
- Implement data retention policies
- Provide user data export capabilities
- Enable account deletion and cleanup

### Selective Disclosure
- Support verifiable credentials without raw data exposure
- Zero-knowledge proof capabilities
- Attribute-based verification (age, residency, etc.)
- User consent management

### Regulatory Compliance
- GDPR compliance for EU users
- CCPA compliance for California users
- Other regional privacy regulations
- Regular compliance audits

## Business Models

### For Email Providers
- Premium PAIX features as add-on service
- Enhanced verification services
- AI integration capabilities
- Enterprise PAIX solutions

### For Identity Providers
- Verified credential issuance
- KYC-as-a-service offerings
- Compliance verification services
- Trust anchor positioning

### For AI Platforms
- Native PAIX integration with AI assistants
- Hosted AI twin services
- Advanced automation features
- Developer tools and APIs

### For Enterprises
- Internal PAIX deployment
- Employee identity management
- Organizational address spaces
- Integration with existing systems

## Why this is safe

- **Users stay in control** → they choose or switch providers anytime
- **Services stay in control** → they decide which providers to trust
- **AI stays bounded** → scoped keys and human confirmation on critical actions
- **Providers act as anchors** → no central authority, but distributed trust

## Why it's valuable for providers

### New Offerings
- Become the issuer of verified PAIX addresses
- Trusted identity provider in agentic ecosystem
- Premium verification services

### New Revenue Streams
- Charge for premium credentials (e.g. verified adult, KYC-as-a-service)
- Subscription models for enhanced features
- Enterprise licensing and support

### Strategic Positioning
- Anchor trust in the agentic internet, just as CAs (certificate authorities) anchored HTTPS
- First-mover advantage in AI-email integration
- Platform for future identity innovations

### Immediate Adoption
- Every service already supports email, so providers add value from day one
- No chicken-and-egg adoption problem
- Build on existing email infrastructure

## Implementation Guide

### Phase 1: Basic Infrastructure
1. Set up paix subdomain and mail routing
2. Implement basic PAIX address issuance
3. Configure email authentication (SPF/DKIM/DMARC)
4. Create capability discovery endpoint

### Phase 2: Enhanced Features
1. Add verified credential capabilities
2. Implement shared inbox access (IMAP)
3. Deploy forwarding mechanisms
4. Create user management interface

### Phase 3: AI Integration
1. Add AI twin endpoint support
2. Implement signed action verification
3. Deploy OTP enforcement mechanisms
4. Create developer tools and SDKs

### Phase 4: Ecosystem Integration
1. Partner with other providers for interoperability
2. Integrate with major email clients
3. Support bring-your-own-domain options
4. Develop enterprise solutions

## Support & Resources

### Technical Documentation
- [PAIX Specification](Spec_v0.1.md)
- [Security Guidelines](Security_Privacy.md)
- [Developer Tools](Developer_Quickstart.md)

### Reference Implementation
- Open source provider reference code (planned)
- Configuration examples and templates
- Testing and validation tools

### Community
- Provider working group participation
- Standards development collaboration
- Best practices sharing

## Getting Started

1. **Review Requirements:** Study the technical specification and security guidelines
2. **Plan Infrastructure:** Design your PAIX domain and mail system integration
3. **Implement Core Features:** Start with basic address issuance and capability discovery
4. **Add Value-Added Services:** Implement verification, credentials, and AI features
5. **Join Ecosystem:** Collaborate with other providers and services for interoperability

## In short

PAIX is a shared smart email protocol anchored by providers.

- **Providers make it trustworthy**
- **Providers add optional verified credentials**
- **Providers bridge individuals, their AIs, and services into one safe, shared channel**
- **Providers can be anyone** — email hosts, AI platforms, enterprises, even governments
- **Users can even own their own domain** for absolute control

**Providers are the trust anchors that turn email into the universal interface for the agentic internet.**

---

*Ready to become a PAIX provider? Start with the technical specification and join our provider community.*