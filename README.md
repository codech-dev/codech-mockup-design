# Codech Mockup Design

A Claude Code plugin for structured design ideation and visual prototyping. Creates design system documents and self-contained HTML showcases that render live in any browser — no build step needed.

## What it does

This plugin provides a 7-phase design workflow that produces two artifacts per design direction:

1. **Design System Document** (`design-system.md`) — tokens, principles, component patterns, accessibility rules
2. **Visual Showcase** (`design-showcase.html`) — a single self-contained HTML file that renders every token, screen, and component live

The showcase is the primary deliverable. Open it in any browser and scroll through to judge the design.

## The workflow

| Phase | What happens |
|---|---|
| **1. Gather intelligence** | Query product type, audience, competitors, emotional register. Integrates with `ui-ux-pro-max` skill for data-driven design decisions. |
| **2. Write design system** | Create a markdown doc with 8 required sections: philosophy, colors, typography, spacing, radius/shadows, motion, component patterns, accessibility. |
| **3. Build showcase HTML** | Generate a self-contained HTML file with Tailwind CDN, Google Fonts, CSS custom properties, scroll-reveal animations, and full-page screen mockups. |
| **4. Present & iterate** | Show the user which file to open, call out specific things to evaluate, collect feedback. |
| **5. Multiple directions** | Create genuinely different alternatives — not just color swaps. Each version must differ on 5+ of 7 differentiation axes. |
| **6. Lock & reference** | Finalize the approved direction, link it from implementation plans, commit to git. |
| **7. Interactive prototype** *(optional)* | Spin up a Vite + React + shadcn + Framer Motion app with real animations, working components, and page routing. |

## When it triggers

The skill activates when you say things like:

- "Design the UI for..."
- "Create a mockup of the dashboard"
- "What should the landing page look like?"
- "Explore different visual directions"
- "Build a design system"
- "Show me a prototype"

Works for any project type: landing pages, dashboards, mobile apps, SaaS products, marketplaces, portfolios, admin panels, e-commerce stores.

## The "identically different" rule

When creating multiple design versions, every version must be **identically different** — not a reskin with swapped colors. This is enforced by a mandatory 7-axis audit:

| Axis | Examples |
|---|---|
| **Layout primitive** | Card grid, horizontal rows, bento, list rows, magazine spread, split-pane |
| **Typography model** | Serif + sans, single geometric sans, monospace-only, heavy display grotesk |
| **Color temperature** | Cool dark, warm light, monochrome, vibrant, pastel, iridescent |
| **Component shape** | Sharp (0-4px), medium (8-12px), generous (16-24px), fully rounded, hard borders |
| **Motion character** | Snappy (150ms), confident (250ms), gentle (400ms), spring-based, minimal |
| **Information density** | Spacious editorial, balanced app, compact dashboard, dense terminal |
| **Emotional register** | Premium editorial, warm craft, technical futurist, playful startup, indie builder |

## Installation

### Claude Code Official Marketplace

```bash
/plugin install codech-mockup-design@claude-plugins-official
```

### Claude Code (via Custom Marketplace)

```bash
/plugin marketplace add codech-dev/codech-mockup-design-marketplace
/plugin install codech-mockup-design@codech-mockup-design-marketplace
```

### Manual Installation (Local)

Clone into your project's `.claude/skills/` directory:

```bash
cd your-project/.claude/skills/
git clone https://github.com/codech-dev/codech-mockup-design.git
```

Or install globally (available across all projects):

```bash
cd ~/.claude/skills/
git clone https://github.com/codech-dev/codech-mockup-design.git
```

## Dependencies

### Required

- **`ui-ux-pro-max` skill** — Design intelligence engine. Provides color palettes, font pairings, UX patterns, and product-type recommendations.
- **Python 3** — Required by ui-ux-pro-max's search scripts.
- **Internet connection** — For Tailwind CDN and Google Fonts in the showcase HTML.

### Target implementation stack

The design system documents target this stack by default (adapts to your project's actual stack):

| Tool | Role |
|---|---|
| **shadcn/ui** | Component library |
| **Framer Motion** | Animation library |
| **Tailwind CSS v4** | Styling system |
| **Lucide React** | Icon library |

## Plugin structure

```
codech-mockup-design/
├── package.json
├── CLAUDE.md
├── README.md
├── LICENSE
└── skills/
    └── codech-mockup-design/
        ├── SKILL.md
        └── references/
            ├── showcase-template.md
            ├── differentiation-axes.md
            └── interactive-prototype-scaffold.md
```

## Example output

The skill was developed while building the Atelier AI-driven Website Marketplace, where it produced:

- **4 marketplace design directions** (dark editorial, warm light, glassmorphism, app layout) — each genuinely different in layout, typography, color, and motion
- **1 dashboard design** (8 screens: onboarding, home, site editor with AI chat, prompt templates, version history, settings, commerce, custom dev requests)
- **4 design system documents** with full token specifications
- **5 visual showcase HTML files** totaling ~8,000 lines of production-quality mockups

## License

MIT

---

Built by [Codech](https://github.com/codech-dev) with Claude Code.