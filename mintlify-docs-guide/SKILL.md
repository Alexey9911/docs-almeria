---
name: mintlify-docs-guide
description: "Complete guide for creating professional Mintlify documentation for ANY project. Covers writing style, realistic tone, component usage, styling customization, navigation structure, and best practices. Use when building or improving documentation sites with Mintlify."
---

# Mintlify Documentation Guide

Comprehensive skill for creating professional, realistic, and polished documentation using Mintlify for **any project**. This guide uses the Ghost Link documentation as a "Gold Standard" reference implementation for style and realism, but the principles apply universally.

## Contents

| Subfolder | Description |
|-----------|-------------|
| [writing-style](./writing-style/SKILL.md) | Universal writing dialect, tone, word choice, and avoiding fake-sounding content |
| [component-patterns](./component-patterns/SKILL.md) | Standard Mintlify patterns: Card, CardGroup, Steps, Note, Warning, Tables |
| [styling-customization](./styling-customization/SKILL.md) | Configuring docs.json, generic color schemes, and professional branding |
| [page-structure](./page-structure/SKILL.md) | Reusable page templates for Features, About, Roadmaps, and more content |
| [api-reference](./api-reference/SKILL.md) | **NEW** OpenAPI endpoints, realistic fake APIs, authentication, error handling |
| [sdk-reference](./sdk-reference/SKILL.md) | **NEW** TypeScript interfaces, Python SDK, WebSocket streaming, CLI tools |
| [extended-docs](./extended-docs/SKILL.md) | **NEW** Multi-page navigation, many categories, content filling techniques |

## Quick Reference

### Writing Principles (The Core Philosophy)

| Principle | Description |
|-----------|-------------|
| **Realistic Over Marketing** | Sound like an engineer explaining, not marketing selling |
| **Concise Over Verbose** | Every sentence should earn its place |
| **Technical Credibility** | Use precise terms, not vague buzzwords |
| **Neutral Confidence** | State facts confidently without overselling |

### docs.json Essential Structure

```json
{
  "$schema": "https://mintlify.com/docs.json",
  "theme": "mint",
  "name": "Your Project",
  "colors": {
    "primary": "#YOUR_COLOR",
    "light": "#YOUR_LIGHT_COLOR", 
    "dark": "#YOUR_DARK_COLOR"
  },
  "appearance": {
    "default": "dark"
  },
  "navbar": {
    "primary": {
      "type": "button",
      "label": "Try App",
      "href": "https://yourapp.com"
    }
  },
  "navigation": {
    "global": {
      "anchors": [
        {
          "anchor": "Try App",
          "icon": "ghost",
          "href": "https://yourapp.com"
        }
      ]
    },
    "tabs": [
      {
        "tab": "Documentation",
        "groups": [
          {
            "group": "Overview",
            "pages": ["index", "protocol"]
          }
        ]
      }
    ]
  }
}
```

### MDX Frontmatter

```mdx
---
title: "Feature Name"
description: "One-line description that appears in search and previews"
---
```

---

## When to Apply This Skill

Use this skill when:
- Creating new Mintlify documentation for **any client or project**
- Restructuring existing documentation to look more professional
- Writing new pages for specific features, tokens, or about sections
- Configuring docs.json for custom navigation and branding
- Adding interactive components (Cards, Steps, Notes)
- Making the documentation sound professional and realistic (not "fake")

---

## Core Components Quick Reference

### Cards

```mdx
<Card title="Feature Name" icon="paper-plane" href="/feature-page">
  Short description of what users can do here.
</Card>
```

### Card Groups

```mdx
<CardGroup cols={2}>
  <Card title="First" icon="code">Description</Card>
  <Card title="Second" icon="shield">Description</Card>
</CardGroup>
```

### Steps

```mdx
<Steps>
  <Step title="Configure Settings">
    Set your preferences and parameters.
  </Step>
  <Step title="Execute Action">
    Run the main process.
  </Step>
</Steps>
```

### Notes and Warnings

```mdx
<Note>
  Important context that helps users understand something.
</Note>

<Warning>
  Critical information about risks or requirements.
</Warning>
```

### Tables

```mdx
| Parameter | Value |
|-----------|-------|
| Max Items | 50    |
| Min Value | 0.001 |
```

### Checkmarks (Roadmap)

```mdx
<Check>
  Completed milestone item
</Check>
```

---

## Reference Examples (from Ghost Link)

While these files are from a specific project, use them as **structural templates**:

- [docs.json](file:///d:/Alexey/threeJS%20journey/DEV-CRYPTO/ghostlink/whitepaper/mintlify-docs/docs.json) - Main configuration example
- [features/send.mdx](file:///d:/Alexey/threeJS%20journey/DEV-CRYPTO/ghostlink/whitepaper/mintlify-docs/features/send.mdx) - Feature documentation pattern
- [about/Team.mdx](file:///d:/Alexey/threeJS%20journey/DEV-CRYPTO/ghostlink/whitepaper/mintlify-docs/about/Team.mdx) - Team page pattern
