---
name: sdk-reference-guide
description: "Guide for creating realistic SDK documentation with TypeScript interfaces, Python examples, WebSocket streaming, and developer tools. For comprehensive developer documentation."
---

# SDK Reference Documentation Guide

Create professional SDK documentation that looks production-ready. Includes TypeScript interfaces, Python SDK patterns, WebSocket streaming, and CLI tools.

## SDK Documentation Structure

```
/whitepaper/developer/
├── quickstart.mdx      # Getting started
├── sdk.mdx             # Full SDK reference
├── tools.mdx           # CLI, extensions, webhooks
└── toolkits.mdx        # Pre-built integrations
```

---

## Quickstart Page Template

```mdx
---
title: "Quickstart"
description: "Get started with the SDK in under 5 minutes"
icon: "rocket"
---

## Installation

<CodeGroup>
```bash npm
npm install @yourproject/sdk
```

```bash yarn
yarn add @yourproject/sdk
```

```bash pnpm
pnpm add @yourproject/sdk
```

```bash pip
pip install yourproject-sdk
```
</CodeGroup>

## Initialize the Client

<CodeGroup>
```typescript TypeScript
import { YourProject } from '@yourproject/sdk';

const client = new YourProject({
  apiKey: process.env.YOUR_API_KEY,
  network: 'mainnet-beta'
});
```

```python Python
from yourproject import YourProject

client = YourProject(
    api_key=os.environ['YOUR_API_KEY'],
    network='mainnet-beta'
)
```
</CodeGroup>

## Your First Request

<CodeGroup>
```typescript TypeScript
// Track a wallet
const wallet = await client.wallet.track('7xKXtg2CW87d97TXJSDpbD5jBkheTqA83TZRuJosgAsU');

console.log(`Balance: ${wallet.balance} SOL`);
console.log(`Token Accounts: ${wallet.tokenAccounts}`);
```

```python Python
# Track a wallet
wallet = client.wallet.track('7xKXtg2CW87d97TXJSDpbD5jBkheTqA83TZRuJosgAsU')

print(f"Balance: {wallet.balance} SOL")
print(f"Token Accounts: {wallet.token_accounts}")
```
</CodeGroup>

## Response Format

All SDK methods return typed objects with consistent structure:

```typescript
interface WalletTrackingData {
  address: string;
  balance: number;
  tokenAccounts: number;
  nftCount: number;
  lastActivity: string;
  riskScore: number;
  tags: string[];
}
```

<Note>
  The SDK automatically handles rate limiting, retries, and error normalization.
</Note>
```

---

## SDK Reference Page Template

```mdx
---
title: "SDK Reference"
description: "Complete SDK documentation for all modules and methods"
icon: "code"
---

## Overview

The SDK provides a type-safe interface to all platform capabilities:

<CardGroup cols={2}>
  <Card title="Wallet Module" icon="wallet" href="#wallet-module">
    Track addresses, query transactions, monitor balances
  </Card>
  <Card title="Analytics Module" icon="chart-line" href="#analytics-module">
    Predictions, anomaly detection, pattern analysis
  </Card>
  <Card title="Agent Module" icon="robot" href="#agent-module">
    Deploy, configure, and manage AI agents
  </Card>
  <Card title="Streaming" icon="bolt" href="#websocket-streaming">
    Real-time updates via WebSocket
  </Card>
</CardGroup>

## Configuration Options

```typescript
interface ClientConfig {
  apiKey: string;
  network?: 'mainnet-beta' | 'devnet' | 'testnet';
  rpcEndpoint?: string;
  timeout?: number;        // Default: 30000ms
  retryAttempts?: number;  // Default: 3
  debug?: boolean;         // Default: false
}
```

---

## Wallet Module

### wallet.track(address)

Start tracking a wallet address for real-time updates and analytics.

**Parameters:**
- `address` - Valid Solana wallet address (base58 encoded)

**Returns:** `Promise<WalletTrackingData>`

```typescript
const wallet = await client.wallet.track('7xKXtg2CW87d97TXJSDpbD5jBkheTqA83TZRuJosgAsU');
```

**Response Type:**

```typescript
interface WalletTrackingData {
  address: string;
  balance: number;
  tokenAccounts: number;
  nftCount: number;
  lastActivity: string;  // ISO 8601
  riskScore: number;     // 0-100
  tags: string[];
}
```

---

### wallet.getTransactions(address, options)

Retrieve transaction history for an address.

**Parameters:**

```typescript
interface TransactionOptions {
  limit?: number;             // Max 1000
  offset?: number;
  order?: 'asc' | 'desc';
  startTime?: number;         // Unix timestamp
  endTime?: number;
  type?: 'all' | 'transfer' | 'swap' | 'stake';
}
```

**Example:**

```typescript
const transactions = await client.wallet.getTransactions(
  '7xKXtg2CW87d97TXJSDpbD5jBkheTqA83TZRuJosgAsU',
  { limit: 50, type: 'swap', order: 'desc' }
);

for (const tx of transactions) {
  console.log(`${tx.signature}: ${tx.type} - ${tx.amount} SOL`);
}
```

---

### wallet.getTokenAccounts(address)

Get all SPL token accounts for an address.

**Returns:** `Promise<TokenAccount[]>`

```typescript
interface TokenAccount {
  mint: string;
  balance: number;
  decimals: number;
  uiAmount: number;
  symbol: string;
  name: string;
  logoUri?: string;
}
```

---

## Analytics Module

### analytics.getPrediction(address)

Get behavior prediction for a wallet.

```typescript
const prediction = await client.analytics.getPrediction(
  '7xKXtg2CW87d97TXJSDpbD5jBkheTqA83TZRuJosgAsU'
);
```

**Response Type:**

```typescript
interface Prediction {
  address: string;
  nextTransactionProbability: number;  // 0-1
  estimatedTimeToNext: number;         // seconds
  likelyAction: 'buy' | 'sell' | 'transfer' | 'stake';
  confidence: number;                  // 0-1
  factors: string[];
}
```

---

### analytics.getAnomalies(address, timeRange)

Detect unusual activity patterns.

```typescript
const anomalies = await client.analytics.getAnomalies(
  '7xKXtg2CW87d97TXJSDpbD5jBkheTqA83TZRuJosgAsU',
  { start: Date.now() - 86400000, end: Date.now() }
);
```

---

## WebSocket Streaming

Subscribe to real-time updates for addresses:

```typescript
const stream = client.wallet.subscribe(address);

stream.on('transaction', (tx: Transaction) => {
  console.log('New TX:', tx.signature);
});

stream.on('balance', (balance: number) => {
  console.log('Balance:', balance);
});

stream.on('token', (token: TokenUpdate) => {
  console.log('Token update:', token);
});

stream.on('error', (err: Error) => {
  console.error('Stream error:', err);
});

// Cleanup
stream.close();
```

---

## Rate Limits

| Tier | Requests/min | WebSocket Connections |
|------|-------------|----------------------|
| Free | 60 | 2 |
| Pro | 300 | 10 |
| Enterprise | 1,000 | 100 |

---

## Python SDK

The Python SDK mirrors the TypeScript API:

```python
from yourproject import YourProject

client = YourProject(
    api_key="your_api_key",
    network="mainnet-beta"
)

# Track wallet
wallet = client.wallet.track("7xKXtg2CW87d97TXJSDpbD5jBkheTqA83TZRuJosgAsU")
print(wallet.balance)

# Get transactions
transactions = client.wallet.get_transactions(
    wallet.address,
    limit=50
)

for tx in transactions:
    print(f"{tx.signature}: {tx.type}")
```

---

## Error Codes

| Code | Description | Resolution |
|------|-------------|------------|
| `INVALID_ADDRESS` | Malformed wallet address | Verify base58 encoding |
| `RATE_LIMITED` | Request limit exceeded | Implement backoff |
| `NETWORK_ERROR` | RPC connection failed | Check endpoint status |
| `AUTH_FAILED` | Invalid API key | Verify credentials |
```

---

## CLI Tools Page Template

```mdx
---
title: "Tools"
description: "Developer tools for building and managing your integration"
icon: "wrench"
---

## CLI Tool

<CodeGroup>
```bash npm
npm install -g @yourproject/cli
```

```bash homebrew
brew install yourproject
```
</CodeGroup>

### Authentication

```bash
yourproject auth login
```

### Commands

| Command | Description |
|---------|-------------|
| `yourproject agents list` | List all deployed agents |
| `yourproject agents deploy <config>` | Deploy from config file |
| `yourproject wallet track <address>` | Start tracking a wallet |
| `yourproject analytics report <address>` | Generate analytics report |
| `yourproject config set <key> <value>` | Update configuration |

**Example:**

```bash
$ yourproject agents list

ID                      NAME                    STATUS    MARKET CAP
agent_abc123def456      Trading Strategy        active    10,234 SOL
agent_xyz789ghi012      Meme Analyzer           active    5,847 SOL
agent_mno345pqr678      Portfolio Manager       paused    12,893 SOL
```

---

## Browser Extension

Real-time wallet insights directly in your browser.

### Features

- Wallet risk scoring on any Solana address
- Transaction notifications
- Token analytics overlay
- One-click tracking activation

### Installation

1. Download from [Chrome Web Store](#) or [Firefox Add-ons](#)
2. Click the extension icon
3. Enter your API key
4. Navigate to any Solana explorer

---

## Webhook Integration

Receive real-time events via HTTP webhooks.

### Setup

```bash
yourproject webhooks create \
  --url https://your-server.com/webhook \
  --events transaction,balance,alert \
  --secret your_webhook_secret
```

### Event Types

| Event | Trigger |
|-------|---------|
| `transaction` | New transaction detected |
| `balance` | Balance change > threshold |
| `alert` | Risk score spike |
| `agent.status` | Agent status change |

### Webhook Payload

```json
{
  "id": "evt_1a2b3c4d5e",
  "type": "transaction",
  "timestamp": "2023-11-07T05:31:56Z",
  "data": {
    "address": "7xKXtg2CW87d97TXJSDpbD5jBkheTqA83TZRuJosgAsU",
    "signature": "5VERv8NMvzbJMEkV8xnrLkEaWRtSz9CosKDYjCJjBRnbJLgp8uirBgmQpjKhoR4tjF3ZpRzrFmBV6UjKdiSZkQUW",
    "type": "swap",
    "amount": 125.47,
    "token": "SOL"
  }
}
```

### Security

Verify webhook signatures:

```typescript
import crypto from 'crypto';

function verifyWebhook(payload: string, signature: string, secret: string): boolean {
  const expected = crypto
    .createHmac('sha256', secret)
    .update(payload)
    .digest('hex');
  
  return crypto.timingSafeEqual(
    Buffer.from(signature),
    Buffer.from(expected)
  );
}
```

---

## GraphQL Playground

Access the interactive GraphQL explorer at:

```
https://api.yourproject.io/graphql
```

### Example Query

```graphql
query WalletAnalytics($address: String!) {
  wallet(address: $address) {
    balance
    tokenAccounts {
      symbol
      uiAmount
    }
    recentTransactions(limit: 10) {
      signature
      type
      timestamp
    }
    analytics {
      riskScore
      prediction {
        likelyAction
        confidence
      }
    }
  }
}
```

---

## Testing Sandbox

Use the devnet environment for testing:

```typescript
const client = new YourProject({
  apiKey: 'test_key_1234567890',
  network: 'devnet'
});
```

<Note>
  Devnet requests don't count against your rate limits.
</Note>

---

## Postman Collection

Import our pre-built collection:

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/xxx)

Or download: [yourproject-api.postman_collection.json](#)
```

---

## Key Patterns for Realism

### TypeScript Interfaces

Always define clear, typed interfaces:

```typescript
// Good - precise types
interface Transaction {
  signature: string;
  blockTime: number;
  slot: number;
  type: 'transfer' | 'swap' | 'stake' | 'nft';
  status: 'confirmed' | 'finalized' | 'failed';
  fee: number;
  accounts: string[];
}

// Bad - vague types
interface Transaction {
  id: any;
  data: object;
  info: string;
}
```

### Method Signatures

```typescript
// Good - clear parameters and return types
wallet.getTransactions(address: string, options?: TransactionOptions): Promise<Transaction[]>

// Good - overloaded signatures for flexibility
analytics.query(address: string): Promise<BasicAnalytics>
analytics.query(address: string, options: AdvancedOptions): Promise<DetailedAnalytics>
```

### Error Types

```typescript
class YourProjectError extends Error {
  code: string;
  statusCode: number;
  details?: Record<string, any>;
}

// Usage
try {
  await client.wallet.track(address);
} catch (error) {
  if (error instanceof YourProjectError) {
    console.log(`Error ${error.code}: ${error.message}`);
  }
}
```
