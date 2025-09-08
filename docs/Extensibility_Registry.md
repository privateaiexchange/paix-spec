# PAIX Extensibility Registry (Draft)

PAIX supports optional **prefixes** in the local-part to enable future consensus extensions:

```
<prefix>-<uid>[.k_<eck>]@paix.<provider>
```

Unknown prefixes MUST degrade gracefully to normal email semantics, ensuring backwards compatibility.

## Design Principles

**Backwards Compatibility**
- All PAIX implementations must handle unknown prefixes gracefully
- Fallback to standard email behavior when prefix is not recognized
- Core protocol remains minimal and stable

**Consensus-Driven**
- Extensions require community discussion and review
- Security implications must be thoroughly analyzed
- Multiple implementation commitment before acceptance

**Namespace Protection**
- Reserved prefixes prevent conflicts and ambiguity
- Clear ownership and maintenance responsibilities
- Deprecation process for unused extensions

## Reserved Prefixes (Proposed)

### **`vc-`** - Verifiable Credentials
**Status:** Proposed  
**Purpose:** Enhanced credential flows and selective disclosure  
**Example:** `vc-k9hm4q.k_ABC123@paix.provider.com`

**Use Cases:**
- Age verification without revealing exact birth date
- Professional credentials (licenses, certifications)
- Institutional affiliations (university, employer)
- Government-issued identity verification

**Security Considerations:**
- Zero-knowledge proof integration
- Credential revocation mechanisms
- Privacy-preserving attribute disclosure

### **`pgp-`** - OpenPGP Integration
**Status:** Proposed  
**Purpose:** End-to-end encryption and digital signing layer  
**Example:** `pgp-user123.k_XYZ789@paix.provider.com`

**Use Cases:**
- Encrypted message payloads
- Enhanced signature verification
- Key distribution and management
- Legacy PGP system integration

### **`org-`** - Organizational Scoping
**Status:** Proposed  
**Purpose:** Enterprise and organizational address management  
**Example:** `org-dept_hr.k_COMPANY1@paix.enterprise.com`

**Use Cases:**
- Department-specific addresses
- Role-based access control
- Organizational hierarchy support
- Multi-tenant provider scenarios

### **`ai-`** - Agent Coordination
**Status:** Proposed  
**Purpose:** Agent-to-agent coordination and metadata  
**Example:** `ai-assistant.k_COORD123@paix.provider.com`

**Use Cases:**
- Multi-agent collaboration hints
- Agent capability advertisement
- Coordination protocol extensions
- AI service discovery

## Extension Proposal Process

### 1. **Proposal Phase**
- Open GitHub Issue with `extension` label
- Use extension proposal template
- Include detailed specification and rationale
- Identify security and privacy implications

### 2. **Community Review (14 days minimum)**
- Public discussion in GitHub Discussions
- Security expert review required
- Implementation feasibility assessment
- Backwards compatibility verification

### 3. **Technical Assessment**
- Formal security review
- Privacy impact analysis
- Interoperability testing
- Performance considerations

### 4. **Implementation Commitment**
- At least two independent implementations planned
- Provider support confirmation
- Client library integration plans
- Migration strategy for existing addresses

### 5. **Acceptance**
- Consensus from maintainers required
- Community support demonstrated
- Documentation complete and reviewed
- Prefix officially reserved

## Extension Requirements

### **Technical Requirements**
- **Graceful Degradation:** Must work as regular email when extension not supported
- **Security Model:** Cannot weaken core PAIX security guarantees
- **Privacy Preservation:** Must not leak additional user information
- **Performance Impact:** Minimal overhead for non-participating systems

### **Documentation Requirements**
- Complete specification with examples
- Security and privacy analysis
- Implementation guide for providers
- Migration guide for existing users
- Test vectors and validation procedures

### **Governance Requirements**
- Clear maintainer commitment
- Deprecation policy defined
- Version compatibility matrix
- Community feedback incorporation

## Prefix Format Rules

### **Naming Convention**
- Lowercase letters only
- 2-4 characters recommended
- Descriptive but concise
- Avoid conflicts with existing standards

### **Format Validation**
```regex
^[a-z]{2,4}-[a-zA-Z_][a-zA-Z0-9_]{5,15}(\\.k_[a-zA-Z0-9_\\-]{8,32})?@paix\\.[a-zA-Z0-9\\-\\.]+$
```

### **Reserved Namespaces**
- Single letters (a-z) reserved for future core protocol use
- `paix-` prefix reserved for meta-protocol extensions
- `test-` prefix reserved for experimental implementations

## Implementation Guidelines

### **Provider Support**
```javascript
function parseExtendedPAIXAddress(address) {
  const match = address.match(/^([a-z]+)-(.+)@paix\.(.+)$/);
  if (!match) return null;
  
  const [, prefix, localPart, domain] = match;
  
  // Check if prefix is supported
  if (!supportedPrefixes.includes(prefix)) {
    // Fallback to standard email handling
    return handleAsRegularEmail(address);
  }
  
  // Process extension-specific logic
  return processExtendedAddress(prefix, localPart, domain);
}
```

### **Client Handling**
```javascript
function createExtendedAddress(prefix, uid, eck, provider) {
  // Validate prefix support
  if (!isExtensionSupported(prefix)) {
    throw new Error(`Extension prefix '${prefix}' not supported`);
  }
  
  const eckPart = eck ? `.k_${eck}` : '';
  return `${prefix}-${uid}${eckPart}@paix.${provider}`;
}
```

## Future Extensions Under Consideration

### **`dns-`** - DNS-Based Discovery
Enhanced service discovery through DNS TXT records

### **`oauth-`** - OAuth Integration
Bridging PAIX with OAuth 2.0 flows

### **`pay-`** - Payment Integration
Streamlined payment and billing automation

### **`iot-`** - IoT Device Support
Internet of Things device communication

## Registry Maintenance

### **Prefix Status Lifecycle**
1. **Proposed** - Under community review
2. **Draft** - Accepted but not yet stable
3. **Stable** - Production ready, backwards compatibility guaranteed
4. **Deprecated** - Being phased out, migration period active
5. **Retired** - No longer supported, prefix may be reused

### **Maintenance Responsibilities**
- Extension authors maintain documentation
- Security reviews required for updates
- Community notification for status changes
- Migration support during deprecation

## Questions and Contributions

**Proposing a New Extension:**
1. Review existing proposals and registry
2. Open GitHub Discussion for initial feedback
3. Submit formal proposal via GitHub Issue
4. Participate in community review process

**Registry Updates:**
- Changes require PR to this document
- Community review for all modifications
- Maintainer approval for registry updates

---

**Status:** Draft Registry  
**Last Updated:** September 9, 2025  
**Maintainers:** PAIX Core Team  

*This registry evolves through community consensus. All extensions must demonstrate clear value and maintain the core principles of simplicity, security, and backwards compatibility.*