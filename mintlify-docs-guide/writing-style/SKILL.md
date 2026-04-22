---
name: Writing Style Guide
description: Universal professional writing patterns for Mintlify docs - realistic tone, concise language, and avoiding marketing speak
---

# Writing Style Guide for Mintlify Documentation

## The Core Problem This Solves

Most documentation sounds either:
- **Too marketing-y**: "Revolutionary groundbreaking solution that transforms everything!"
- **Too boring**: Dry, robotic text that puts users to sleep
- **Fake**: Overpromising features, vague claims, buzzword soup

This guide shows how to write like **a skilled engineer explaining their work to a peer** — confident, precise, and honest. This applies to **any project**, whether it's crypto, SaaS, open source, or enterprise software.

---

## The Golden Rules

### 1. Realistic Over Marketing

| ❌ Fake/Marketing | ✅ Realistic/Professional |
|------------------|--------------------------|
| "Revolutionary privacy solution" | "Privacy-first payment routing layer" |
| "Game-changing technology" | "Zero-knowledge proofs protecting transaction metadata" |
| "Unlock the power of..." | "Enable users to [action]..." |
| "Seamless, frictionless experience" | "Complete the flow in 5 steps" |

### 2. Concise Over Verbose

Every sentence should earn its place. If you can say it in fewer words, do it.

| ❌ Wordy | ✅ Concise |
|---------|-----------|
| "Our platform is a revolutionary new system that enables users to..." | "Our platform enables users to..." |
| "The user will be able to utilize this feature to..." | "Use this feature to..." |
| "This allows you to be able to..." | "This lets you..." |

### 3. Technical Credibility

Use precise terminology. If it's ZK proofs, say ZK proofs. If it's an API wrapper, say API wrapper. Don't dumb it down to the point of being wrong.

```mdx
<!-- ❌ Vague -->
Our advanced technology keeps your data safe.

<!-- ✅ Technical -->
AES-256 encryption protects all data at rest and in transit.
```

### 4. Neutral Confidence

State facts confidently without overselling. Let the feature speak for itself.

```mdx
<!-- ❌ Overselling -->
The BEST solution in the ENTIRE ecosystem!

<!-- ✅ Neutral confidence -->
[Product] provides [feature] using [technology].
```

---

## Sentence Structure Patterns

### For Introductions (First Sentence)

**Pattern**: `[Product/Feature] is [what it is] for [who/what purpose].`

```mdx
<!-- ✅ Good examples -->
Ghost Link is a privacy-first payment routing layer built on Solana.
NextJS is a React framework for production-grade applications.
Stripe Connect is the fastest way to integrate payments into your platform.
```

### For Feature Descriptions

**Pattern**: `[What it does]. Perfect for [use case].`

```mdx
<!-- ✅ Good examples -->
Distribute is used to fund bulk wallets. Perfect for airdrops, payroll, and mass payments.
Hot Reloading instantly updates your UI. Perfect for rapid development cycles.
```

### For Technical Explanations

**Pattern**: `[How it works] — [why it matters].`

```mdx
<!-- ✅ Good examples -->
All guarantees are enforced cryptographically, replacing the need for trust.
Data is cached at the edge, reducing latency for global users.
```

---

## Word Choice Reference

### Words to USE

| Good Word | Context |
|-----------|---------|
| **enables** | "Enables [functionality]" |
| **provides** | "Provides [benefit]" |
| **supports** | "Supports [platforms/assets]" |
| **validates** | "Validates inputs without..." |
| **allows** | "Allows you to [action]" |
| **maintains** | "Maintains [state/security]" |
| **optimizes** | "Optimizes [metric]" |

### Words to AVOID

| ❌ Avoid | Why | ✅ Use Instead |
|---------|-----|----------------|
| Revolutionary | Overused, sounds marketing | (describe what it actually does) |
| Game-changing | Vague, no meaning | (explain the specific improvement) |
| Seamless | Everyone says this | "In X steps" or describe the actual flow |
| Frictionless | Same as seamless | Describe what was removed |
| Unlock the power | Meaningless | (just explain the feature) |
| Next-gen | Empty buzzword | (explain the actual technology) |
| Best-in-class | Unprovable claim | (omit or use specific metrics) |
| Synergy | Corporate speak | (describe the actual relationship) |

---

## Content Length Guidelines

### Page Introductions
- **2-3 sentences max**
- Explain what, who for, and why it matters

```mdx
<!-- ✅ Good length -->
## Feature Name

[Feature] is the core module for [function]. Perfect for [user type] who needs to [goal].
```

### Section Descriptions
- **1-2 sentences**
- Get to the point immediately

```mdx
<!-- ✅ Good length -->
## Supported Formats

The API supports the following data formats:
- **JSON** - Standard REST response
- **XML** - Legacy support
- **CSV** - For bulk data exports
```

### Card Descriptions
- **1 sentence**
- Maximum 15-20 words

```mdx
<!-- ✅ Good length -->
<Card title="Authentication">
  Learn how to generate API keys and authenticate requests.
</Card>

<!-- ❌ Too long -->
<Card title="Authentication">
  In this section, we will cover everything you need to know about how to 
  properly authenticate your requests using our secure API key system 
  so that you can access your data.
</Card>
```

### Note/Warning Content
- **1-2 sentences**
- Should feel like a helpful aside, not a paragraph

```mdx
<!-- ✅ Good -->
<Note>
  Rate limits apply to all free tier accounts.
</Note>
```

---

## Realistic Tone Examples

### Describing Limitations (Don't Hide Them)

Good documentation acknowledges limitations honestly:

```mdx
| Parameter | Value |
|-----------|-------|
| Max Requests | 100 per minute |
| Retention | 30 days |
| Latency | ~50ms (typical) |
```

### Describing Fees (Be Transparent)

Don't bury fees. State them clearly:

```mdx
## Pricing

| Tier | Cost |
| ---- | ---- |
| Free | $0/mo |
| Pro  | $29/mo |
| Team | $99/mo |
```

### Describing What's Not Ready Yet

Be honest about development status:

```mdx
<Warning>
  This feature is currently in Beta. API methods may change.
</Warning>

**Coming Soon:**
- Mobile SDK
- GraphQL support
```

---

## Common Mistakes and Fixes

| ❌ Mistake | ✅ Fix |
|-----------|-------|
| Starting with "Welcome to..." | Start with what the product does |
| Using "we" too much | Use product name or focus on user ("you can...") |
| Explaining why users should care | Show it through features, don't tell |
| Empty superlatives | Replace with specific capabilities |
| Repeating the same info | State once, reference elsewhere |
| Overusing exclamation marks | Almost never use them |

---

## Testing Your Writing

Before publishing, ask:

1. **Would an engineer be embarrassed to share this?** If yes, it's too marketing-y
2. **Can I delete any words without losing meaning?** If yes, delete them
3. **Does every claim have a backing feature?** If not, remove the claim
4. **Would a skeptic roll their eyes?** If yes, tone it down
5. **Is this what actually happens?** If not, fix it or remove it

---

## Reference Examples

### Good Introduction
```mdx
[Product] is a [category] built for [platform]. It enables [function] without 
requiring [trade-off].
```

### Good Feature Summary
```mdx
[Feature] enables [capability]. Configure, deploy, and monitor [assets] without 
leaving the dashboard.
```

### Good Note
```mdx
<Note>
  [Product] does not store your private keys. You are responsible for backup.
</Note>
```

### Good Limitation Statement
```mdx
| Feature | Limit |
| ------- | ----- |
| Max File Size | 50 MB |
| Concurrent Jobs | 5 |
```
