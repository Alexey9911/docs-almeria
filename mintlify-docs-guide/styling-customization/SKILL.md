---
name: Styling Customization
description: docs.json configuration - colors, logos, navbar, anchors, footer, hover effects, and button positioning
---

# Mintlify Styling Customization

## docs.json Configuration

The `docs.json` file controls all visual styling and navigation structure.

---

## Core Configuration

### Basic Setup

```json
{
  "$schema": "https://mintlify.com/docs.json",
  "theme": "mint",
  "name": "Your Project Name"
}
```

**Available Themes**: `mint`, `maple`, `palm`, `willow`, `linden`, `almond`, `aspen`

---

## Colors

### Color Schema

```json
{
  "colors": {
    "primary": "#YOUR_BRAND_COLOR",
    "light": "#YOUR_LIGHT_COLOR",
    "dark": "#YOUR_DARK_COLOR"
  }
}
```

| Property | Purpose | Example |
|----------|---------|---------|
| `primary` | Main accent color (buttons, links) | `#9CA3AF` (gray) |
| `light` | Light mode accent | `#6B7280` (darker gray) |
| `dark` | Dark mode background | `#1A1A1A` (near black) |

### Professional Color Schemes

**Neutral/Professional (Clean):**
```json
{
  "colors": {
    "primary": "#64748b",
    "light": "#94a3b8",
    "dark": "#0f172a"
  }
}
```

**Blue/Tech (Trustworthy):**
```json
{
  "colors": {
    "primary": "#3B82F6",
    "light": "#60A5FA",
    "dark": "#1E3A5F"
  }
}
```

**Green/Success (Growth):**
```json
{
  "colors": {
    "primary": "#10B981",
    "light": "#34D399",
    "dark": "#064E3B"
  }
}
```

**Purple/Premium (Creative):**
```json
{
  "colors": {
    "primary": "#8B5CF6",
    "light": "#A78BFA",
    "dark": "#1E1B4B"
  }
}
```

---

## Appearance

### Default Theme Mode

```json
{
  "appearance": {
    "default": "dark"
  }
}
```

Options: `"dark"` or `"light"`

---

## Logo Configuration

### Light and Dark Mode Logos

```json
{
  "logo": {
    "light": "/logoDark.svg",
    "dark": "/logoWhite.svg",
    "height": 120
  }
}
```

| Property | Purpose |
|----------|---------|
| `light` | Logo shown in light mode (usually dark-colored logo) |
| `dark` | Logo shown in dark mode (usually light-colored logo) |
| `height` | Logo height in pixels |

### Logo Best Practices

| Guideline | Reason |
|-----------|--------|
| Use SVG format | Crisp at any size |
| Keep height 80-120px | Fits navbar well |
| Include both variants | Looks professional in both modes |
| Place in `/logo` folder or root | Easy to find |

---

## Favicon

```json
{
  "favicon": "/favicon.svg"
}
```

SVG favicons work best for modern browsers.

---

## Navbar

### Primary CTA Button

The main call-to-action button in the top-right corner:

```json
{
  "navbar": {
    "primary": {
      "type": "button",
      "label": "Try App",
      "href": "https://yourapp.com"
    }
  }
}
```

This creates a prominent button that stands out from other nav items.

### Additional Navbar Links

```json
{
  "navbar": {
    "links": [
      {
        "label": "Community",
        "href": "https://discord.gg/yourlink"
      }
    ],
    "primary": {
      "type": "button",
      "label": "Sign Up",
      "href": "https://yourapp.com/signup"
    }
  }
}
```

---

## Global Anchors (Corner Buttons)

### What Are Anchors?

Anchors are persistent navigation buttons that appear in the **sidebar corners** throughout the docs. Perfect for:
- Main app link ("Dashboard")
- Social media (Twitter/X)
- Community links (Discord, Telegram)

### Anchor Configuration

```json
{
  "navigation": {
    "global": {
      "anchors": [
        {
          "anchor": "Dashboard",
          "icon": "globe",
          "href": "https://yourapp.com/login"
        },
        {
          "anchor": "Twitter",
          "icon": "x-twitter",
          "href": "https://x.com/YourHandle"
        }
      ]
    }
  }
}
```

### Common Anchor Icons

| Icon | Use For |
|------|---------|
| `ghost` | Brand/main app |
| `rocket` | Launch/App |
| `x-twitter` | Twitter/X |
| `discord` | Discord server |
| `telegram` | Telegram group |
| `github` | GitHub repo |
| `link` | Generic link |

### Anchor Positioning

Anchors appear in order from top to bottom in the sidebar. Position your most important link first.

---

## Footer

### Social Links

```json
{
  "footer": {
    "socials": {
      "x": "https://x.com/Yourhandle",
      "github": "https://github.com/your-org",
      "discord": "https://discord.gg/yourlink"
    }
  }
}
```

### Available Social Platforms

| Key | Platform |
|-----|----------|
| `x` | Twitter/X |
| `twitter` | Twitter (legacy) |
| `telegram` | Telegram |
| `discord` | Discord |
| `github` | GitHub |
| `linkedin` | LinkedIn |
| `youtube` | YouTube |
| `instagram` | Instagram |
| `website` | Custom website |

---

## Navigation Structure

### Tabs

Tabs are top-level navigation sections:

```json
{
  "navigation": {
    "tabs": [
      {
        "tab": "Documentation",
        "groups": [
          {
            "group": "Introduction",
            "pages": ["index", "quickstart"]
          }
        ]
      },
      {
        "tab": "API Reference",
        "groups": [...]
      }
    ]
  }
}
```

### Groups Within Tabs

Groups are sidebar sections within a tab:

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
            "group": "Core Concepts",
            "pages": [
              "concepts/authentication",
              "concepts/rate-limits"
            ]
          },
          {
            "group": "Resources",
            "pages": [
              "resources/faq",
              "resources/support"
            ]
          }
        ]
      }
    ]
  }
}
```

### Navigation Best Practices

| Guideline | Reason |
|-----------|--------|
| 3-5 groups max per tab | Prevents overwhelming sidebar |
| 2-6 pages per group | Easy to scan |
| Use logical ordering | Users can predict where things are |
| First page = most important | It's the entry point |

---

## SEO Configuration

```json
{
  "seo": {
    "indexHiddenPages": false
  }
}
```

---

## Complete docs.json Example

```json
{
  "$schema": "https://mintlify.com/docs.json",
  "theme": "mint",
  "name": "Project Name",
  "colors": {
    "primary": "#3B82F6",
    "light": "#60A5FA",
    "dark": "#1E3A5F"
  },
  "favicon": "/favicon.svg",
  "navigation": {
    "global": {
      "anchors": [
        {
          "anchor": "Dashboard",
          "icon": "rocket",
          "href": "https://app.com"
        },
        {
          "anchor": "Reference",
          "icon": "book",
          "href": "https://api.app.com"
        }
      ]
    },
    "tabs": [
      {
        "tab": "Documentation",
        "groups": [
          {
            "group": "Getting Started",
            "pages": ["index", "quickstart"]
          },
          {
            "group": "Features",
            "pages": [
              "features/auth",
              "features/database"
            ]
          }
        ]
      }
    ]
  },
  "logo": {
    "light": "/logoDark.svg",
    "dark": "/logoWhite.svg",
    "height": 120
  },
  "navbar": {
    "links": [
      {
        "label": "Support",
        "href": "https://support.app.com"
      }
    ],
    "primary": {
      "type": "button",
      "label": "Sign Up",
      "href": "https://app.com/signup"
    }
  },
  "footer": {
    "socials": {
      "x": "https://x.com/handle",
      "github": "https://github.com/org",
      "website": "https://app.com"
    }
  },
  "appearance": {
    "default": "dark"
  }
}
```

---

## Custom Inline Styling

### Colored Status Text

```mdx
<span style={{ color:"#22c55e", fontWeight:"bold" }}>Live</span>
```

### Centered Content

```mdx
<div style={{ textAlign: 'center', marginBottom: '2rem' }}>
  Content here
</div>
```

### Images with Max Width

```mdx
<img 
  src="/image.png" 
  alt="Description" 
  style={{ width: '100%', maxWidth: '1500px' }} 
/>
```

---

## Hover Effects and Interactivity

Mintlify handles hover effects automatically for:
- Cards (slight lift and shadow)
- Links (color change)
- Buttons (color/opacity change)

The `primary` color in your config determines these hover states.

### Custom Hover via Theme

The theme you choose (`mint`, `quill`, etc.) determines hover behavior. For more control, you may need custom CSS which requires Mintlify Enterprise.

---

## Common Customization Mistakes

| ❌ Mistake | ✅ Fix |
|-----------|-------|
| Missing dark mode logo | Add `logo.dark` |
| Colors too similar | Ensure contrast between primary/light/dark |
| Too many anchors | Limit to 2-3 essential links |
| Inconsistent capitalization in nav | Keep page names consistent |
| Broken page references | Ensure paths match actual file locations |
