# Security & Privacy (Working Draft)

## Threat Model (to be expanded)

**Addressed Threats:**
- **Spoofed sender / missing DKIM** → reject or mark untrusted
- **Replay attacks** → nonce cache + short token lifetimes
- **Body tampering** → canonical hash binding
- **Phishing / UI confusion** → OTP UX guidance, clear origin headers
- **Provider compromise** → key rotation, revocation lists, audit trail

**Ongoing Risks:**
- Provider compromise
- Private key theft
- Social engineering attacks
- DNS hijacking
- Man-in-the-middle attacks

## Mail Hygiene Requirements

- **SPF/DKIM/DMARC MUST pass** or be treated as untrusted
- Providers SHOULD publish strict DMARC policies
- Regular monitoring of authentication failures
- Proper key rotation procedures

## Cryptographic Requirements

**Digital Signatures:**
- ECDSA with P-256 curve (ES256) recommended
- RSA with PSS padding (PS256) as alternative
- Minimum 2048-bit RSA keys

**Hashing:**
- SHA-256 for all hash operations
- HMAC-SHA256 for MAC operations

## Privacy Protections

**Data Minimization:**
- Claims avoid PII; use DIDs/domains
- Collect minimal necessary information
- Implement data retention limits

**Selective Disclosure:**
- Share proofs (e.g., "over 18") without raw data
- Verifiable credentials for attributes (age/residency) without underlying PII
- Zero-knowledge proof capabilities where applicable

**User Control:**
- Complete audit trail visible to users
- Ability to revoke addresses and keys
- Control over AI permissions per service

## Security Implementation Guidelines

### JWS Signature Process
```
1. Canonicalize message body
2. Generate SHA-256 hash of body
3. Create JWS header with algorithm and key ID
4. Sign with private key
5. Include signature in X-PAIX-Preamble header
```

### Nonce and Replay Protection
- Minimum 128-bit random nonce required
- Replay cache must maintain nonces for token lifetime
- Timestamp validation within acceptable window
- Idempotent action processing where possible

### Key Management
- Regular key rotation (recommended: annually)
- Secure key storage (HSM preferred)
- Revocation lists published and checked
- Public key distribution via DNS/HTTPS

## OTP Security Requirements

**Human-in-the-Loop Guarantees:**
- OTP cannot be bypassed by AI systems
- Clear action description in OTP prompts
- Time-limited OTP validity (recommended: 10 minutes)
- Single-use OTP codes

**Sensitive Action Categories:**
- Financial transactions
- Account deletion or suspension
- Security setting changes
- Data export or migration
- Legal agreement modifications

## Audit and Logging

**Required Logging:**
- All PAIX action attempts and results
- Authentication failures and successes
- Key usage and rotation events
- OTP generation and verification

**User Visibility:**
- Complete action history accessible to users
- Real-time notifications for sensitive actions
- Audit export capabilities

## Open Items (Help Wanted)

- **Formal threat model** expansion
- **Abuse rate limits** and anomaly detection patterns
- **Secure storage guidance** for keys (KMS/HSM recommendations)
- **Browser extension security** model
- **Provider security certification** framework
- **Incident response** procedures for compromised keys

## References

- RFC 7515: JSON Web Signature (JWS)
- RFC 7208: Sender Policy Framework (SPF)
- RFC 6376: DomainKeys Identified Mail (DKIM)
- RFC 7489: Domain-based Message Authentication (DMARC)

---

**Status:** Working Draft  
**Last Updated:** September 9, 2025  
**Contributors Needed:** Security experts, cryptographers, email authentication specialists

*This document is a living specification. Contributions and security reviews are welcomed through GitHub Issues and Discussions.*