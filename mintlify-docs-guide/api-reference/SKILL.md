---
name: api-reference-guide
description: "Complete guide for creating realistic, professional API Reference documentation in Mintlify. Covers OpenAPI integration, endpoint structure, code examples, response schemas, and authentication patterns."
---

# API Reference Documentation Guide

Create fake but realistic API Reference documentation that looks professional and functional. The goal is documentation that appears production-ready even without a working backend.

## Core Principles

### What Makes API Docs Look Real

1. **Consistent naming conventions** - Use snake_case for JSON, camelCase for JS/TS
2. **Realistic IDs and addresses** - Use proper formats (UUIDs, Solana addresses, etc.)
3. **Meaningful defaults** - Choose values that make sense in context
4. **Standard HTTP patterns** - Follow REST conventions strictly
5. **Error handling** - Include realistic error responses

### What to Avoid

| ❌ Don't | ✅ Do Instead |
|----------|--------------|
| Generic placeholder IDs: `"id": "123"` | Realistic IDs: `"id": "agent_abc123def456"` |
| Round numbers: `"balance": 1000` | Precise values: `"balance": 1847.293` |
| Invalid addresses: `"wallet": "abc123"` | Valid format: `"address": "7xKXtg2CW87d97TXJSDpbD5jBkheTqA83TZRuJosgAsU"` |
| Fake dates: `"date": "2024-01-01"` | ISO 8601: `"createdAt": "2023-11-07T05:31:56Z"` |
| Made-up status codes | Real HTTP codes: 200, 201, 400, 401, 403, 404, 429, 500 |

---

## docs.json Structure for API Reference

```json
{
  "navigation": {
    "tabs": [
      {
        "tab": "API Reference",
        "groups": [
          {
            "group": "Core Endpoints",
            "pages": [
              "api-reference/authentication",
              "api-reference/agents/deploy",
              "api-reference/agents/list",
              "api-reference/agents/get"
            ]
          },
          {
            "group": "Wallet Operations",
            "pages": [
              "api-reference/wallet/track",
              "api-reference/wallet/transactions",
              "api-reference/wallet/balance"
            ]
          },
          {
            "group": "Analytics",
            "pages": [
              "api-reference/analytics/predict",
              "api-reference/analytics/anomalies"
            ]
          }
        ]
      }
    ]
  }
}
```

---

## OpenAPI Endpoint Page Template

Use Mintlify's OpenAPI integration for automatic endpoint documentation:

```mdx
---
title: "Deploy Agent"
api: "POST https://api.yourproject.io/v1/agents/deploy"
description: "Deploy a new tokenized AI Agent to the marketplace"
---

### Authorization

<ParamField header="Authorization" type="string" required>
  JWT Bearer token. Format: `Bearer <token>`
</ParamField>

### Body Parameters

<ParamField body="name" type="string" required>
  Display name for the agent. Max 64 characters.
</ParamField>

<ParamField body="category" type="string" required>
  Category classification.
  
  **Options:** `trading`, `analytics`, `social`, `gaming`, `defi`, `nft`, `automation`
</ParamField>

<ParamField body="model" type="string" default="gpt-4">
  AI model to power the agent.
  
  **Options:** `gpt-4`, `gpt-3.5-turbo`, `claude-3`, `llama-2`
</ParamField>

<ParamField body="initialSupply" type="integer" required>
  Total token supply for the agent. Range: 1,000 - 1,000,000,000
</ParamField>

<ParamField body="description" type="string">
  Agent description. Max 500 characters.
</ParamField>

<ParamField body="capabilities" type="array">
  List of capability identifiers.
  
  Example: `["price_analysis", "portfolio_management", "risk_assessment"]`
</ParamField>

<ParamField body="pricePerToken" type="number" required>
  Initial token price in SOL. Min: 0.0001
</ParamField>

<ParamField body="revenueShare" type="number" default="0.3">
  Percentage of revenue shared with token holders. Range: 0.0 - 1.0
</ParamField>

### Response

<ResponseField name="agentId" type="string">
  Unique agent identifier. Format: `agent_<12 chars>`
</ResponseField>

<ResponseField name="name" type="string">
  Agent display name
</ResponseField>

<ResponseField name="tokenAddress" type="string">
  Solana SPL token address (base58)
</ResponseField>

<ResponseField name="marketCap" type="number">
  Current market capitalization in SOL
</ResponseField>

<ResponseField name="holders" type="integer">
  Number of unique token holders
</ResponseField>

<ResponseField name="status" type="string">
  Agent status. Values: `active`, `paused`, `deprecated`
</ResponseField>

<ResponseField name="deployedAt" type="string">
  ISO 8601 deployment timestamp
</ResponseField>

<RequestExample>
```bash cURL
curl --request POST \
  --url https://api.yourproject.io/v1/agents/deploy \
  --header 'Authorization: Bearer <token>' \
  --header 'Content-Type: application/json' \
  --data '{
    "name": "Trading Strategy Agent",
    "category": "trading",
    "model": "gpt-4",
    "initialSupply": 1000000,
    "description": "Automated DeFi trading agent with risk management",
    "capabilities": [
      "price_analysis",
      "portfolio_management",
      "risk_assessment"
    ],
    "pricePerToken": 0.01,
    "revenueShare": 0.3
  }'
```

```javascript JavaScript
const response = await fetch('https://api.yourproject.io/v1/agents/deploy', {
  method: 'POST',
  headers: {
    'Authorization': `Bearer ${apiKey}`,
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    name: 'Trading Strategy Agent',
    category: 'trading',
    model: 'gpt-4',
    initialSupply: 1000000,
    description: 'Automated DeFi trading agent with risk management',
    capabilities: ['price_analysis', 'portfolio_management', 'risk_assessment'],
    pricePerToken: 0.01,
    revenueShare: 0.3
  })
});
```

```python Python
import requests

response = requests.post(
    'https://api.yourproject.io/v1/agents/deploy',
    headers={
        'Authorization': f'Bearer {api_key}',
        'Content-Type': 'application/json'
    },
    json={
        'name': 'Trading Strategy Agent',
        'category': 'trading',
        'model': 'gpt-4',
        'initial_supply': 1000000,
        'description': 'Automated DeFi trading agent with risk management',
        'capabilities': ['price_analysis', 'portfolio_management', 'risk_assessment'],
        'price_per_token': 0.01,
        'revenue_share': 0.3
    }
)
```
</RequestExample>

<ResponseExample>
```json 200 - Success
{
  "agentId": "agent_abc123def456",
  "name": "Trading Strategy Agent",
  "tokenAddress": "7xKXtg2CW87d97TXJSDpbD5jBkheTqA83TZRuJosgAsU",
  "marketCap": 10000,
  "holders": 1,
  "status": "active",
  "deployedAt": "2023-11-07T05:31:56Z"
}
```

```json 400 - Bad Request
{
  "error": "validation_error",
  "message": "initialSupply must be between 1000 and 1000000000",
  "field": "initialSupply"
}
```

```json 401 - Unauthorized
{
  "error": "invalid_token",
  "message": "The provided authentication token is invalid or expired"
}
```
</ResponseExample>
```

---

## Realistic Data Patterns

### IDs and Addresses

```javascript
// Agent/Resource IDs
"agentId": "agent_abc123def456"
"userId": "user_9f8e7d6c5b4a"
"txId": "tx_1a2b3c4d5e6f"

// Solana addresses (44 chars, base58)
"address": "7xKXtg2CW87d97TXJSDpbD5jBkheTqA83TZRuJosgAsU"
"mint": "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v"

// Transaction signatures (88 chars)
"signature": "5VERv8NMvzbJMEkV8xnrLkEaWRtSz9CosKDYjCJjBRnbJLgp8uirBgmQpjKhoR4tjF3ZpRzrFmBV6UjKdiSZkQUW"

// UUIDs
"sessionId": "550e8400-e29b-41d4-a716-446655440000"
```

### Timestamps

```javascript
// Always use ISO 8601
"createdAt": "2023-11-07T05:31:56Z"
"updatedAt": "2023-11-07T14:22:33.847Z"
"expiresAt": "2024-01-15T00:00:00Z"

// Unix timestamps for internal use
"timestamp": 1699335116
"startTime": 1698768000
```

### Numeric Values

```javascript
// Balances - use realistic precision
"balance": 1847.293847
"available": 892.15
"locked": 955.143847

// Percentages
"confidence": 0.847
"feeRate": 0.003
"share": 0.25

// Counts
"totalTransactions": 15847
"holders": 342
"activeUsers": 1293
```

---

## Authentication Section

Always include a dedicated authentication page:

```mdx
---
title: "Authentication"
description: "Learn how to authenticate with the API"
---

## API Keys

All API requests require authentication via Bearer token in the Authorization header.

```bash
Authorization: Bearer your_api_key_here
```

### Obtaining API Keys

1. Navigate to the [Developer Dashboard](https://app.yourproject.io/developers)
2. Create a new API key with appropriate permissions
3. Store the key securely - it will only be shown once

<Warning>
  Never expose your API key in client-side code or public repositories.
</Warning>

### Key Permissions

| Scope | Description |
|-------|-------------|
| `read:agents` | View agent details and configurations |
| `write:agents` | Create, update, and deploy agents |
| `read:wallet` | Access wallet tracking data |
| `read:analytics` | Access prediction and analysis endpoints |
| `admin` | Full account access |

### Rate Limits

| Tier | Requests/min | Requests/day |
|------|-------------|--------------|
| Free | 60 | 1,000 |
| Pro | 300 | 50,000 |
| Enterprise | 1,000 | Unlimited |

<Note>
  Rate limit headers are included in every response:
  - `X-RateLimit-Limit`
  - `X-RateLimit-Remaining`
  - `X-RateLimit-Reset`
</Note>
```

---

## Error Responses Template

Include consistent error response patterns:

```mdx
---
title: "Error Handling"
description: "API error codes and handling"
---

## Error Response Format

All errors follow a consistent structure:

```json
{
  "error": "error_code",
  "message": "Human-readable error description",
  "details": {}  // Optional additional context
}
```

## Error Codes

| Code | HTTP Status | Description |
|------|-------------|-------------|
| `validation_error` | 400 | Invalid request parameters |
| `invalid_token` | 401 | Authentication token is invalid or expired |
| `insufficient_permissions` | 403 | Token lacks required scopes |
| `not_found` | 404 | Requested resource does not exist |
| `rate_limit_exceeded` | 429 | Too many requests |
| `internal_error` | 500 | Server-side error |

## Retry Strategy

For transient errors (429, 500, 502, 503, 504), implement exponential backoff:

```typescript
async function fetchWithRetry(url: string, options: RequestInit, maxRetries = 3) {
  for (let attempt = 0; attempt < maxRetries; attempt++) {
    try {
      const response = await fetch(url, options);
      
      if (response.status === 429) {
        const retryAfter = response.headers.get('Retry-After') || '1';
        await sleep(parseInt(retryAfter) * 1000);
        continue;
      }
      
      if (response.status >= 500) {
        await sleep(Math.pow(2, attempt) * 1000);
        continue;
      }
      
      return response;
    } catch (error) {
      if (attempt === maxRetries - 1) throw error;
      await sleep(Math.pow(2, attempt) * 1000);
    }
  }
}
```
```

---

## Metrics and Analytics Endpoints

Use technical metric names that sound real:

```javascript
// Good metric names
"engagement_rate": 0.0847
"viral_score": 72.4
"sentiment_analysis": { "positive": 0.65, "neutral": 0.28, "negative": 0.07 }
"follower_growth": 1247
"influence_score": 84.3
"liquidity_depth": 45892.47
"slippage_estimate": 0.0012
"whale_activity_index": 0.34
"smart_money_flow": 892341.87
"holder_concentration": 0.23
"token_velocity": 4.7

// Good analytics response
{
  "address": "7xKXtg2CW87d97TXJSDpbD5jBkheTqA83TZRuJosgAsU",
  "period": "24h",
  "metrics": {
    "transactionCount": 847,
    "volumeIn": 15234.89,
    "volumeOut": 12847.23,
    "uniqueCounterparties": 234,
    "avgTransactionSize": 17.98,
    "largestTransaction": 2500.00
  },
  "riskIndicators": {
    "score": 23,
    "flags": ["high_frequency", "new_address"],
    "confidence": 0.89
  }
}
```

---

## Tips for Realistic Feel

1. **Version your API** - Always use `/v1/`, `/v2/` in URLs
2. **Include pagination** - Add `limit`, `offset`, `cursor` params
3. **Add metadata** - Include `total`, `page`, `hasMore` in list responses
4. **Use proper HTTP verbs** - GET, POST, PUT, PATCH, DELETE appropriately
5. **Include request IDs** - Add `X-Request-ID` header mentions
6. **Document webhooks** - Show event payloads with realistic data
7. **Show SDK examples** - Multiple languages (cURL, JS, Python, Go)
