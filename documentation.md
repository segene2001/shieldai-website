# ShieldAI Documentation

## Complete Customer Documentation

---

# Table of Contents

1. [Getting Started](#getting-started)
2. [Quick Start](#quick-start)
3. [API Reference](#api-reference)
4. [Integration Guides](#integration-guides)
5. [Compliance](#compliance)
6. [Security](#security)
7. [Troubleshooting](#troubleshooting)
8. [FAQ](#faq)

---

# Getting Started

## What is ShieldAI?

ShieldAI is a PIPEDA-compliant AI gateway that enables Canadian enterprises to safely use AI services like OpenAI's ChatGPT while maintaining full privacy compliance.

### Key Features:
- ✅ **PIPEDA Compliant** - Full compliance with Canadian privacy laws
- ✅ **Canadian Data Residency** - All data processed in Canada
- ✅ **Automatic PII Protection** - Detect and mask sensitive data
- ✅ **Complete Audit Trail** - Full compliance reporting
- ✅ **Easy Integration** - Drop-in replacement for OpenAI API

### How It Works:

```
Your Application
      ↓
ShieldAI Gateway (Canada)
  - Detect PII
  - Mask sensitive data
  - Log for compliance
      ↓
AI Provider (OpenAI, Claude, etc.)
      ↓
Response
      ↓
Your Application
```

---

# Quick Start

## 1. Get Your API Key

After signing up, you'll receive your API key:

```
tct_yourcompany_abc123xyz456
```

**Keep this secure!** Treat it like a password.

## 2. Make Your First Request

### Using cURL:

```bash
curl https://api.shieldai.ca/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "model": "gpt-3.5-turbo",
    "messages": [
      {"role": "user", "content": "Hello from ShieldAI!"}
    ]
  }'
```

### Using Python:

```python
import openai

# Configure ShieldAI
openai.api_base = "https://api.shieldai.ca/v1"
openai.api_key = "YOUR_API_KEY"

# Make request
response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[
        {"role": "user", "content": "Hello from ShieldAI!"}
    ]
)

print(response.choices[0].message.content)
```

### Using Node.js:

```javascript
const { Configuration, OpenAIApi } = require("openai");

const configuration = new Configuration({
  apiKey: "YOUR_API_KEY",
  basePath: "https://api.shieldai.ca/v1"
});

const openai = new OpenAIApi(configuration);

const response = await openai.createChatCompletion({
  model: "gpt-3.5-turbo",
  messages: [
    {role: "user", content: "Hello from ShieldAI!"}
  ]
});

console.log(response.data.choices[0].message.content);
```

## 3. Check Your Dashboard

Visit https://dashboard.shieldai.ca to see:
- Request logs
- PII detections
- Compliance reports
- Usage statistics

---

# API Reference

## Base URL

```
https://api.shieldai.ca/v1
```

## Authentication

All requests require an API key in the Authorization header:

```
Authorization: Bearer YOUR_API_KEY
```

## Endpoints

### Chat Completions

**POST** `/v1/chat/completions`

OpenAI-compatible chat completions endpoint.

**Request:**

```json
{
  "model": "gpt-3.5-turbo",
  "messages": [
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "Hello!"}
  ],
  "temperature": 0.7,
  "max_tokens": 150
}
```

**Response:**

```json
{
  "id": "chatcmpl-123",
  "object": "chat.completion",
  "created": 1677652288,
  "model": "gpt-3.5-turbo",
  "choices": [{
    "index": 0,
    "message": {
      "role": "assistant",
      "content": "Hello! How can I help you today?"
    },
    "finish_reason": "stop"
  }],
  "usage": {
    "prompt_tokens": 9,
    "completion_tokens": 12,
    "total_tokens": 21
  }
}
```

**Compliance Headers:**

```
X-PIPEDA-Compliant: true
X-Data-Residency: CANADA
X-PII-Detected: 2
X-PII-Masked: true
```

### Health Check

**GET** `/health`

Check API status.

**Response:**

```json
{
  "status": "healthy",
  "timestamp": "2025-01-15T10:30:00Z",
  "jurisdiction": "Canada",
  "compliance": "PIPEDA"
}
```

### Usage Statistics

**GET** `/customer/usage`

Get your current usage statistics.

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
```

**Response:**

```json
{
  "customer_id": "yourcompany",
  "customer_name": "Your Company Inc.",
  "plan": "professional",
  "tokens_used": 250000,
  "tokens_limit": 1000000,
  "usage_percentage": 25.0,
  "total_cost": 75.50
}
```

### Billing

**GET** `/customer/bill`

Get your current month's bill.

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
```

**Response:**

```json
{
  "customer_id": "yourcompany",
  "billing_period": "2025-01",
  "base_fee": 10000,
  "tokens_included": 1000000,
  "tokens_used": 1250000,
  "overage_tokens": 250000,
  "overage_cost": 15.00,
  "total_bill": 10015.00
}
```

### Compliance Audit

**GET** `/compliance/audit`

Get audit logs for compliance reporting.

**Parameters:**
- `limit` (optional): Number of logs to return (default: 100)

**Response:**

```json
{
  "total_logs": 1523,
  "returned_logs": 100,
  "compliance_framework": "PIPEDA",
  "jurisdiction": "Canada",
  "logs": [
    {
      "timestamp": "2025-01-15T10:30:00Z",
      "endpoint": "/v1/chat/completions",
      "pii_detected": 2,
      "pii_types": ["email", "phone"],
      "latency_ms": 145,
      "status": "success"
    }
  ]
}
```

### Compliance Report

**POST** `/compliance/report`

Generate PIPEDA compliance report.

**Response:**

```json
{
  "report_generated": "2025-01-15T10:30:00Z",
  "jurisdiction": "Canada",
  "compliance_framework": "PIPEDA",
  "summary": {
    "total_requests": 1523,
    "pii_detections": 342,
    "average_latency_ms": 156,
    "pipeda_compliance_rate": 100.0
  },
  "pipeda_compliance": {
    "principle_1_accountability": "Compliant",
    "principle_2_identifying_purposes": "Compliant",
    ...
  }
}
```

---

# Integration Guides

## Python Integration

### Installation

```bash
pip install openai
```

### Basic Setup

```python
import openai
import os

# Configure ShieldAI
openai.api_base = "https://api.shieldai.ca/v1"
openai.api_key = os.getenv("SHIELDAI_API_KEY")

def chat(message):
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[
            {"role": "user", "content": message}
        ]
    )
    return response.choices[0].message.content

# Use it
result = chat("What is PIPEDA?")
print(result)
```

### With Error Handling

```python
import openai
from openai.error import APIError, RateLimitError, AuthenticationError

openai.api_base = "https://api.shieldai.ca/v1"
openai.api_key = "YOUR_API_KEY"

def safe_chat(message):
    try:
        response = openai.ChatCompletion.create(
            model="gpt-3.5-turbo",
            messages=[{"role": "user", "content": message}]
        )
        return response.choices[0].message.content
    except AuthenticationError:
        return "Error: Invalid API key"
    except RateLimitError:
        return "Error: Rate limit exceeded"
    except APIError as e:
        return f"Error: {str(e)}"
```

## Node.js Integration

### Installation

```bash
npm install openai
```

### Basic Setup

```javascript
const { Configuration, OpenAIApi } = require("openai");

const configuration = new Configuration({
  apiKey: process.env.SHIELDAI_API_KEY,
  basePath: "https://api.shieldai.ca/v1"
});

const openai = new OpenAIApi(configuration);

async function chat(message) {
  const response = await openai.createChatCompletion({
    model: "gpt-3.5-turbo",
    messages: [{role: "user", content: message}]
  });
  
  return response.data.choices[0].message.content;
}

// Use it
chat("What is PIPEDA?").then(console.log);
```

### Express.js API

```javascript
const express = require('express');
const { Configuration, OpenAIApi } = require("openai");

const app = express();
app.use(express.json());

const configuration = new Configuration({
  apiKey: process.env.SHIELDAI_API_KEY,
  basePath: "https://api.shieldai.ca/v1"
});

const openai = new OpenAIApi(configuration);

app.post('/api/chat', async (req, res) => {
  try {
    const { message } = req.body;
    
    const response = await openai.createChatCompletion({
      model: "gpt-3.5-turbo",
      messages: [{role: "user", content: message}]
    });
    
    res.json({
      response: response.data.choices[0].message.content
    });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

app.listen(3000, () => console.log('Server running on port 3000'));
```

## Java Integration

### Maven Dependency

```xml
<dependency>
    <groupId>com.theokanning.openai-gpt3-java</groupId>
    <artifactId>service</artifactId>
    <version>0.14.0</version>
</dependency>
```

### Basic Setup

```java
import com.theokanning.openai.OpenAiService;
import com.theokanning.openai.completion.chat.ChatCompletionRequest;
import com.theokanning.openai.completion.chat.ChatMessage;

public class ShieldAIClient {
    private static final String API_KEY = System.getenv("SHIELDAI_API_KEY");
    private static final String BASE_URL = "https://api.shieldai.ca/v1";
    
    public static void main(String[] args) {
        OpenAiService service = new OpenAiService(API_KEY);
        service.setApiUrl(BASE_URL);
        
        ChatCompletionRequest request = ChatCompletionRequest.builder()
            .model("gpt-3.5-turbo")
            .messages(Arrays.asList(
                new ChatMessage("user", "What is PIPEDA?")
            ))
            .build();
        
        String response = service.createChatCompletion(request)
            .getChoices().get(0).getMessage().getContent();
        
        System.out.println(response);
    }
}
```

## C# / .NET Integration

### NuGet Package

```bash
dotnet add package OpenAI
```

### Basic Setup

```csharp
using OpenAI_API;
using OpenAI_API.Chat;

class Program
{
    static async Task Main(string[] args)
    {
        var api = new OpenAIAPI(
            apiKey: Environment.GetEnvironmentVariable("SHIELDAI_API_KEY"),
            apiUrlFormat: "https://api.shieldai.ca/v1/{0}"
        );
        
        var chat = api.Chat.CreateConversation();
        chat.AppendUserInput("What is PIPEDA?");
        
        string response = await chat.GetResponseFromChatbotAsync();
        Console.WriteLine(response);
    }
}
```

---

# Compliance

## PIPEDA Compliance

ShieldAI ensures full compliance with all 10 PIPEDA principles:

### 1. Accountability
- Complete audit trail of all requests
- Designated privacy officer
- Regular compliance audits

### 2. Identifying Purposes
- Purpose logged for each request
- Clear documentation
- User consent tracked

### 3. Consent
- API key authentication
- Explicit customer agreements
- Consent management

### 4. Limiting Collection
- Only necessary data processed
- Minimal data retention
- Purpose-specific collection

### 5. Limiting Use, Disclosure, and Retention
- Data used only for stated purpose
- No third-party sharing
- Automatic data deletion

### 6. Accuracy
- Data integrity maintained
- Regular validation
- Error correction procedures

### 7. Safeguards
- TLS 1.3 encryption
- PII masking
- Access controls
- Regular security audits

### 8. Openness
- Transparent processing
- Public documentation
- Clear privacy policy

### 9. Individual Access
- Audit logs available
- Data access requests supported
- Timely responses

### 10. Challenging Compliance
- Compliance reports on demand
- Privacy officer contact
- Complaint procedures

## PII Detection

ShieldAI automatically detects and masks:

### Canadian PII Types:
- **Social Insurance Number (SIN)** - 123-456-789
- **Health Card Numbers** - Provincial formats
- **Driver's Licenses** - Provincial formats
- **Postal Codes** - A1A 1A1
- **Phone Numbers** - +1-416-555-1234

### Universal PII Types:
- **Email Addresses** - user@example.com
- **Credit Card Numbers** - 1234-5678-9012-3456
- **IP Addresses** - 192.168.1.1

### Example:

**Input:**
```
"My SIN is 123-456-789 and email is john@example.com"
```

**Masked (sent to AI):**
```
"My SIN is [SIN_REDACTED] and email is [EMAIL_REDACTED]"
```

## Compliance Reporting

Generate compliance reports anytime:

```bash
curl https://api.shieldai.ca/compliance/report \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -X POST
```

Reports include:
- Total requests processed
- PII detections
- Compliance rate (always 100%)
- PIPEDA principle compliance
- Technical safeguards
- Audit trail summary

---

# Security

## Authentication

### API Key Security:
- ✅ Store in environment variables
- ✅ Never commit to version control
- ✅ Rotate regularly
- ✅ Use different keys for dev/prod
- ❌ Never hardcode in source code
- ❌ Never share publicly

### Example (.env file):

```bash
SHIELDAI_API_KEY=tct_yourcompany_abc123xyz456
```

### Example (Python):

```python
import os
from dotenv import load_dotenv

load_dotenv()
api_key = os.getenv("SHIELDAI_API_KEY")
```

## Encryption

- **In Transit:** TLS 1.3
- **At Rest:** AES-256
- **Database:** Encrypted backups

## Access Control

- API key authentication
- Rate limiting
- IP whitelisting (Enterprise)
- Role-based access (Enterprise)

## Monitoring

- Real-time threat detection
- Anomaly detection
- Automated alerts
- 24/7 SOC monitoring

## Compliance Certifications

- ✅ PIPEDA Compliant
- 🔄 SOC 2 Type II (Q2 2025)
- 🔄 ISO 27001 (Q3 2025)
- 🔄 PHIPA Certified (Q3 2025)

---

# Troubleshooting

## Common Issues

### 401 Unauthorized

**Problem:** Invalid API key

**Solution:**
```bash
# Check your API key
echo $SHIELDAI_API_KEY

# Verify it's correct in dashboard
# https://dashboard.shieldai.ca/settings
```

### 429 Rate Limit Exceeded

**Problem:** Too many requests

**Solution:**
- Implement exponential backoff
- Upgrade to higher tier
- Contact support for rate limit increase

### 500 Internal Server Error

**Problem:** Server error

**Solution:**
- Check status page: https://status.shieldai.ca
- Retry with exponential backoff
- Contact support if persists

### Slow Response Times

**Problem:** High latency

**Solution:**
- Check your internet connection
- Verify you're using Canadian servers
- Reduce request size
- Enable caching

## Error Codes

| Code | Meaning | Solution |
|------|---------|----------|
| 400 | Bad Request | Check request format |
| 401 | Unauthorized | Verify API key |
| 403 | Forbidden | Check account status |
| 429 | Rate Limit | Implement backoff |
| 500 | Server Error | Retry or contact support |
| 503 | Service Unavailable | Check status page |

## Getting Help

### Support Channels:

**Email:** support@shieldai.ca
- Response time: <4 hours (business hours)
- 24/7 for Enterprise customers

**Slack:** [Join our community]
- Real-time chat
- Community support
- Product updates

**Phone:** 1-800-SHIELD-AI
- Enterprise customers only
- 24/7 emergency support

**Documentation:** https://docs.shieldai.ca
- Comprehensive guides
- API reference
- Code examples

---

# FAQ

## General

**Q: What is ShieldAI?**
A: ShieldAI is a PIPEDA-compliant AI gateway that enables Canadian enterprises to safely use AI services while maintaining full privacy compliance.

**Q: How is ShieldAI different from using OpenAI directly?**
A: ShieldAI adds a compliance layer that detects and masks PII, logs all requests for audit, and ensures Canadian data residency - all required for PIPEDA compliance.

**Q: Do I need an OpenAI account?**
A: No! ShieldAI handles everything. You only need a ShieldAI account.

**Q: Where is my data stored?**
A: All data is processed and stored in Canada (AWS Montreal region).

**Q: Is ShieldAI PIPEDA compliant?**
A: Yes, 100%. We comply with all 10 PIPEDA principles.

## Technical

**Q: Is ShieldAI compatible with OpenAI's API?**
A: Yes! It's a drop-in replacement. Just change the base URL and API key.

**Q: What AI models are supported?**
A: Currently GPT-3.5-turbo and GPT-4. More models coming soon (Claude, Gemini).

**Q: What's the latency?**
A: Average <200ms overhead. Total response time depends on AI model.

**Q: What's the uptime SLA?**
A: 99.9% uptime guarantee for Professional and Enterprise plans.

**Q: Can I use ShieldAI with my existing code?**
A: Yes! Just change two lines: base URL and API key.

## Pricing

**Q: How much does ShieldAI cost?**
A: Plans start at $2,000/month. See pricing page for details.

**Q: What's included in my plan?**
A: Base fee includes tokens, compliance features, and support. See plan details.

**Q: What happens if I exceed my token limit?**
A: You're charged overage rates ($0.04-0.08 per 1K tokens depending on plan).

**Q: Can I change plans?**
A: Yes, anytime. Upgrades are immediate, downgrades at renewal.

**Q: Do you offer discounts?**
A: Yes! Annual plans get 20% off. Volume discounts available.

## Compliance

**Q: Is ShieldAI PHIPA compliant?**
A: Yes, suitable for healthcare use cases. PHIPA certification in progress.

**Q: Can I use ShieldAI for government projects?**
A: Yes! We meet government data sovereignty requirements.

**Q: How long do you keep audit logs?**
A: 7 years by default (configurable for Enterprise).

**Q: Can I get compliance reports?**
A: Yes, generate anytime via API or dashboard.

**Q: What if there's a data breach?**
A: We have incident response procedures and will notify within 72 hours per PIPEDA.

## Support

**Q: What support do you offer?**
A: Email support for all plans. Phone support for Enterprise. See plan details.

**Q: How fast do you respond?**
A: <4 hours during business hours. <1 hour for Enterprise (24/7).

**Q: Do you offer training?**
A: Yes! Onboarding training included. Additional training available.

**Q: Can you help with integration?**
A: Yes! We provide integration support for all customers.

---

## Need More Help?

📧 **Email:** support@shieldai.ca
📱 **Phone:** 1-800-SHIELD-AI
🌐 **Website:** https://shieldai.ca
💬 **Slack:** [Join our community]

**We're here to help!** 🛡️
