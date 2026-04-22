---
name: Page Structure
description: Mintlify page organization - frontmatter, navigation hierarchy, file structure, and reusable page templates
---

# Mintlify Page Structure Guide

## File System Structure

### Recommended Directory Layout

```
mintlify-docs/
├── docs.json               # Main configuration
├── index.mdx               # Landing page
├── introduction.mdx        # Technical overview
├── favicon.svg             # Site favicon
├── logo/
│   ├── logoDark.svg        # Logo for light mode
│   └── logoWhite.svg       # Logo for dark mode
├── images/                 # All illustrative images
│   └── dashboard.png
├── features/               # Feature documentation
│   ├── analytics.mdx
│   ├── payments.mdx
│   └── users.mdx
├── api-reference/          # API docs (if applicable)
│   ├── authentication.mdx
│   └── endpoints.mdx
└── about/                  # Company/Project info
    ├── team.mdx
    └── roadmap.mdx
```

### Folder Naming Conventions

| Convention | Example |
|------------|---------|
| Lowercase folders | `features/`, `api/`, `about/` |
| Kebab-case for multi-word | `getting-started/` |
| Descriptive names | `features/` not `f/` |

### File Naming Conventions

| Convention | Example |
|------------|---------|
| Lowercase or PascalCase | `analytics.mdx` or `Analytics.mdx` |
| Match docs.json references | If config says `features/analytics`, file is `features/analytics.mdx` |
| No spaces | `getting-started.mdx` not `getting started.mdx` |

---

## Frontmatter

### Required Fields

Every `.mdx` file must have frontmatter:

```mdx
---
title: "Page Title"
description: "Brief description for SEO and previews"
---
```

### Frontmatter Best Practices

| Field | Guidelines |
|-------|------------|
| `title` | 2-4 words, capitalize main words |
| `description` | 10-15 words, one sentence, what the page covers |

### Examples

```mdx
---
title: "Project Overview"
description: "High-level introduction to the platform architecture"
---
```

```mdx
---
title: "Authentication"
description: "How to generate and use API keys securely"
---
```

### What NOT to Include in Frontmatter

- Long paragraphs (keep description to one line)
- HTML or MDX components
- Links
- Complex formatting

---

## Navigation Hierarchy

### Tab → Group → Page

```
Tab: "Documentation"
├── Group: "Getting Started"
│   ├── Page: index
│   └── Page: quickstart
├── Group: "Core Features"
│   ├── Page: features/analytics
│   ├── Page: features/reporting
│   └── Page: features/automation
└── Group: "Company"
    └── Page: about/team
```

### docs.json Navigation Reference

```json
{
  "navigation": {
    "tabs": [
      {
        "tab": "Documentation",
        "groups": [
          {
            "group": "Getting Started",
            "pages": ["index", "quickstart"]
          },
          {
            "group": "Core Features",
            "pages": [
              "features/analytics",
              "features/reporting"
            ]
          }
        ]
      }
    ]
  }
}
```

---

## Page Templates

### 1. Landing Page (index.mdx)

Use this for the root `index.mdx` of your documentation.

```mdx
---
title: "Introduction"
description: "Welcome to the [Project Name] documentation"
---

<img className="block dark:hidden" src="/images/hero-light.png" alt="Hero Light" />
<img className="hidden dark:block" src="/images/hero-dark.png" alt="Hero Dark" />

## Introduction

[Project Name] is a [category] that enables [user type] to [main benefit]. It solves [core problem] by [main solution].

## What [Project Name] Does

<CardGroup cols={2}>
  <Card title="Feature 1" icon="sparkles">
    Brief description of first feature.
  </Card>
  <Card title="Feature 2" icon="chart-mixed">
    Brief description of second feature.
  </Card>
  <Card title="Feature 3" icon="code">
    Brief description of third feature.
  </Card>
  <Card title="Feature 4" icon="shield-check">
    Brief description of fourth feature.
  </Card>
</CardGroup>

## Why It Matters

<Note>
  [Key insight, philosophy, or differentiator]
</Note>

[1-2 sentences explaining why this solution is important/different/better.]

## Core Principles

| Principle | Description |
|-----------|-------------|
| Principle 1 | Brief explanation |
| Principle 2 | Brief explanation |

<Card title="Get Started" icon="rocket" href="/quickstart">
  Install and configure [Project Name] in 5 minutes.
</Card>
```

### 2. Feature Page Template

Use this for documentation pages inside `features/` or `modules/`.

```mdx
---
title: "Feature Name"
description: "One-line summary of what this feature handles"
---

<Card title="Try it Live" icon="play" href="https://app.com/feature">
  Launch the [Feature] demo
</Card>

## Overview

[2-3 sentences: What is this feature? Who is it for? What problem does it solve?]

## Capabilities

[Feature] supports:
- **Capability 1** - Description
- **Capability 2** - Description
- **Capability 3** - Description

## How It Works

<Steps>
  <Step title="Step 1 Title">
    Brief description of what happens.
  </Step>
  <Step title="Step 2 Title">
    Brief description of what happens.
  </Step>
  <Step title="Step 3 Title">
    Brief description of what happens.
  </Step>
</Steps>

## Configuration / Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| param_1 | string | Description of param 1 |
| param_2 | integer | Description of param 2 |

<Note>
  [Helpful tip or edge case to be aware of]
</Note>

## Examples

```javascript
// Example code snippet
const result = await feature.execute({
  param_1: "value",
  param_2: 123
});
```
```

### 3. Technical/Protocol Overview Template

Use this for describing architecture, protocols, or deep-dive technical topics.

```mdx
---
title: "Architecture"
description: "How [Project] works under the hood"
---

## System Overview

[Project] consists of three main components:

1. **Component A** - Description
2. **Component B** - Description
3. **Component C** - Description

## Data Flow

High-level description of how data moves through the system.

## Security Model

description of security guarantees or practices.

<Warning>
  [Important security warning or responsibility]
</Warning>

## Technical Specifications

- **Spec 1**: Value
- **Spec 2**: Value
- **Spec 3**: Value

<Card title="Read API Docs" icon="book" href="/api-reference">
  View the complete API reference.
</Card>
```

### 4. Roadmap Page Template

Use this for `about/roadmap.mdx` or similar status pages.

```mdx
---
title: "Roadmap"
description: "Development phases and upcoming milestones"
---

## Current Status

We are currently in **Phase 2 (Beta)**.

---

## Phase 1: Foundation (Completed)

<Check>
  Core architecture setup
</Check>

<Check>
  Alpha release
</Check>

---

## Phase 2: Expansion (Current)

<Check>
  Public Beta Launch
</Check>

**In Progress:**

- Feature A integration
- Mobile SDK

---

## Phase 3: Scaling (Planned)

| Feature | Status |
|---------|--------|
| Enterprise SSO | Planned |
| Analytics Dashboard | <span style={{ color:"#fbbf24", fontWeight:"bold" }}>Designing</span> |
| Audit Logs | Planned |

---

## Request a Feature

Have an idea? [Submit a request](https://feedback.yourproject.com).
```

### 5. Team Page Template

Use this for `about/team.mdx`.

```mdx
---
title: "Team"
description: "Meet the people building [Project]"
---

## Leadership

<CardGroup cols={2}>
  <Card title="Name" icon="user">
    **Role**
    
    Brief bio or responsibility.
    
    [Twitter](https://x.com/handle) | [Portfolio](https://website.com)
  </Card>
  <Card title="Name" icon="user">
    **Role**
    
    Brief bio or responsibility.
    
    [Twitter](https://x.com/handle)
  </Card>
</CardGroup>

## Mission

<Note>
  [Mission statement]
</Note>

## Values

| Value | Description |
|-------|-------------|
| **Transparency** | We build in public. |
| **User First** | We obsess over UX. |
```

---

## Page Order Guidelines

### Recommended Group Order

1. **Getting Started** - Installation, Quickstart
2. **Core Features** - The meat of the product
3. **Advanced / Technical** - Architecture, deeper config
4. **Reference** - API, CLI commands
5. **Company / About** - Team, Roadmap, Legal

### Within Each Group

Order pages from:
1. Most important / most used
2. Entry point for new users (e.g., "Overview" before "Configuration")
3. Supplementary / reference pages last

---

## Common Page Structure Mistakes

| ❌ Mistake | ✅ Fix |
|-----------|-------|
| No frontmatter | Add title and description |
| Title too long | Keep to 2-4 words |
| Description is a paragraph | Make it one sentence |
| Pages don't match docs.json | Sync file paths with config |
| Inconsistent page depth | Keep similar pages at same folder level |
| Missing index.mdx | Every docs needs a landing page |
