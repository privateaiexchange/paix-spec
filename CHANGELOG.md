# PAIX Protocol Changelog

All notable changes to the PAIX protocol specification will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Initial repository structure
- Core documentation framework
- Community governance guidelines

## [0.1.0-draft] - 2025-09-09

### Added
- **Core Protocol Design**
  - PAIX address format: `<uid>[.k_<eck>][+tag]@paix.<provider-domain>`
  - ECK (Embedded Connect Key) for email→HTTPS escalation
  - AT-EP (Authenticated Email Actions) with JWS signing
  - PCP (Provider Capability Protocol) for capability discovery
  - OTP (One-Time Password) guardrails for sensitive operations

- **Documentation**
  - Protocol primer and overview
  - Technical specification v0.1
  - Security and privacy considerations
  - Developer and user guides
  - Real-world usage scenarios

- **Core Features**
  - Shared inbox access (IMAP + forwarding)
  - Cryptographic action verification
  - Provider capability advertisement
  - User-controlled permission system
  - Extensibility framework for future enhancements

- **Security Model**
  - Built on email authentication (SPF/DKIM/DMARC)
  - Human-in-the-loop for sensitive actions
  - Cryptographic signing for all automated actions
  - Selective credential disclosure
  - Complete audit trail

### Technical Specifications
- Address parsing and validation rules
- ECK generation and management
- AT-EP message format and verification
- PCP query/response protocol
- Provider discovery mechanisms

### Design Principles
- Universal compatibility (works with existing email)
- Gradual adoption path for services
- User ownership and control
- Privacy by default
- Open and vendor-neutral

---

## Version Guidelines

### Version Format
- **Major.Minor.Patch** (e.g., 1.0.0)
- **Pre-release** suffixed with `-draft`, `-alpha`, `-beta` (e.g., 0.1.0-draft)

### Change Categories
- **Added** - New features and capabilities
- **Changed** - Changes to existing functionality
- **Deprecated** - Features marked for removal
- **Removed** - Features removed from specification
- **Fixed** - Bug fixes and corrections
- **Security** - Security-related changes and improvements

### Breaking Changes
Breaking changes are changes that require updates to existing implementations:
- Address format modifications
- Core protocol behavior changes
- Mandatory new requirements for providers/services
- Removal of previously supported features

### Backwards Compatibility
The PAIX protocol prioritizes backwards compatibility. Breaking changes will:
- Be clearly marked and explained
- Include migration guidance
- Have extended deprecation periods where possible
- Be avoided unless absolutely necessary for security or fundamental improvements

---

## Contributing to Changelog

When contributing changes:
1. Add entries under `[Unreleased]` section
2. Use appropriate change category (Added, Changed, etc.)
3. Write clear, concise descriptions
4. Reference GitHub issues/PRs where applicable
5. Indicate if change affects backwards compatibility

Example entry:
```markdown
### Added
- New capability for encrypted message payloads (#123)

### Changed
- Improved ECK key rotation mechanism for better security (#456)

### Security
- Enhanced validation for AT-EP signatures to prevent replay attacks (#789)
```