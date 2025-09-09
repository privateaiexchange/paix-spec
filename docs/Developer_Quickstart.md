# Developer Quickstart Guide

**Get started with recognizing and integrating PAIX addresses in your service**

## Overview

This guide helps developers quickly add PAIX (Private AI eXchange) support to their existing services. PAIX extends email to enable secure human-AI collaboration, and your service can participate with minimal changes.

## SDK Libraries & Tools

For ready-to-use libraries and complete integration examples:
- **[PAIX Examples Repository](https://github.com/privateaiexchange/paix-examples)** - SDK libraries, integration examples, and reference implementations
- **[JavaScript/TypeScript SDK](https://github.com/privateaiexchange/paix-examples/tree/main/sdks/javascript)** *(coming soon)*
- **[Python SDK](https://github.com/privateaiexchange/paix-examples/tree/main/sdks/python)** *(coming soon)*
- **[Security Examples](https://github.com/privateaiexchange/paix-examples/tree/main/security)** *(coming soon)*

## Quick Integration Levels

### Level 0: Do Nothing ✅
**Effort:** Zero  
**Benefit:** PAIX emails work like regular email

Your service already works with PAIX! Users can send emails from PAIX addresses and you'll receive them normally.

```python
# Your existing email handling continues to work
def handle_incoming_email(sender, subject, body):
    # sender might be: "user123@paix.example.com"
    # Process normally - no changes needed
    process_email(sender, subject, body)
```

### Level 1: Recognition 🎯
**Effort:** 5 minutes  
**Benefit:** Reduce spam, improve routing, better user experience

Detect PAIX addresses to apply special handling like reduced spam filtering or premium support routing.

```python
import re

def is_paix_address(email):
    """Check if email is a PAIX address"""
    pattern = r'^[a-zA-Z_][a-zA-Z0-9_]{5,15}(\\.k_[a-zA-Z0-9_\\-]{8,32})?(\\+[a-zA-Z0-9_\\-]{1,32})?@paix\\.[a-zA-Z0-9\\-\\.]+$'
    return bool(re.match(pattern, email))

def handle_email(sender, subject, body):
    if is_paix_address(sender):
        # PAIX user - apply premium routing
        route_to_premium_support(sender, subject, body)
    else:
        # Regular email handling
        route_to_standard_support(sender, subject, body)
```

> **💡 Pro Tip**: See [address validation examples](https://github.com/privateaiexchange/paix-examples/tree/main/tools/address-parser) for production-ready parsers in multiple languages.

### Level 2: Capability Discovery 🔍
**Effort:** 30 minutes  
**Benefit:** Advertise PAIX features to users and their AIs

Let PAIX users know what features you support for AI automation.

```python
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/.well-known/paix')
def paix_capabilities():
    return jsonify({
        "paix_version": "0.1",
        "supported_features": {
            "account": {
                "actions": ["view_profile", "update_email", "export_data"],
                "escalation": True,
                "otp_required": ["export_data"]
            },
            "billing": {
                "actions": ["view_invoices", "update_payment"],
                "escalation": True, 
                "otp_required": ["update_payment"]
            },
            "notifications": {
                "actions": ["subscribe", "unsubscribe", "preferences"],
                "escalation": False,
                "otp_required": []
            }
        },
        "provider_info": {
            "name": "Your Service Name",
            "paix_endpoint": "https://api.yourservice.com/paix",
            "documentation": "https://docs.yourservice.com/paix"
        }
    })
```

> **💡 Pro Tip**: Check out [capability discovery examples](https://github.com/privateaiexchange/paix-examples/tree/main/tools/capability-client) for different implementation patterns.

### Level 3: Action Processing ⚡
**Effort:** 2-4 hours  
**Benefit:** Enable AI automation with human oversight

Process structured action requests from AIs, with user confirmation for sensitive operations.

```python
import json
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.primitives.asymmetric import ec

def parse_paix_action(email_body, headers):
    """Parse PAIX action from email"""
    try:
        # Check for PAIX action headers
        if 'PAIX-Action-ID' not in headers:
            return None
            
        # Parse JSON body
        action_data = json.loads(email_body)
        
        return {
            'action': action_data.get('action'),
            'parameters': action_data.get('parameters', {}),
            'action_id': headers['PAIX-Action-ID'],
            'signature': headers.get('PAIX-Signature')
        }
    except (json.JSONDecodeError, KeyError):
        return None

def handle_paix_action(sender, action_data):
    """Process PAIX action with appropriate security"""
    action = action_data['action']
    params = action_data['parameters']
    
    # Verify signature
    if not verify_action_signature(action_data, sender):
        return send_error_response(sender, "Invalid signature")
    
    # Check if OTP required
    if requires_otp(action):
        return send_otp_challenge(sender, action_data)
    
    # Process action
    result = process_action(action, params, sender)
    return send_action_response(sender, result)
```

> **💡 Pro Tip**: See [signature verification examples](https://github.com/privateaiexchange/paix-examples/tree/main/security/signature-verify) for production-ready security implementations.

## Address Format Quick Reference

```
# Basic PAIX address
user123@paix.provider.com

# With Embedded Connect Key (ECK) for API access
user123.k_ABC123@paix.provider.com

# With tag for categorization  
user123+billing@paix.provider.com

# Full format
user123.k_ABC123+billing@paix.provider.com
```

## Common Integration Patterns

### 1. Email-First Services
```python
# Perfect for: Support systems, newsletters, notifications
def handle_support_request(sender, subject, body):
    user_info = {
        'email': sender,
        'is_paix': is_paix_address(sender),
        'supports_ai': has_embedded_connect_key(sender)
    }
    
    if user_info['is_paix']:
        # Enable AI-friendly features
        enable_structured_responses(user_info)
        
    process_support_ticket(user_info, subject, body)
```

> **💡 See Example**: [Customer Support Integration](https://github.com/privateaiexchange/paix-examples/tree/main/integrations/support)

### 2. SaaS Applications
```python
# Perfect for: Project management, CRM, productivity tools
def create_api_session(paix_address):
    eck = extract_embedded_connect_key(paix_address)
    if eck:
        # Verify ECK and create scoped API session
        session = verify_and_create_session(eck)
        return session
    return None
```

> **💡 See Example**: [SaaS Platform Integration](https://github.com/privateaiexchange/paix-examples/tree/main/integrations/saas)

### 3. E-commerce Platforms
```python
# Perfect for: Order tracking, returns, customer service
def handle_order_inquiry(sender, body):
    if is_paix_address(sender):
        # Parse structured query
        query = parse_structured_query(body)
        if query:
            return handle_ai_query(sender, query)
    
    # Fall back to human customer service
    route_to_human_agent(sender, body)
```

> **💡 See Example**: [E-commerce Integration](https://github.com/privateaiexchange/paix-examples/tree/main/integrations/ecommerce)

## Security Implementation

### Basic Signature Verification
```python
def verify_action_signature(action_data, sender_address):
    """Verify PAIX action signature"""
    try:
        signature = action_data.get('signature')
        if not signature:
            return False
            
        # Get sender's public key
        public_key = get_public_key_for_address(sender_address)
        if not public_key:
            return False
            
        # Verify JWS signature
        return verify_jws_signature(signature, action_data, public_key)
        
    except Exception as e:
        log_security_error(f"Signature verification failed: {e}")
        return False
```

> **💡 Production Ready**: Use the [signature verification utilities](https://github.com/privateaiexchange/paix-examples/tree/main/security/signature-verify) for battle-tested implementations.

### OTP Implementation
```python
def send_otp_challenge(sender, action_data):
    """Send OTP challenge for sensitive actions"""
    otp_code = generate_otp()
    store_pending_action(sender, action_data, otp_code)
    
    challenge_email = f"""
Subject: PAIX-OTP Required: {action_data['action']}
From: noreply@yourservice.com
To: {sender}
PAIX-Version: 0.1
PAIX-OTP-Challenge: true

Your AI is requesting to: {describe_action(action_data)}

To approve this action, reply with:
OTP: {otp_code}

This request expires in 10 minutes.
Action ID: {action_data['action_id']}
"""
    send_email(challenge_email)

def verify_otp_response(sender, otp_response):
    """Verify OTP and process pending action"""
    pending = get_pending_action(sender)
    if not pending or pending['otp'] != otp_response:
        return False
        
    # OTP verified, process the action
    return process_action(pending['action_data'])
```

> **💡 See Examples**: [OTP challenge/response patterns](https://github.com/privateaiexchange/paix-examples/tree/main/security/otp-handlers) for different implementation approaches.

## Testing Your Integration

### 1. Test Address Recognition
```python
def test_paix_recognition():
    test_cases = [
        ("user123@paix.example.com", True),
        ("user123.k_ABC123@paix.example.com", True),
        ("user123+tag@paix.example.com", True),
        ("user@example.com", False),
        ("ab@paix.example.com", False)  # Too short
    ]
    
    for address, expected in test_cases:
        result = is_paix_address(address)
        assert result == expected, f"Failed for {address}"
```

### 2. Test Capability Discovery
```bash
# Test your capability endpoint
curl https://yourservice.com/.well-known/paix

# Should return JSON with supported features
```

### 3. Test Action Processing
```python
def test_action_processing():
    test_action = {
        "action": "view_profile",
        "parameters": {},
        "timestamp": "2025-09-09T12:00:00Z",
        "action_id": "test_123"
    }
    
    result = handle_paix_action("user123@paix.example.com", test_action)
    assert result['status'] == 'success'
```

## Error Handling

### Common Error Responses
```python
def send_error_response(sender, error_message, error_code=None):
    """Send structured error response"""
    response = {
        "status": "error",
        "error": {
            "message": error_message,
            "code": error_code,
            "timestamp": datetime.utcnow().isoformat()
        }
    }
    
    email_body = f"""
Subject: PAIX-Response: Error
From: noreply@yourservice.com
To: {sender}
PAIX-Version: 0.1
PAIX-Response-Type: error

{json.dumps(response, indent=2)}
"""
    send_email(email_body)
```

### Error Scenarios
```python
# Invalid signature
send_error_response(sender, "Action signature verification failed", "INVALID_SIGNATURE")

# Unsupported action
send_error_response(sender, "Action 'delete_universe' not supported", "UNSUPPORTED_ACTION")

# Missing parameters
send_error_response(sender, "Required parameter 'order_id' missing", "MISSING_PARAMETER")

# Rate limiting
send_error_response(sender, "Too many requests, try again later", "RATE_LIMITED")
```

## Best Practices

### 1. Start Simple
- Begin with Level 1 (recognition) 
- Add features gradually based on user demand
- Monitor usage patterns to prioritize features

### 2. Security First
- Always verify signatures for actions
- Use OTP for sensitive operations
- Log all PAIX interactions for audit
- Implement rate limiting

### 3. User Experience
- Provide clear error messages
- Support both AI and human interaction
- Maintain backwards compatibility
- Document your PAIX features

### 4. Testing Strategy
```python
# Test with real PAIX addresses from development providers
def integration_test():
    # Use test PAIX provider for development
    test_address = "testuser@paix.dev-provider.com"
    
    # Test each integration level
    assert is_paix_address(test_address)
    
    capabilities = get_capabilities()
    assert capabilities['paix_version'] == '0.1'
    
    # Test action flow with test credentials
    test_signed_action(test_address)
```

## Community Examples

Real-world implementations and patterns from the community:
- **[Community Integrations](https://github.com/privateaiexchange/paix-examples/tree/main/community)** - User-contributed examples
- **[Platform-Specific Guides](https://github.com/privateaiexchange/paix-examples/tree/main/integrations)** - Integration patterns for popular platforms
- **[Security Patterns](https://github.com/privateaiexchange/paix-examples/tree/main/security)** - Production security implementations

## Next Steps

1. **Choose Your Level**: Start with Level 1 recognition
2. **Use SDKs**: Check [available SDKs](https://github.com/privateaiexchange/paix-examples/tree/main/sdks) for your language
3. **Join Community**: Participate in [GitHub Discussions](https://github.com/privateaiexchange/paix-spec/discussions)
4. **Get Test Credentials**: Contact PAIX providers for development access
5. **Share Examples**: Contribute to [paix-examples](https://github.com/privateaiexchange/paix-examples) to help others

## Resources

### Technical Documentation
- **Full Specification**: [Spec_v0.1.md](Spec_v0.1.md)
- **Address Examples**: [examples/addresses.md](../examples/addresses.md)
- **Security Guide**: [Security_Privacy.md](Security_Privacy.md)
- **Provider Guide**: [Providers_Guide.md](Providers_Guide.md)

### Implementation Examples
- **[Examples Repository](https://github.com/privateaiexchange/paix-examples)** - Complete implementations and SDKs
- **Real-world Scenarios**: [Journey_Emma.md](Journey_Emma.md)
- **Services Guide**: [Services_Guide.md](Services_Guide.md)

### Community & Support
- **[GitHub Issues](https://github.com/privateaiexchange/paix-spec/issues)** - Bug reports and feature requests
- **[GitHub Discussions](https://github.com/privateaiexchange/paix-spec/discussions)** - Questions and community help
- **[Contributing Guide](../CONTRIBUTING.md)** - How to contribute to PAIX

---

## 🧭 Navigation

**Getting Started**: [Primer](Primer_Cover.md) → [Whitepaper](Whitepaper.md) → **Developer Quickstart**

**By Role**:
- **End Users**: [Individuals Guide](Individuals_Guide.md)
- **Services**: [Services Guide](Services_Guide.md) | [Business Case](PAIX_Value_Stack.md)
- **Providers**: [Providers Guide](Providers_Guide.md)

**Technical**: [Specification](Spec_v0.1.md) | [Security](Security_Privacy.md) | [Examples](https://github.com/privateaiexchange/paix-examples)

---

*Ready to enable AI-human collaboration in your service? Start with Level 1 recognition and grow from there!*