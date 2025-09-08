# PAIX Address Examples

This document provides examples of valid and invalid PAIX addresses, along with usage guidelines.

## Valid Address Examples

### Basic Addresses
```
k9hm4q@paix.example.com
user123@paix.provider.org
alice_w@paix.company.net
```

### Addresses with Embedded Connect Key (ECK)
```
k9hm4q.k_AB12CD34@paix.example.com
user123.k_XY98ZW76@paix.provider.org
alice_w.k_SECURE12345@paix.company.net
```

### Addresses with Tags
```
k9hm4q+billing@paix.example.com
user123+travel@paix.provider.org
alice_w+work@paix.company.net
```

### Full Format (UID + ECK + Tag)
```
k9hm4q.k_AB12CD34+billing@paix.example.com
user123.k_XY98ZW76+travel@paix.provider.org
alice_w.k_SECURE12345+work@paix.company.net
```

## Invalid Address Examples

### Missing PAIX Subdomain
```
❌ k9hm4q@example.com           # Should be: k9hm4q@paix.example.com
❌ user123@provider.org         # Should be: user123@paix.provider.org
```

### Incorrect ECK Format
```
❌ k9hm4q.AB12CD34@paix.example.com     # Missing 'k_' prefix
❌ user123.key_XY98@paix.provider.org   # Wrong prefix format
❌ alice_w.k_@paix.company.net          # Empty ECK value
```

### UID Too Short
```
❌ ab@paix.example.com          # UID must be 6-16 characters
❌ x123@paix.provider.org       # Too short
❌ short@paix.company.net       # Exactly 5 chars (below minimum)
```

### UID Too Long
```
❌ verylongusernamethatexceedslimit@paix.example.com
❌ thisiswaytoolongforavaliduid@paix.provider.org
```

### Invalid Characters
```
❌ user@name@paix.example.com   # Invalid '@' in UID
❌ user.name@paix.example.com   # Periods not allowed in UID (except before ECK)
❌ user+tag@paix.example.com    # Plus only allowed after UID.ECK
```

## Usage Patterns

### Personal vs. Professional
```
# Personal use
emma_k@paix.prifina.com
john_doe@paix.personal.net

# Professional use  
j_smith@paix.company.com
sales_team@paix.business.org
```

### Service-Specific Tags
```
# Different services/contexts
user123+netflix@paix.example.com      # For Netflix interactions
user123+banking@paix.example.com      # For banking services  
user123+travel@paix.example.com       # For travel bookings
user123+shopping@paix.example.com     # For e-commerce
```

### ECK Scoping
```
# Service-specific ECKs (different keys for different services)
user123.k_NETFLIX01@paix.example.com
user123.k_BANK_SEC@paix.example.com  
user123.k_TRAVEL99@paix.example.com
```

## Real-World Scenarios

### Emma's PAIX Addresses
```
# Primary address with general ECK
emma_k.k_GH78IJ90@paix.prifina.com

# Service-specific addresses
emma_k.k_AIR_TRV+flights@paix.prifina.com    # For airline services
emma_k.k_FIN_SEC+banking@paix.prifina.com    # For financial services
emma_k+social@paix.prifina.com               # For social platforms (no ECK)
```

### Service Provider Examples
```
# Different providers
alice123@paix.prifina.com       # Prifina as provider
bob456@paix.microsoft.com       # Microsoft as provider  
carol789@paix.google.com        # Google as provider
dave012@paix.selfhosted.dev     # Self-hosted provider
```

## Security Considerations

### ECK Best Practices
```
# Good: Specific, time-limited ECKs
user.k_BANK2025Q1@paix.example.com      # Banking for Q1 2025
user.k_SHOP_DEC@paix.example.com        # Shopping for December

# Avoid: Generic, long-term ECKs  
user.k_MASTER@paix.example.com          # Too broad
user.k_PERM@paix.example.com            # Permanent access
```

### Tag Usage for Privacy
```
# Good: Generic tags
user+services@paix.example.com
user+commerce@paix.example.com

# Avoid: Revealing personal info
user+divorce_lawyer@paix.example.com
user+medical_debt@paix.example.com
```

## Parsing Guidelines

### Regular Expression Pattern
```regex
^([a-zA-Z_][a-zA-Z0-9_]{5,15})(\\.k_[a-zA-Z0-9_\\-]{8,32})?(\\+[a-zA-Z0-9_\\-]{1,32})?@paix\\.[a-zA-Z0-9\\-\\.]+$
```

### Component Extraction
```javascript
function parsePAIXAddress(address) {
  const regex = /^([a-zA-Z_][a-zA-Z0-9_]{5,15})(\.k_([a-zA-Z0-9_\-]{8,32}))?(\+([a-zA-Z0-9_\-]{1,32}))?@paix\.(.+)$/;
  const match = address.match(regex);
  
  if (!match) return null;
  
  return {
    uid: match[1],
    eck: match[3] || null,
    tag: match[5] || null,
    provider: match[6],
    full: address
  };
}
```

### Validation Examples
```javascript
// Valid addresses
console.log(parsePAIXAddress("user123@paix.example.com"));
// { uid: "user123", eck: null, tag: null, provider: "example.com" }

console.log(parsePAIXAddress("user123.k_ABC123+work@paix.example.com"));
// { uid: "user123", eck: "ABC123", tag: "work", provider: "example.com" }

// Invalid addresses
console.log(parsePAIXAddress("user@example.com"));        // null
console.log(parsePAIXAddress("ab@paix.example.com"));     // null (UID too short)
```

## Migration from Regular Email

### Gradual Transition
```
# Phase 1: Start using PAIX for new services
newservice@example.com → user123+newservice@paix.provider.com

# Phase 2: Migrate existing services  
oldservice@example.com → user123+oldservice@paix.provider.com

# Phase 3: Enable AI features with ECKs
user123+service@paix.provider.com → user123.k_ABC123+service@paix.provider.com
```

### Backup Email Configuration
```
# Keep regular email as backup
Primary: user123@paix.provider.com
Backup: user123@gmail.com

# Forward PAIX to regular email during transition
PAIX Address → Forwards to → Regular Email
            ↘ Also accessible by AI
```