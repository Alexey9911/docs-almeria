---
name: Component Patterns
description: Mintlify component usage patterns - Cards, CardGroups, Steps, Notes, Warnings, Tables, and layout techniques
---

# Mintlify Component Patterns

## Available Components

| Component | Use For |
|-----------|---------|
| `<Card>` | Feature highlights, navigation links, CTAs |
| `<CardGroup>` | Grouping multiple cards in columns |
| `<Steps>` | Sequential processes, how-to guides |
| `<Note>` | Helpful context, tips |
| `<Warning>` | Critical info, risks, incomplete features |
| `<Check>` | Completed items in roadmaps |
| Tables | Feature specs, fee structures, comparisons |

---

## Cards

### Basic Card

```mdx
<Card title="Feature Name" icon="paper-plane">
  Short description of the feature.
</Card>
```

### Card with Link

```mdx
<Card title="Continue Reading" icon="arrow-right" href="/next-page">
  Learn more about this topic.
</Card>
```

### CTA Card (Call-to-Action)

Place at the top of feature pages to drive users to try the feature:

```mdx
<Card title="Try App" icon="rocket" href="https://yourapp.com">
  Launch the Dashboard now
</Card>
```

**Best Practice**: One CTA card at the top, one navigation card at the bottom.

### Card Icons

Common icons from Font Awesome:

| Icon | Use For |
|------|---------|
| `paper-plane` | Send, messaging |
| `users` | Teams, distribution |
| `broom` | Clean up, sweep |
| `ghost` | Brand, main app |
| `code` | Development, tech |
| `shield` | Security, protection |
| `server` | Infrastructure |
| `flask` | R&D, experiments |
| `crown` | Leadership, founder |
| `arrow-right` | Navigation, continue |
| `arrow-trend-up` | Growth, business |
| `rocket` | Launch, get started |
| `desktop` | UI, frontend |

### Custom Icon Styling

```mdx
<Card title="Custom Icon" icon="star" iconType="solid" color="#FFD700">
  Custom colored icon with solid style.
</Card>
```

---

## CardGroup

### Two Columns

Standard layout for feature pairs:

```mdx
<CardGroup cols={2}>
  <Card title="Analysis" icon="chart-simple">
    Visual analytics for your data.
  </Card>
  <Card title="Reporting" icon="file-invoice">
    Automated daily reports.
  </Card>
</CardGroup>
```

### Three Columns

For compact feature overviews:

```mdx
<CardGroup cols={3}>
  <Card title="Build" icon="hammer">
    Create new resources
  </Card>
  <Card title="Deploy" icon="cloud-arrow-up">
    Push to production
  </Card>
  <Card title="Monitor" icon="gauge">
    Track performance
  </Card>
</CardGroup>
```

### Single Column (Wide Cards)

For detailed feature descriptions:

```mdx
<CardGroup cols={1}>
  <Card title="Enterprise Security">
    SSO enforcement, audit logs, and role-based access control.
  </Card>
  <Card title="Automatic Compliance">
    SOC2 and HIPAA compliance controls included by default.
  </Card>
</CardGroup>
```

### Multiple CardGroups (Stacked)

For larger teams or feature sets, stack multiple CardGroups:

```mdx
<CardGroup cols={2}>
  <Card title="Feature A" icon="star">First pair</Card>
  <Card title="Feature B" icon="heart">First pair</Card>
</CardGroup>

<CardGroup cols={2}>
  <Card title="Feature C" icon="bell">Second pair</Card>
  <Card title="Feature D" icon="bolt">Second pair</Card>
</CardGroup>
```

---

## Steps

### Basic Steps

Perfect for "How it works" sections:

```mdx
## How It Works

<Steps>
  <Step title="Create Account">
    Sign up and verify your email address.
  </Step>
  <Step title="Configure API">
    Generate your API key and set permissions.
  </Step>
  <Step title="Make Request">
    Send your first request to the endpoints.
  </Step>
  <Step title="View Results">
    Analyze the response data in your dashboard.
  </Step>
</Steps>
```

### Step Content Guidelines

| Guideline | Example |
|-----------|---------|
| Title: Action verb + object | "Select Asset" or "Configure API" |
| Description: 1-2 sentences | What the user does or what happens |
| Keep technical details minimal | Save deep dives for other sections |

---

## Notes and Warnings

### Note (General Information)

Use for helpful context, tips, or important caveats:

```mdx
<Note>
  You can override these settings at the user level.
</Note>

<Note>
  Free tier accounts are limited to 1,000 requests per day.
</Note>
```

### Warning (Critical Information)

Use for risks, incomplete features, or legal disclaimers:

```mdx
<Warning>
  Deleting an environment is permanent and cannot be undone.
</Warning>

<Warning>
  This API endpoint is deprecated and will be removed in v2.0.
</Warning>
```

### When to Use Each

| Use Note For | Use Warning For |
|--------------|-----------------|
| Tips and best practices | Missing features ("coming soon") |
| Clarifications | Legal disclaimers |
| Fee exemptions | Risks or important considerations |
| Technical context | Things that could cause loss |

---

## Tables

### Feature Specifications

```mdx
| Feature | Detail |
|---------|--------|
| Supported Formats | JSON, XML, CSV |
| Max File Size | 50 MB |
| Retention | 30 Days |
```

### Fee Structure (with Notes in Cells)

```mdx
| Tier | Pricing |
|------|---------|
| Hobby | Free for personal use |
| Pro | $29/mo <br />(includes priority support) |
| Enterprise | Custom pricing |
```

### Roadmap Status Table

```mdx
| Feature | Status |
|---------|--------|
| User Auth | <span style={{ color:"#22c55e", fontWeight:"bold" }}>Live</span> |
| Payment Gateway | Beta |
| Mobile App | Planned |
```

---

## Check Component (Roadmap)

For completed milestones:

```mdx
## Phase 1: Foundation

<Check>
  Core architecture setup
</Check>

<Check>
  Alpha release
</Check>
```

For in-progress items, use plain text or markdown:

```mdx
**In Progress:**

- Integration tests
- Documentation updates
```

---

## Images

### Hero Image (Full Width)

```mdx
<div style={{ textAlign: 'center', marginBottom: '2rem' }}>
  <img 
    src="/width-image.png" 
    alt="Product dashboard screenshot" 
    style={{ width: '100%', maxWidth: '1500px' }} 
  />
</div>
```

### Image Best Practices

| Guideline | Reason |
|-----------|--------|
| Use descriptive alt text | Accessibility and SEO |
| Set maxWidth | Prevent huge images on wide screens |
| Center images | Cleaner visual hierarchy |
| Put in /images folder | Keep root clean |

---

## Layout Patterns

### Feature Page Structure

```mdx
---
title: "Feature Name"
description: "One-line description"
---

<Card title="Try [Feature]" icon="relevant-icon" href="https://app.com/feature">
  Launch the [Feature] feature now
</Card>

## Main Heading

Brief overview paragraph (2-3 sentences).

## How [Feature] Works

<Steps>
  <Step title="Step 1">Description</Step>
  <Step title="Step 2">Description</Step>
</Steps>

## Key Features / Capabilities

| Feature | Detail |
|---------|--------|

## Pricing / Usage Limits

| Tier | Limit |
|------|-------|

<Note>
  Helpful note.
</Note>

## Technical Details

- **Feature 1**: Description
- **Feature 2**: Description
```

### Overview Page Structure

```mdx
---
title: "Product Name"
description: "Tagline"
---

<div>(Hero image if applicable)</div>

## Introduction

2-3 sentences about what the product is and what it does.

## What [Product] Does

<CardGroup cols={1}>
  <Card title="Feature 1">Description</Card>
  <Card title="Feature 2">Description</Card>
</CardGroup>

## Why It Matters

<Note>
  Key insight or philosophy.
</Note>

Brief explanation paragraph.

## Core Principles

| Principle | Description |
|-----------|-------------|

<Card title="Continue Reading" icon="arrow-right" href="/next">
  Learn how it works.
</Card>
```

### Team Page Structure

```mdx
## Meet The Team

One-line description.

<CardGroup cols={2}>
  <Card title="Name" icon="crown">
    **Role**
    
    Description of what they do.
    
    [Follow on X](https://x.com/handle)
  </Card>
  (more team cards)
</CardGroup>

## Our Mission

<Note>
  Mission statement.
</Note>

Brief paragraph.

## Connect With The Team

Link list to social profiles.
```

---

## Common Mistakes

| ❌ Mistake | ✅ Fix |
|-----------|-------|
| Too many icons per page | Use 3-4 distinct icons max |
| Cards with no href | Add navigation or remove if static |
| Notes that are paragraphs | Keep to 1-2 sentences |
| Inconsistent icon choices | Pick an icon set and stick to it |
| Steps with 10+ items | Split into multiple sections |
| Tables with empty cells | Use "N/A" or restructure |
