---
name: clean-and-simple-mintlify
description: "Master guide for creating ultra-clean, minimalist, and highly realistic Mintlify documentation. Focuses on premium aesthetics, realistic content generation, avoiding bloat, and the 'Havn-style' approach to developer docs (500+ line extended edition)."
---

# Clean and Simple Mintlify Guide

This module details how to create documentation that feels like a multi-million-dollar tech company (like Stripe or Havn Finance) built it. It emphasizes restraint, realistic API design, and highly curated aesthetics over simply dumping text onto a page.

## 1. The Core Philosophy

### Less is More
Modern developer documentation should not require endless scrolling. Content should be dense, technical, and restricted to maximum `80vh` to `100vh` per section whenever possible. 

### "Fake" but Real
When prototyping or designing without a live backend, the content must be indistinguishable from a production system. 
* **Never use:** `"id": "123"`
* **Instead use:** `"id": "crd_8f7b2c9a1e3d4f5b"`

## 2. Global Aesthetics & the Hero Image

The foundation of a premium Mintlify site is a restrained color palette and a striking welcoming image.

### The Home Page Hero Rule
The root `index.mdx` of your documentation is the first thing users see. It must establish brand authority immediately. 

**RULE:** Always place a large `<img />` or markdown image directly under the frontmatter of your `index.mdx` file.

```mdx
---
title: "The Vision"
description: "Bridging DeFi and traditional commerce."
icon: "bolt"
---

<img src="/logo/dark.svg" alt="Brand Logo" className="hidden dark:block mb-8 rounded-xl" />
<img src="/logo/light.svg" alt="Brand Logo" className="block dark:hidden mb-8 rounded-xl" />

# The Protocol
Welcome to the documentation...
```
*Note the use of Tailwind classes `hidden dark:block` to show different images based on the user's theme.*

---

## 3. The Perfect `docs.json` Implementation

Your `docs.json` file controls everything. A chaotic config file leads to chaotic documentation. Below is the **exact** structure you should use to achieve the Havn-style minimalist approach.

<Note>
Notice the use of `anchors` for secondary links, a singular `primary` CTA in the navbar, and the `tabs` structure for separating Documentation from the API Reference.
</Note>

```json docs.json
{
  "$schema": "https://mintlify.com/docs.json",
  "theme": "mint",
  "name": "Havn Finance",
  "logo": {
    "light": "/logo/light.svg",
    "dark": "/logo/dark.svg"
  },
  "favicon": "/favicon.svg",
  "colors": {
    "primary": "#0055FF",
    "light": "#3377FF",
    "dark": "#002266"
  },
  "appearance": {
    "default": "dark"
  },
  "navigation": {
    "global": {
      "anchors": [
        {
          "anchor": "Website",
          "icon": "laptop",
          "href": "https://havn.finance"
        },
        {
          "anchor": "Twitter",
          "icon": "x-twitter",
          "href": "https://x.com/havnfi"
        }
      ]
    },
    "tabs": [
      {
        "tab": "Documentation",
        "groups": [
          {
            "group": "HAVN VISION",
            "pages": [
              "index"
            ]
          },
          {
            "group": "HAVN PROTOCOL",
            "pages": [
              "protocol/what-is-havn",
              "protocol/how-it-works",
              "protocol/features"
            ]
          },
          {
            "group": "CARD ECOSYSTEM",
            "pages": [
              "cards/types",
              "cards/tiers",
              "cards/integration"
            ]
          },
          {
            "group": "ABOUT US",
            "pages": [
              "about/privacy"
            ]
          }
        ]
      },
      {
        "tab": "API Reference",
        "groups": [
          {
            "group": "Introduction",
            "pages": [
              "api-reference/introduction"
            ]
          },
          {
            "group": "Card Operations",
            "pages": [
              "api-reference/endpoint/create-card",
              "api-reference/endpoint/list-cards",
              "api-reference/endpoint/transactions",
              "api-reference/endpoint/freeze-card"
            ]
          },
          {
            "group": "Wallet Operations",
            "pages": [
              "api-reference/endpoint/get-wallet"
            ]
          }
        ]
      }
    ]
  },
  "navbar": {
    "primary": {
      "type": "button",
      "label": "Get Your Card",
      "href": "https://havn.finance"
    }
  },
  "footer": {
    "socials": {
      "x": "https://x.com/havnfi",
      "website": "https://havn.finance"
    }
  }
}
```

---

## 4. Writing Realistic Technical Content

When filling out the "About" or "Features" pages, avoid generic lorem ipsum. Write dense, technical prose that sounds like it was written by an engineer.

### Example: The Dense MDX Pattern

Here is the **exact** source code of a premium `features.mdx` page. Study how it uses the Mintlify `<Steps>` component instead of bullet points, and how it embeds Markdown tables for data density.

```mdx features.mdx
---
title: "Features & Architecture"
description: "Technical overview of the non-custodial gateway and routing engine."
icon: "microchip"
---

# Technical Architecture

The platform is architected to seamlessly bridge decentralized liquidity pools with fiat settlement networks globally. By minimizing intermediary steps, we achieve sub-second execution for stablecoins and major L1 assets.

## The Routing Engine

Our custom smart contract routing engine is deployed across EVM-compatible networks and Solana.

### Transaction Lifecycle

<Steps>
  <Step title="Quote Generation">
    Upon receiving a top-up request, our frontend queries aggregated off-chain oracle prices (Chainlink, Pyth) against real-time DEX liquidity (Jupiter, Uniswap) to secure a fixed conversion rate valid for 30 seconds.
  </Step>
  <Step title="Asset Locking">
    The user signs a transaction sending the exact crypto amount to a single-use deterministic smart contract vault.
  </Step>
  <Step title="JIT Conversion">
    Sub-second Just-In-Time (JIT) execution converts the volatile asset (if applicable) against stablecoin deep liquidity.
  </Step>
  <Step title="Fiat Ledger Settlement">
    The stablecoin is settled via institutional API with our banking partner, immediately reflecting the fiat balance on the virtual card ledger via webhooks.
  </Step>
</Steps>

## Deep Liquidity Integration

We utilize advanced Smart Order Routing (SOR) algorithms to minimize slippage, particularly for high-tier card funding operations.

### Cross-Chain Capabilities

| Network | Principal Aggregator | Average Finality |
| :--- | :--- | :--- |
| **Solana** | Jupiter (JUP) | < 400ms |
| **Ethereum** | Uniswap / 1inch | ~ 12s |
| **Polygon (PoS)** | QuickSwap / 1inch | ~ 2s |
| **Base** | Aerodrome | ~ 2s |

## Security & Compliance Model

Security is paramount in financial bridging infrastructure. We inherently limit total value locked (TVL) risks by operating purely as a gateway rather than an AMM or lending protocol.

### Smart Contract Protections

* **No Proxy Upgradability on Vaults:** Funding vaults are immutable, ensuring logic cannot be maliciously altered mid-transaction.
* **Slippage Tolerance Checks:** All on-chain conversions fail/revert if the execution price deviates outside the strictly defined SLA threshold (0.5% max).
* **Timelocked Funds:** If fiat settlement via the banking partner API times out or fails, smart contracts have a built-in 24-hour timelock, after which funds become directly withdrawable by the originating wallet.

### Non-Custodial Assurances

Because we do not use multi-sig wallets for holding user deposits, there is zero platform counterparty risk regarding the crypto assets. **Your keys, your crypto.** Funds exist either strictly under your self-custody or are instantly materialized as fiat purchasing power on the authorized banking ledger.
```

---

## 5. Crafting the Perfect API Reference

The API reference is where a documentation site is truly judged. Mintlify's `<ParamField>` and `<ResponseField>` components must be used rigorously.

### Endpoint Structure Rules
Every endpoint page should follow this exact hierarchy:
1. `api` frontmatter string (e.g., `"GET https://api.domain.com/v1/resource"`)
2. `### Authorization` section (Bearer tokens)
3. `### Path Parameters` (if applicable)
4. `### Query Parameters` (if applicable)
5. `### Body Parameters` (if applicable)
6. `### Response` overview
7. `<RequestExample>` covering at least cURL and one Language (Node.js/Python)
8. `<ResponseExample>` covering 200 Success and at least one relevant Error code (400, 401, 403, 404).

### Example: The POST Endpoint Pattern

Here is the **exact source code** required to build a world-class API endpoint documentation page for a hypothetical `create-card` route. Notice the precision of the variable names and the exactness of the JSON response block.

```mdx create-card.mdx
---
title: "Provision Card"
api: "POST https://api.havn.finance/v1/cards"
description: "Provision a new virtual Visa® or Mastercard® using decentralized assets."
---

### Authorization

<ParamField header="Authorization" type="string" required>
  Bearer token. Format: `Bearer <token>`
</ParamField>

### Body Parameters

<ParamField body="network" type="string" required>
  The source blockchain network name.
  
  **Options:** `solana`, `ethereum`, `polygon`, `base`, `optimism`
</ParamField>

<ParamField body="asset" type="string" required>
  The ticker of the asset you intend to fund with.
  
  **Options:** `SOL`, `ETH`, `USDC`, `USDT`, `BTC`
</ParamField>

<ParamField body="cardType" type="string" default="visa">
  The desired virtual card network credential.
  
  **Options:** `visa`, `mastercard`
</ParamField>

<ParamField body="fundingAmount" type="number" required>
  The USD value you wish to load onto the card. Our Oracle will generate the exact crypto equivalent required. Minimum: `10.00`.
</ParamField>

### Response

<ResponseField name="cardId" type="string">
  Unique internal identifier for the card provisioning request. Format: `crd_<16 chars>`
</ResponseField>

<ResponseField name="depositAddress" type="string">
  The single-use deterministic smart contract address where you must send the crypto assets.
</ResponseField>

<ResponseField name="requiredAmount" type="number">
  The exact amount of the specified crypto asset required (calculated by the Oracle).
</ResponseField>

<ResponseField name="status" type="string">
  Current provisioning status. Values: `awaiting_deposit`, `converting`, `provisioned`, `failed`
</ResponseField>

<ResponseField name="expiresAt" type="string">
  ISO 8601 timestamp indicating when this quote/deposit address expires (usually 15-30 minutes).
</ResponseField>

<RequestExample>
```bash cURL
curl --request POST \
  --url https://api.havn.finance/v1/cards \
  --header 'Authorization: Bearer havn_live_abc123def456' \
  --header 'Content-Type: application/json' \
  --data '{
    "network": "solana",
    "asset": "SOL",
    "cardType": "visa",
    "fundingAmount": 500.00
  }'
```

```javascript Node.js
const response = await fetch('https://api.havn.finance/v1/cards', {
  method: 'POST',
  headers: {
    'Authorization': `Bearer ${process.env.HAVN_API_KEY}`,
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    network: 'solana',
    asset: 'SOL',
    cardType: 'visa',
    fundingAmount: 500.00
  })
});
const data = await response.json();
```
</RequestExample>

<ResponseExample>
```json 200 - Success
{
  "cardId": "crd_8f7b2c9a1e3d4f5b",
  "depositAddress": "7xKXtg2CW87d97TXJSDpbD5jBkheTqA83TZRuJosgAsU",
  "requiredAmount": 3.42910,
  "status": "awaiting_deposit",
  "expiresAt": "2026-03-01T14:30:00Z"
}
```

```json 400 - Validation Error
{
  "error": "invalid_asset",
  "message": "The asset 'DOGE' is not currently supported for funding."
}
```
</ResponseExample>
```

### The "Has More" Pagination Pattern
For listing endpoints (e.g., returning arrays of cards or transactions), always include pagination parameters in the request (`limit`, `startingAfter`) and pagination context in the response (`hasMore: boolean`). This proves you understand backend scalability.

Here is the exact code snippet for a professional GET list endpoint.

```mdx transactions.mdx
---
title: "Get Transactions"
api: "GET https://api.havn.finance/v1/cards/{cardId}/transactions"
description: "Retrieve a paginated history of fiat authorizations on a specific virtual card."
---

### Authorization

<ParamField header="Authorization" type="string" required>
  Bearer token. Format: `Bearer <token>`
</ParamField>

### Path Parameters

<ParamField path="cardId" type="string" required>
  The unique identifier of the virtual card (returned during the `POST /v1/cards` provisioning call).
  Format: `crd_<16 chars>`
</ParamField>

### Query Parameters

<ParamField query="limit" type="number" default="20">
  Maximum number of transactions to return per page. Max: 100.
</ParamField>

<ParamField query="startingAfter" type="string">
  A cursor for use in pagination. `startingAfter` is an object ID that defines your place in the list.
</ParamField>

### Response

<ResponseField name="data" type="array">
  List of transaction objects.
</ResponseField>

<ResponseField name="hasMore" type="boolean">
  Whether there are more transactions available beyond this page.
</ResponseField>

### Transaction Object Attributes

<ResponseField name="id" type="string">
  Unique transaction identifier. Format: `txn_<12 chars>`
</ResponseField>

<ResponseField name="amount" type="number">
  The USD fiat amount authorized/settled.
</ResponseField>

<ResponseField name="merchant" type="string">
  The merchant descriptor from the Visa® or Mastercard® network.
</ResponseField>

<ResponseField name="status" type="string">
  Status of the transaction. Values: `pending`, `settled`, `declined`, `refunded`
</ResponseField>

<ResponseField name="createdAt" type="string">
  ISO 8601 timestamp of the authorization.
</ResponseField>

<RequestExample>
```bash cURL
curl --request GET \
  --url 'https://api.havn.finance/v1/cards/crd_8f7b2c9a1e3d4f5b/transactions?limit=2' \
  --header 'Authorization: Bearer havn_live_abc123def456'
```
</RequestExample>

<ResponseExample>
```json 200 - Success
{
  "data": [
    {
      "id": "txn_84jf902nf4kd",
      "amount": 14.99,
      "merchant": "NETFLIX.COM",
      "status": "settled",
      "createdAt": "2026-02-15T08:12:44Z"
    },
    {
      "id": "txn_1nfb9g48dbk7",
      "amount": 298.50,
      "merchant": "APPLE STORE R102",
      "status": "pending",
      "createdAt": "2026-02-18T14:30:11Z"
    }
  ],
  "hasMore": true
}
```

```json 403 - Forbidden
{
  "error": "insufficient_permissions",
  "message": "This API key does not have the 'read:cards' scope."
}
```
</ResponseExample>
```

---

## Summary Checklist for "Clean" Mintlify
1. [ ] Place a `<img />` Hero block right beneath the `index.mdx` frontmatter.
2. [ ] Check `docs.json` for a restrained (non-neon) 3-tier color palette.
3. [ ] Ensure the Navbar has only ONE primary CTA button.
4. [ ] Verify secondary links are tucked into Global Anchors in the sidebar.
5. [ ] Check every `.mdx` file for an `icon:` in the frontmatter.
6. [ ] Audit all JSON examples for realistic IDs (`ch_123`, `txn_abc`), strict ISO-8601 dates, and precise decimal math.
7. [ ] Confirm no single page scrolls infinitely (aim for 80vh-100vh chunks).
8. [ ] Ensure lists use the `<Steps>` component instead of bullet points where things imply a sequence or progression.
