# PAIX Protocol Specification v0.1 (Draft)

**Private AI eXchange - Technical Specification**

---

## Abstract

PAIX (Private AI eXchange) is an open protocol that extends email to create a shared communication interface between individuals, their AI assistants, and services. This specification defines the technical components that enable secure, verifiable, and user-controlled AI-to-service interactions using existing email infrastructure.

## 1. Introduction

### 1.1 Purpose

PAIX addresses the fundamental challenge of AI agents interacting with services in a scalable, secure, and user-controlled manner. Rather than relying on fragile web scraping or expensive API development, PAIX leverages email's universal reach and established security mechanisms.

### 1.2 Design Goals

- **Universal Compatibility**: Works with existing email infrastructure
- **User Control**: Individuals maintain ownership and oversight of AI actions
- **Security**: Built on proven email authentication methods
- **Gradual Adoption**: Services can participate with minimal changes
- **Extensibility**: Framework for future protocol enhancements

### 1.3 Protocol Overview

PAIX consists of four core components:
1. **Address Format**: Structured email addresses with embedded capabilities
2. **ECK (Embedded Connect Key)**: Secure email-to-HTTPS escalation
3. **AT-EP (Authenticated Email Actions)**: Cryptographically signed actions
4. **PCP (Provider Capability Protocol)**: Service capability discovery

## 2. Address Format

### 2.1 Specification

```
<uid>[.k_<eck>][+tag]@paix.<provider-domain>
```

**Components:**
- `uid`: Unique identifier (6-16 alphanumeric characters)
- `k_<eck>`: Optional Embedded Connect Key (8-32 characters)
- `+tag`: Optional categorization tag
- `paix.<provider-domain>`: Provider-hosted PAIX domain

### 2.2 Examples

**Valid addresses:**
```
k9hm4q@paix.example.com                    # Basic address
k9hm4q.k_AB12CD34@paix.example.com         # With ECK
k9hm4q+billing@paix.example.com            # With tag
k9hm4q.k_AB12CD34+travel@paix.example.com  # Full format
```

**Invalid addresses:**
```
k9hm4q@example.com           # Missing 'paix.' subdomain
k9hm4q.AB12CD34@paix.com     # Missing 'k_' ECK prefix
short@paix.example.com       # UID too short (min 6 chars)
```

### 2.3 Validation Rules

**UID Requirements:**
- Length: 6-16 characters
- Characters: alphanumeric (a-z, A-Z, 0-9) and underscore
- Must not start with number
- Case-insensitive for routing

**ECK Requirements:**
- Length: 8-32 characters after 'k_' prefix
- Characters: alphanumeric and basic punctuation
- Base64url encoding recommended
- Must be URL-safe

**Tag Requirements:**
- Length: 1-32 characters after '+' prefix
- Characters: alphanumeric, hyphen, underscore
- Used for categorization and routing

## 3. Embedded Connect Key (ECK)

### 3.1 Purpose

ECK enables secure escalation from email communication to HTTPS API access, providing scoped authorization for AI agents to interact with services.

### 3.2 Generation

```javascript
// Pseudocode for ECK generation
function generateECK(userContext, serviceScope) {
  const payload = {
    sub: userContext.uid,
    aud: serviceScope.domain,
    iat: currentTimestamp(),
    exp: currentTimestamp() + validity_period,
    scope: serviceScope.permissions
  };
  
  return base64url.encode(
    crypto.sign(payload, userContext.privateKey, 'ES256')
  );
}
```

### 3.3 Usage Flow

1. **Email Authentication**: Service receives PAIX email with ECK
2. **ECK Extraction**: Service extracts ECK from address
3. **HTTPS Escalation**: Service uses ECK to establish secure API session
4. **Scoped Access**: AI performs authorized actions within defined scope

### 3.4 Security Properties

- **Time-limited**: ECKs have defined expiration periods
- **Scope-limited**: Permissions are explicitly defined
- **Revocable**: Users can revoke ECKs at any time
- **Auditable**: All ECK usage is logged

## 4. Authenticated Email Actions (AT-EP)

### 4.1 Purpose

AT-EP provides cryptographic verification of AI-initiated actions, ensuring integrity and non-repudiation of automated operations.

### 4.2 Message Format

```
Subject: PAIX-Action: <action-type>
From: k9hm4q.k_AB12CD34@paix.example.com
To: service@example.com
Date: Mon, 9 Sep 2025 12:00:00 +0000
PAIX-Version: 0.1
PAIX-Action-ID: act_1234567890abcdef
PAIX-Signature: eyJ0eXAiOiJKV1MiLCJhbGciOiJFUzI1NiJ9...

{
  "action": "update_subscription",
  "parameters": {
    "plan": "premium",
    "billing_cycle": "annual"
  },
  "timestamp": "2025-09-09T12:00:00Z",
  "nonce": "rand_abc123def456"
}
```

### 4.3 Signature Generation

```javascript
// AT-EP signature process
function generateATEPSignature(messageBody, privateKey) {
  const bodyHash = sha256(messageBody);
  const header = {
    alg: 'ES256',
    typ: 'JWS'
  };
  
  const payload = {
    body_hash: bodyHash,
    iat: currentTimestamp(),
    iss: senderAddress
  };
  
  return jws.sign({
    header: header,
    payload: payload,
    secret: privateKey
  });
}
```

### 4.4 Verification Process

1. **Extract Signature**: Parse PAIX-Signature header
2. **Verify JWS**: Validate signature using sender's public key
3. **Check Body Hash**: Ensure message body hasn't been tampered with
4. **Validate Timestamp**: Ensure message is within acceptable time window
5. **Check Nonce**: Prevent replay attacks

## 5. Provider Capability Protocol (PCP)

### 5.1 Purpose

PCP enables services to discover and advertise PAIX capabilities, allowing for dynamic feature negotiation and capability-aware interactions.

### 5.2 Capability Query

**Request Email:**
```
Subject: PAIX-Query: capabilities
From: k9hm4q@paix.example.com
To: support@service.example.com
PAIX-Version: 0.1
PAIX-Query-Type: capabilities

{
  "query": "capabilities",
  "supported_versions": ["0.1"],
  "requested_features": ["billing", "notifications", "api_escalation"]
}
```

**Response Format:**
```json
{
  "paix_version": "0.1",
  "supported_features": {
    "billing": {
      "actions": ["view_invoices", "update_payment", "cancel_subscription"],
      "escalation": true,
      "otp_required": ["cancel_subscription"]
    },
    "notifications": {
      "actions": ["subscribe", "unsubscribe", "preferences"],
      "escalation": false,
      "otp_required": []
    }
  },
  "provider_info": {
    "name": "Example Service",
    "paix_endpoint": "https://api.service.example.com/paix",
    "documentation": "https://docs.service.example.com/paix"
  }
}
```

### 5.3 Well-Known Endpoint

Services SHOULD publish capability information at:
```
https://service.example.com/.well-known/paix
```

## 6. One-Time Password (OTP) Requirements

### 6.1 Purpose

OTP provides human-in-the-loop verification for sensitive operations, ensuring user oversight of critical AI actions.

### 6.2 OTP-Required Actions

Services MUST require OTP for actions that:
- Involve financial transactions
- Change security settings
- Delete user data
- Access sensitive personal information
- Modify legal agreements

### 6.3 OTP Flow

1. **Action Initiation**: AI sends AT-EP signed action request
2. **OTP Challenge**: Service responds with OTP challenge
3. **User Verification**: User receives and enters OTP
4. **Action Completion**: Service processes verified action

### 6.4 OTP Message Format

```
Subject: PAIX-OTP Required: <action-description>
From: service@example.com
To: k9hm4q@paix.example.com
PAIX-Version: 0.1
PAIX-OTP-Challenge: true

Your AI assistant is requesting to: Cancel Premium Subscription

To approve this action, reply with:
OTP: [6-digit code sent to your verified phone]

This request expires in 10 minutes.
Action ID: act_1234567890abcdef
```

## 7. Provider Requirements

### 7.1 Domain Setup

Providers MUST:
- Configure `paix.<provider-domain>` subdomain
- Implement proper MX records
- Configure SPF, DKIM, and DMARC records
- Provide HTTPS endpoint for capability queries

### 7.2 Shared Access Models

**IMAP Shared Access:**
- Both user and AI access same mailbox
- Separate IMAP credentials for AI
- Read/write permissions for both parties

**Forwarding Model:**
- PAIX address forwards to user's real email
- AI receives copy through separate channel
- User maintains primary control

### 7.3 Security Obligations

Providers MUST:
- Implement proper email authentication
- Maintain audit logs of all actions
- Provide user controls for AI permissions
- Support ECK revocation
- Ensure secure key storage

## 8. Security Considerations

### 8.1 Threat Model

**Addressed Threats:**
- Message tampering (AT-EP signatures)
- Replay attacks (timestamps and nonces)
- Unauthorized AI actions (OTP requirements)
- Impersonation (email authentication)

**Ongoing Risks:**
- Provider compromise
- Private key theft
- Social engineering
- DNS hijacking

### 8.2 Cryptographic Requirements

**Digital Signatures:**
- ECDSA with P-256 curve (ES256)
- RSA with PSS padding (PS256) as alternative
- Minimum 2048-bit RSA keys

**Hashing:**
- SHA-256 for all hash operations
- HMAC-SHA256 for MAC operations

### 8.3 Key Management

**Provider Keys:**
- Regular key rotation (recommended: annually)
- Secure hardware storage preferred
- Public key distribution via DNS/HTTPS

**User Keys:**
- Generated by trusted providers
- Backup and recovery mechanisms
- Revocation and replacement procedures

## 9. Privacy Considerations

### 9.1 Data Minimization

PAIX implementations SHOULD:
- Collect minimal necessary information
- Use selective disclosure for credentials
- Implement data retention limits
- Provide user data deletion mechanisms

### 9.2 Selective Disclosure

Example credential disclosure:
```json
{
  "credential_type": "age_verification",
  "claim": "over_18",
  "proof": "zero_knowledge_proof_data",
  "issuer": "trusted_provider.com",
  "expires": "2026-09-09T00:00:00Z"
}
```

## 10. Extensibility Framework

### 10.1 Extension Prefixes

Future extensions MAY use reserved prefixes:
```
vc-<uid>@paix.provider.com    # Verifiable Credentials
pgp-<uid>@paix.provider.com   # PGP Integration
org-<uid>@paix.provider.com   # Organization Addresses
```

### 10.2 Extension Process

1. **Proposal**: Submit extension proposal via GitHub
2. **Review**: Community and security review
3. **Testing**: Reference implementation
4. **Adoption**: Prefix reservation and documentation

## 11. IANA Considerations

This specification requests no actions from IANA. The `paix.` subdomain pattern uses existing DNS infrastructure without requiring new registry entries.

## 12. References

### Normative References
- RFC 5321: Simple Mail Transfer Protocol
- RFC 5322: Internet Message Format
- RFC 7515: JSON Web Signature (JWS)
- RFC 8174: Ambiguity of Uppercase vs Lowercase

### Informative References
- RFC 7208: Sender Policy Framework (SPF)
- RFC 6376: DomainKeys Identified Mail (DKIM)
- RFC 7489: Domain-based Message Authentication (DMARC)

---

## Appendices

### Appendix A: Reference Implementations

Reference implementations and code samples available at:
- https://github.com/privateaiexchange/paix-examples

### Appendix B: Test Vectors

[TODO: Add test vectors for address parsing, signature generation, etc.]

### Appendix C: Migration Guide

[TODO: Add guidance for migrating from other authentication methods]

---

**Document Status**: Draft v0.1  
**Last Updated**: September 9, 2025  
**Authors**: Valto Loikkanen, Tero Ahola  
**License**: MIT