# ShieldAI Integration Guide

Welcome to ShieldAI! This guide will help you integrate in 5 minutes.

---

## 🔑 Your Credentials

**API Key:** `[YOU'LL FILL THIS IN]`
**Endpoint:** `http://localhost:8002/v1` (or your deployed URL)

⚠️ **Keep your API key secure!** Never commit it to version control.

---

## 🚀 Quick Start

### Python

```python
import openai

# Configure ShieldAI
openai.api_base = "http://localhost:8002/v1"
openai.api_key = "YOUR_API_KEY_HERE"

# Make request
response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[
        {"role": "user", "content": "Hello from ShieldAI!"}
    ]
)

print(response.choices[0].message.content)
```

### Node.js

```javascript
const { Configuration, OpenAIApi } = require("openai");

const configuration = new Configuration({
  apiKey: "YOUR_API_KEY_HERE",
  basePath: "http://localhost:8002/v1"
});

const openai = new OpenAIApi(configuration);

const response = await openai.createChatCompletion({
  model: "gpt-3.5-turbo",
  messages: [{role: "user", content: "Hello from ShieldAI!"}]
});

console.log(response.data.choices[0].message.content);
```

### cURL

```bash
curl http://localhost:8002/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY_HERE" \
  -d '{
    "model": "gpt-3.5-turbo",
    "messages": [{"role": "user", "content": "Hello!"}]
  }'
```

---

## ✅ What ShieldAI Does

1. **Detects PII** - Automatically finds sensitive data
2. **Masks PII** - Redacts before sending to AI
3. **Logs Everything** - Complete audit trail
4. **Canadian Data** - All processing in Canada
5. **PIPEDA Compliant** - Full compliance guaranteed

---

## 📊 Check Your Usage

Contact your account manager or check your monthly invoice.

---

## 🆘 Need Help?

- **Email:** support@shieldai.ca
- **Phone:** [Your phone]
- **Documentation:** [Your docs URL]

---

## 🎉 You're Ready!

Start making AI requests safely and compliantly!
