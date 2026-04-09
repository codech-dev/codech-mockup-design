---
name: codech-mockup-design
description: |
  Codech Mockup Design Skill — structured design ideation and visual prototyping workflow. Creates design system documents (tokens, principles, accessibility rules) and self-contained HTML showcases that render live in any browser — no build step needed. Use this skill PROACTIVELY when the user asks to design UI, create a design system, prototype screens, explore visual directions, build a landing page mockup, design a dashboard, or compare design alternatives. Also trigger when the user says things like "show me what it would look like", "design the UI", "create a mockup", "explore different styles", "what should the homepage look like", or "build a visual prototype". Works for any project: landing pages, dashboards, mobile apps, SaaS products, marketplaces, portfolios.
---

# Codech Mockup Design Skill

A structured workflow for design ideation that produces two artifacts per design direction:
1. **Design system document** (`design-system.md`) — tokens, principles, component patterns, accessibility rules
2. **Visual showcase** (`design-showcase.html`) — self-contained HTML that renders every token, screen, and component live in any browser

The showcase is the primary deliverable — it's what the user judges the design against. The markdown document supports it with rationale and implementation guidance.

## Prerequisites (required)

Before using this skill, ensure the following are installed and available:

1. **`ui-ux-pro-max` skill** — REQUIRED for design intelligence queries. The skill will NOT proceed to Phase 2 (design system creation) without first running ui-ux-pro-max queries in Phase 1. If the skill is not available, stop and tell the user:
   > "The `ui-ux-pro-max` skill is required for design intelligence. Please install it first, then re-run this skill."

2. **Python 3** — Required by ui-ux-pro-max's search.py script. Verify with `python3 --version` or `python --version`.

3. **Internet connection** — Required at showcase render time for Tailwind CDN and Google Fonts. The showcase HTML files will not render correctly offline.

**Implementation stack (for the actual project, not the showcase):**
- **shadcn/ui** — the component library all designs target. The design system document must reference specific shadcn components for each UI pattern.
- **Framer Motion** — the animation library all motion patterns target. The design system document must include Framer Motion code examples for each animation.
- **Tailwind CSS v4** — the styling system. All design tokens map to Tailwind's theme.extend.
- **Lucide React** — the icon library. All icons in the showcase use inline SVGs matching Lucide's style.

If the project doesn't use shadcn/ui, Framer Motion, or Tailwind, adapt the component patterns and animation examples to the project's actual stack — but default to these unless told otherwise.

## Recommended tech stack

The skill is designed around a modern frontend stack. Use these tools by default unless the user specifies otherwise:

- **UI/UX Intelligence:** `ui-ux-pro-max` skill — run design system queries (`--design-system`, `--domain color`, `--domain ux`, `--domain landing`) before making design decisions. Provides color palettes, font pairings, UX patterns, and product-type recommendations.
- **Component Library:** **shadcn/ui** — use shadcn components (Button, Card, Badge, Separator, Input, Tabs, Sheet, Dialog, Command, ScrollArea, Avatar, Tooltip, Accordion) as the building blocks for all UI. Reference shadcn component patterns in the design system document so the implementation team knows exactly which primitives to use.
- **Animation:** **Framer Motion** — all entrance animations, hover states, page transitions, and scroll-triggered reveals should be designed with Framer Motion patterns in mind. Specify easing curves as `cubic-bezier()` values, durations in ms, and stagger delays. The showcase HTML simulates these with CSS transitions (since Framer Motion requires React), but the design system doc should note the Framer Motion equivalent for each animation.
- **Styling:** **Tailwind CSS** — all designs use Tailwind utility classes. The showcase HTML loads Tailwind via CDN. The design system document defines all tokens as CSS custom properties that map to Tailwind's `theme.extend`.
- **Icons:** **Lucide React** — use Lucide icons (consistent stroke width, tree-shakeable). Never use emojis as structural UI icons. In showcase HTML, use inline SVGs matching Lucide's style (1.5–2px stroke width, round line caps).

When writing the design system document, include a "Implementation notes" section that specifies:
```
### Implementation notes
- Component library: shadcn/ui (install via `pnpm dlx shadcn@latest add <component>`)
- Animation: Framer Motion (`initial`, `animate`, `whileInView`, `variants` patterns)
- Icons: Lucide React (`lucide-react` package)
- Fonts: Load via `next/font/google` for automatic optimization
```

## When to use this skill

- User asks to design or prototype any UI (landing page, dashboard, app screen, component library)
- User wants to explore visual directions before building
- User asks "what should this look like?" or "show me a mockup"
- User wants to compare multiple design alternatives
- User needs a design system established before implementation
- User says "create a design" or "design the interface" or "prototype the screens"

## The workflow

### Phase 1 — Gather intelligence (before designing)

Run the `ui-ux-pro-max` skill to get informed design recommendations BEFORE making any visual decisions. This is mandatory — do not skip to Phase 2 without running at least the `--design-system` query.

```bash
# REQUIRED: Get overall design system recommendation
python3 <ui-ux-pro-max-path>/scripts/search.py "<product_type> <industry> <keywords>" --design-system -p "<Project>"

# REQUIRED: Get color palette options for the product type
python3 <ui-ux-pro-max-path>/scripts/search.py "<industry> <mood>" --domain color -n 3

# RECOMMENDED: Get UX patterns for key interactions
python3 <ui-ux-pro-max-path>/scripts/search.py "<interaction_pattern>" --domain ux -n 5

# RECOMMENDED: Get page structure patterns
python3 <ui-ux-pro-max-path>/scripts/search.py "<page_type>" --domain landing -n 3
```

If `ui-ux-pro-max` is not installed, stop and inform the user that it's a required dependency. Do not proceed with design work based solely on general knowledge — the intelligence queries are what make this skill produce informed, defensible design decisions rather than guesswork.

**Key intelligence to gather before designing:**
- Product type (SaaS, marketplace, portfolio, dashboard, mobile app)
- Target audience (technical vs non-technical, age range, context of use)
- Competitor references (what should this look like vs NOT look like)
- Emotional register (premium, playful, corporate, editorial, warm, technical)
- Any locked decisions (brand colors, fonts, existing design tokens)

### Phase 2 — Write the design system document

Create `docs/design/design-system.md` (or version-suffixed like `design-system-v2.md` for alternatives).

**Required sections:**

1. **Design philosophy** — 2–3 principles that guide every decision. Not generic ("be accessible") — specific to THIS project ("the work is the hero, the frame recedes").

2. **Color system** — Every color as a named token with hex value, contrast ratio against the base, and usage guidance.
   ```
   | Token | Hex | Use |
   |---|---|---|
   | --color-bg | #FAFAFA | Page background |
   | --color-fg | #0A0A0B | Primary text |
   | --color-accent | #F97316 | Primary CTAs, active states |
   ```

3. **Typography** — Font pairing with rationale, full type scale (display → body → caption → mono), line heights, letter spacing, weight rules.

4. **Spacing & layout** — 4px or 8px grid, container widths, breakpoints, specific spacing values used.

5. **Border radius & shadows** — Scale with named tokens and usage guidance.

6. **Motion system** — Easing curves (with cubic-bezier values), durations (fast/normal/slow), entrance patterns, reduced-motion handling. Include Framer Motion code examples for key patterns:
   ```tsx
   // Standard entrance (document in design system)
   <motion.div
     initial={{ opacity: 0, y: 24 }}
     animate={{ opacity: 1, y: 0 }}
     transition={{ duration: 0.6, ease: [0.22, 1, 0.36, 1] }}
   />

   // Scroll-triggered stagger (document in design system)
   <motion.div
     variants={{ visible: { transition: { staggerChildren: 0.08 } } }}
     initial="hidden"
     whileInView="visible"
     viewport={{ once: true }}
   />

   // Hover interaction (document in design system)
   <motion.div whileHover={{ y: -4, transition: { duration: 0.15 } }} />
   ```

7. **Component patterns** — How buttons, cards, inputs, badges, and navigation look and behave across states (hover, focus, active, disabled).

8. **Accessibility baseline** — Contrast minimums, focus ring style, touch targets, keyboard navigation rules, reduced-motion commitment.

### Phase 3 — Build the visual showcase HTML

This is the core deliverable. Create a **single self-contained HTML file** that opens in any browser with zero build steps.

**Technical requirements:**

```html
<!-- Load Tailwind via CDN — no npm -->
<script src="https://cdn.tailwindcss.com"></script>

<!-- Load Google Fonts via link tags -->
<link href="https://fonts.googleapis.com/css2?family=..." rel="stylesheet">
```

**Architecture of the HTML file:**

```
design-showcase.html
├── <style> block with CSS custom properties (all design tokens)
├── Scroll-reveal animation classes (.reveal, .stagger)
├── @media (prefers-reduced-motion) fallbacks
├── Section 0: Intro / title card
├── Section 1: Design tokens rendered live
│   ├── Color swatches (rendered as colored boxes)
│   ├── Type scale (rendered at actual sizes)
│   ├── Spacing scale (rendered as bars)
│   ├── Border radius (rendered as shapes)
│   ├── Motion values (listed with easing curves)
│   └── Primitives (buttons, badges, inputs — interactive)
├── Section N: Full-page screen mockups
│   └── Each framed in a bordered container with shadow
│       to look like a real app screenshot
├── Footer with navigation links
└── <script> IntersectionObserver for entrance animations
```

**CSS custom properties pattern (always use this):**

```css
:root {
  /* Base */
  --color-bg: #FAFAFA;
  --color-surface: #FFFFFF;
  --color-border: #E7E5E4;
  --color-fg: #0A0A0B;
  --color-fg-muted: #57534E;
  --color-fg-subtle: #A8A29E;

  /* Accent */
  --color-accent: #F97316;
  --color-accent-hover: #EA580C;

  /* Motion */
  --ease-out: cubic-bezier(0.22, 1, 0.36, 1);

  /* Shadows */
  --shadow-sm: 0 1px 2px rgba(0,0,0,0.04);
  --shadow-md: 0 4px 12px -2px rgba(0,0,0,0.06);
  --shadow-lg: 0 12px 24px -6px rgba(0,0,0,0.10);
}
```

**Scroll-reveal animation pattern (always include):**

```css
.reveal {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.7s var(--ease-out), transform 0.7s var(--ease-out);
}
.reveal.visible { opacity: 1; transform: translateY(0); }

/* Staggered children */
.stagger > * {
  opacity: 0; transform: translateY(16px);
  transition: opacity 0.6s var(--ease-out), transform 0.6s var(--ease-out);
}
.stagger.visible > * { opacity: 1; transform: translateY(0); }
.stagger.visible > *:nth-child(1) { transition-delay: 0.05s; }
.stagger.visible > *:nth-child(2) { transition-delay: 0.13s; }
/* ... continue for expected child count */

@media (prefers-reduced-motion: reduce) {
  .reveal, .stagger > * {
    transition: none !important;
    opacity: 1 !important;
    transform: none !important;
  }
}
```

**IntersectionObserver script (always include at end of body):**

```html
<script>
(function() {
  const prefersReduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  const reveal = (el) => el.classList.add('visible');
  if (prefersReduced) {
    document.querySelectorAll('.reveal, .stagger').forEach(reveal);
    return;
  }
  const io = new IntersectionObserver(
    (entries) => {
      for (const entry of entries) {
        if (entry.isIntersecting) {
          reveal(entry.target);
          io.unobserve(entry.target);
        }
      }
    },
    { threshold: 0.12, rootMargin: '0px 0px -40px 0px' }
  );
  document.querySelectorAll('.reveal, .stagger').forEach((el) => io.observe(el));
})();
</script>
```

**Screen mockup framing pattern:**

Each full-page screen mockup should be wrapped in a container that looks like a device/browser frame:

```html
<div class="rounded-2xl overflow-hidden border border-[var(--color-border)] bg-white"
     style="box-shadow: var(--shadow-xl);">
  <!-- The actual screen content goes here -->
</div>
<p class="mt-4 text-xs text-[var(--color-fg-subtle)] text-center font-mono">
  Brief annotation explaining what this screen shows
</p>
```

**Section header pattern:**

```html
<div class="flex items-end justify-between mb-8 reveal">
  <div>
    <p class="text-[11px] font-mono uppercase tracking-[0.14em] text-[var(--color-accent)] mb-3">
      §01 — Section Name
    </p>
    <h2 class="font-display text-4xl md:text-5xl tracking-[-0.02em] font-medium">
      Display Title
    </h2>
  </div>
  <p class="hidden md:block text-sm text-[var(--color-fg-muted)] max-w-sm text-right leading-[1.6]">
    Brief description of what this section contains
  </p>
</div>
```

### Phase 4 — Present and iterate

After building the showcase:

1. Tell the user which file to open and how (e.g., "Open design-showcase.html in a browser")
2. List what each section shows
3. Call out specific things to evaluate ("look at the card hover states", "compare the type scale")
4. Ask for explicit approval or change requests
5. If changes requested, edit the existing file or create a new version

### Phase 5 — Multiple directions (when requested)

When the user wants to compare alternatives, every version MUST be **identically different** — not a reskin with swapped colors. This is the single most important rule in the skill. Users will reject versions that feel like cousins of each other.

**The identically-different rule:** Each version must differ from every other version on **at least 5 of these 7 axes**. Before building any v2/v3/v4, explicitly audit the previous versions against this checklist and verify 5+ axes are genuinely changing. If fewer than 5 change, the new version is a reskin — go back and make it more different.

| Axis | What must change | Bad (reskin) | Good (identically different) |
|---|---|---|---|
| **Layout primitive** | The fundamental page structure | v1 card grid → v2 card grid | v1 card grid → v2 horizontal rows → v3 bento → v4 sidebar+rows |
| **Font family** | The actual typefaces used | v1 Inter → v2 Inter | v1 Playfair+Inter → v2 Fraunces+DM Sans → v3 Geist only → v4 General Sans+Instrument Serif |
| **Color system** | Base palette + accent + temperature | v1 dark+pink → v2 dark+blue | v1 dark near-black+magenta → v2 warm cream+terracotta → v3 aurora+violet → v4 near-white+coral |
| **Component architecture** | How cards, nav, detail pages are built | Same card layout with different border radius | v1 rounded cards → v2 hairline-border cards → v3 glass panels → v4 cinematic wide cards in scroll rows |
| **Motion character** | Speed, easing, entrance style | Same ease-out at different durations | v1 snappy 250ms → v2 gentle 400ms → v3 spring-physics 500ms + blur-in → v4 crisp app 150ms |
| **Information density** | How much per viewport | Similar whitespace | v1 spacious editorial → v2 magazine rhythm → v3 floating spatial → v4 compact app |
| **Emotional register** | The personality the design communicates | "Premium" with different colors | v1 "Vercel at night" → v2 "Aesop in the morning" → v3 "Apple Vision Pro" → v4 "Spotify app" |

**Before building a new version, write a 7-row audit table** comparing the new direction against all previous versions. Show it to yourself and verify 5+ rows are genuinely different. If you can't fill 5 rows with real differences, you don't have a new direction — you have a reskin. Go back to `references/differentiation-axes.md` and pick a different archetype.

Name each direction with a memorable codename (e.g., "Vitrine," "Atelier," "Oracle") and include cross-navigation links in each showcase file so the user can switch between tabs easily.

See `references/differentiation-axes.md` for the full axis reference with 8 ready-to-use archetype combinations.

### Phase 6 — Lock and reference

Once the user approves a direction:
1. Note which version was approved in the design system doc
2. Add a reference link from implementation plans/specs to the approved design files
3. Replace any `{{BRAND_NAME}}` or other placeholders with real values
4. Commit the design files to git if the project has a repo

### Phase 7 — Interactive prototype (optional, on request)

After the static showcase is approved, the user may ask for a **real interactive prototype** with working animations, hover states, scroll effects, and component interactivity. This goes beyond what static HTML can do — it requires React.

**When to offer this:** When the user says "make it interactive", "add animations", "use shadcn and Framer Motion", "build a working prototype", or "I want to click through it."

**What to build:** A standalone **Vite + React + TypeScript** app in a `prototype/` folder within the project. This is NOT the production app — it's a lightweight interactive proof-of-concept that renders the approved design with real interactivity.

**Setup steps:**

```bash
# 1. Scaffold the prototype app
cd <project-root>
pnpm create vite prototype --template react-ts
cd prototype
pnpm install

# 2. Install the design stack
pnpm add framer-motion lucide-react
pnpm add tailwindcss @tailwindcss/vite -D

# 3. Install shadcn/ui
pnpm dlx shadcn@latest init
pnpm dlx shadcn@latest add button card badge separator input tabs \
  sheet dialog command scroll-area avatar tooltip accordion
```

**Project structure:**

```
prototype/
├── src/
│   ├── components/
│   │   ├── ui/              # shadcn components (auto-generated)
│   │   ├── landing/         # Landing page sections
│   │   │   ├── Hero.tsx
│   │   │   ├── ProblemSection.tsx
│   │   │   ├── ValueProps.tsx
│   │   │   ├── AISpotlight.tsx
│   │   │   ├── HowItWorks.tsx
│   │   │   ├── SandboxDemo.tsx
│   │   │   ├── GalleryGrid.tsx
│   │   │   ├── SocialProof.tsx
│   │   │   └── FinalCTA.tsx
│   │   ├── marketplace/     # App screen components
│   │   │   ├── Sidebar.tsx
│   │   │   ├── CategoryRow.tsx
│   │   │   ├── SiteCard.tsx
│   │   │   └── FloatingChat.tsx
│   │   ├── dashboard/       # Dashboard components
│   │   │   ├── Onboarding.tsx
│   │   │   ├── SiteEditor.tsx
│   │   │   ├── AIChat.tsx
│   │   │   └── VersionHistory.tsx
│   │   └── shared/          # Shared components
│   │       ├── Navigation.tsx
│   │       ├── AIAvatar.tsx
│   │       └── DeviceSwitcher.tsx
│   ├── lib/
│   │   ├── tokens.ts        # Design tokens as JS constants
│   │   └── animations.ts    # Framer Motion variants & transitions
│   ├── styles/
│   │   └── globals.css      # CSS custom properties + Tailwind
│   ├── pages/
│   │   ├── Landing.tsx
│   │   ├── Marketplace.tsx
│   │   ├── Detail.tsx
│   │   └── Dashboard.tsx
│   ├── App.tsx
│   └── main.tsx
├── index.html
├── tailwind.config.ts
├── tsconfig.json
├── vite.config.ts
└── package.json
```

**Design tokens file** (`src/lib/tokens.ts`):

Translate the CSS custom properties from the design system into TypeScript constants so they're usable in both Tailwind config and Framer Motion:

```ts
export const tokens = {
  colors: {
    bg: '#FAFAFA',
    surface: '#FFFFFF',
    border: '#E7E5E4',
    fg: '#0A0A0B',
    fgMuted: '#57534E',
    fgSubtle: '#A8A29E',
    accent: '#F97316',
    accentHover: '#EA580C',
    accentSubtle: '#FFEDD5',
    success: '#22C55E',
    warning: '#F59E0B',
    danger: '#EF4444',
  },
  gradients: {
    ai: 'linear-gradient(135deg, #8B5CF6 0%, #EC4899 33%, #F97316 66%, #FBBF24 100%)',
  },
} as const;
```

**Animation variants file** (`src/lib/animations.ts`):

Define reusable Framer Motion variants that match the design system's motion spec:

```ts
import type { Variants, Transition } from 'framer-motion';

export const ease = [0.22, 1, 0.36, 1] as const;

export const duration = {
  fast: 0.15,
  normal: 0.25,
  slow: 0.4,
  slower: 0.6,
} as const;

// Standard entrance — fade + slide up
export const fadeInUp: Variants = {
  hidden: { opacity: 0, y: 24 },
  visible: { opacity: 1, y: 0, transition: { duration: duration.slower, ease } },
};

// Stagger children
export const staggerContainer: Variants = {
  hidden: {},
  visible: { transition: { staggerChildren: 0.08, delayChildren: 0.1 } },
};

export const staggerChild: Variants = {
  hidden: { opacity: 0, y: 20 },
  visible: { opacity: 1, y: 0, transition: { duration: 0.5, ease } },
};

// Card hover
export const cardHover = {
  y: -4,
  transition: { duration: duration.fast, ease } as Transition,
};

// Scale on tap
export const tapScale = { scale: 0.98 };
```

**Component pattern** — every section component follows this structure:

```tsx
'use client';
import { motion } from 'framer-motion';
import { fadeInUp, staggerContainer, staggerChild } from '@/lib/animations';
import { Button } from '@/components/ui/button';
import { Card } from '@/components/ui/card';

export function HowItWorks() {
  return (
    <section className="px-8 md:px-12 py-16 bg-white">
      <motion.div
        className="max-w-4xl mx-auto text-center mb-12"
        initial="hidden"
        whileInView="visible"
        viewport={{ once: true, margin: '-100px' }}
        variants={fadeInUp}
      >
        <h2 className="text-3xl md:text-4xl font-medium">
          Three steps. <em>That's it.</em>
        </h2>
      </motion.div>

      <motion.div
        className="grid md:grid-cols-3 gap-8 max-w-5xl mx-auto"
        initial="hidden"
        whileInView="visible"
        viewport={{ once: true }}
        variants={staggerContainer}
      >
        {steps.map((step) => (
          <motion.div key={step.num} variants={staggerChild}>
            <Card className="text-center p-6">
              {/* ... */}
            </Card>
          </motion.div>
        ))}
      </motion.div>
    </section>
  );
}
```

**What the prototype delivers that the static showcase cannot:**
- Real Framer Motion animations (spring physics, whileInView, stagger, layout animations)
- Working shadcn components (Dialog opens, Tabs switch, Accordion expands, Command palette opens with ⌘K)
- Interactive hover states with motion (cards lift with spring, buttons scale on press)
- Working device switcher (preview iframe resizes)
- Simulated AI chat (typing indicator, streaming text response, action buttons that work)
- Page routing (landing → marketplace → detail → dashboard)
- Responsive layout (sidebar collapses on mobile, horizontal rows scroll with touch)

**What the prototype does NOT need:**
- Real backend/API
- Real data (use hardcoded mock data matching the showcase)
- Authentication
- Database
- Deployment (runs locally via `pnpm dev`)

**How to run:**

```bash
cd prototype
pnpm dev
# Opens at http://localhost:5173
```

**When to suggest this to the user:**
After the static showcase is approved AND the user wants to feel the interactions before committing to the full production build. Frame it as: "The static showcase shows the design. The interactive prototype lets you *feel* it — real animations, real component interactions, working navigation. It takes ~1 session to build and can serve as a reference implementation for the production app."

## Quality checklist

**For multi-version designs (v2, v3, v4...) — verify FIRST:**
- [ ] Audit table written comparing new version against all previous versions on all 7 axes
- [ ] At least 5 of 7 axes are genuinely different (not just tweaked)
- [ ] Different font families used (not the same fonts with different weights)
- [ ] Different layout primitive (not the same grid with different card shapes)
- [ ] Different color temperature (not the same hue at different lightness)
- [ ] Different component architecture (not the same cards with different borders)
- [ ] A unique codename assigned to the new direction

**For every showcase — verify before presenting:

- [ ] HTML opens correctly in a browser with no console errors
- [ ] All fonts load (Google Fonts link tags present and correct)
- [ ] Tailwind CDN script tag present
- [ ] All CSS custom properties defined in `:root`
- [ ] Scroll-reveal animations work (IntersectionObserver script at end of body)
- [ ] `prefers-reduced-motion` media query present and functional
- [ ] Color contrast meets WCAG AA (4.5:1 body text, 3:1 large text)
- [ ] Focus-visible styles defined for interactive elements
- [ ] No emojis used as structural icons (use SVGs)
- [ ] Every section has a numbered header (§01, §02, etc.)
- [ ] Annotation text below each framed mockup
- [ ] Navigation in the top bar links to all sections

## File naming convention

```
docs/design/
├── design-system.md           # v1 (or only version)
├── design-system-v2.md        # alternative direction
├── design-system-v3.md        # another alternative
├── design-showcase.html       # v1 showcase
├── design-showcase-v2.html    # v2 showcase
├── design-showcase-v3.html    # v3 showcase
├── design-showcase-dashboard.html  # screen-specific showcase
└── design-system-v4.md        # approved version (noted in doc)
```

## Common pitfalls to avoid

1. **Reskinning instead of redesigning — the #1 failure mode.** When asked for "a different version," you MUST change the layout primitive, the font families, the color temperature, the component architecture, AND the motion character — at minimum 5 of 7 axes. Changing colors from magenta to terracotta on the same card grid with the same serif+sans type model is NOT a new version. The user WILL notice and WILL ask you to redo it. Write the 7-axis audit table BEFORE building to catch this early.

2. **Designing in a vacuum.** Always gather intelligence first (product type, audience, competitors, emotional register). A wellness-coach marketplace and a developer-tool dashboard need fundamentally different designs even if both are "modern and minimal."

3. **Making the showcase too simple.** The showcase needs real content — real headlines, real card data, real interaction states. Placeholder-heavy showcases don't help the user judge the design.

4. **Forgetting mobile.** Every showcase should be responsive. Use Tailwind responsive prefixes (`md:`, `lg:`) throughout.

5. **Skipping accessibility.** Every showcase must have: contrast-passing colors, focus-visible rings, reduced-motion fallbacks, semantic HTML, no emoji icons.

6. **Not annotating.** Every framed mockup needs a brief annotation below it explaining what the screen shows. The user shouldn't have to guess.