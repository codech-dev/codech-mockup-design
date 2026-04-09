# Showcase HTML Template Reference

This is the structural template for building design showcase HTML files. Every showcase follows this skeleton. Customize the tokens, sections, and content per project.

## Minimal working template

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>{{PROJECT}} — Design Showcase</title>

<!-- Google Fonts (customize per design direction) -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">

<!-- Tailwind CDN — no npm needed -->
<script src="https://cdn.tailwindcss.com"></script>

<style>
  :root {
    /* === DESIGN TOKENS === */
    /* Base palette */
    --color-bg: #FAFAFA;
    --color-surface: #FFFFFF;
    --color-border: #E5E5E5;
    --color-border-strong: #D4D4D4;
    --color-fg: #0A0A0A;
    --color-fg-muted: #525252;
    --color-fg-subtle: #A3A3A3;

    /* Accent */
    --color-accent: #2563EB;
    --color-accent-hover: #1D4ED8;
    --color-accent-subtle: #DBEAFE;

    /* Functional */
    --color-success: #22C55E;
    --color-warning: #F59E0B;
    --color-danger: #EF4444;

    /* Motion */
    --ease-out: cubic-bezier(0.22, 1, 0.36, 1);

    /* Shadows */
    --shadow-sm: 0 1px 2px rgba(0,0,0,0.05);
    --shadow-md: 0 4px 12px -2px rgba(0,0,0,0.08);
    --shadow-lg: 0 12px 24px -6px rgba(0,0,0,0.12);
    --shadow-xl: 0 24px 48px -12px rgba(0,0,0,0.16);
  }

  * { box-sizing: border-box; }
  html { scroll-behavior: smooth; }

  body {
    font-family: 'Inter', system-ui, sans-serif;
    background: var(--color-bg);
    color: var(--color-fg);
    -webkit-font-smoothing: antialiased;
    margin: 0;
  }

  ::selection {
    background: var(--color-accent);
    color: #FFFFFF;
  }

  /* === SCROLL REVEAL === */
  .reveal {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.7s var(--ease-out), transform 0.7s var(--ease-out);
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  .stagger > * {
    opacity: 0;
    transform: translateY(16px);
    transition: opacity 0.6s var(--ease-out), transform 0.6s var(--ease-out);
  }
  .stagger.visible > * { opacity: 1; transform: translateY(0); }
  .stagger.visible > *:nth-child(1) { transition-delay: 0.05s; }
  .stagger.visible > *:nth-child(2) { transition-delay: 0.13s; }
  .stagger.visible > *:nth-child(3) { transition-delay: 0.21s; }
  .stagger.visible > *:nth-child(4) { transition-delay: 0.29s; }
  .stagger.visible > *:nth-child(5) { transition-delay: 0.37s; }
  .stagger.visible > *:nth-child(6) { transition-delay: 0.45s; }

  @media (prefers-reduced-motion: reduce) {
    .reveal, .stagger > * {
      transition: none !important;
      opacity: 1 !important;
      transform: none !important;
    }
  }

  /* === FOCUS === */
  :focus-visible {
    outline: none;
    box-shadow: 0 0 0 2px var(--color-bg), 0 0 0 4px var(--color-accent);
    border-radius: inherit;
  }

  section[id] { scroll-margin-top: 80px; }
</style>
</head>
<body>

<!-- TOP NAV -->
<nav class="fixed top-0 inset-x-0 z-50 h-14 bg-white/80 backdrop-blur-xl border-b border-[var(--color-border)]">
  <div class="max-w-[1400px] mx-auto h-full px-6 lg:px-10 flex items-center justify-between">
    <div class="flex items-center gap-3">
      <span class="text-lg font-semibold tracking-tight">{{PROJECT}}</span>
      <span class="text-[10px] font-mono uppercase tracking-[0.14em] text-[var(--color-accent)] border border-[var(--color-accent-subtle)] rounded-full px-2 py-0.5">design showcase</span>
    </div>
    <div class="hidden md:flex items-center gap-1 text-sm">
      <a href="#tokens" class="px-3 py-1.5 rounded-lg text-[var(--color-fg-muted)] hover:text-[var(--color-fg)] hover:bg-gray-100 transition-colors">Tokens</a>
      <!-- Add section links here -->
    </div>
  </div>
</nav>

<!-- INTRO -->
<section class="relative pt-32 pb-20 px-6 lg:px-10">
  <div class="max-w-4xl mx-auto text-center">
    <h1 class="reveal text-4xl md:text-5xl lg:text-6xl leading-[1.05] tracking-[-0.02em] font-medium mb-8">
      {{PROJECT}} Design
    </h1>
    <p class="reveal text-lg text-[var(--color-fg-muted)] max-w-2xl mx-auto leading-[1.65] mb-10">
      {{DESCRIPTION}}
    </p>
  </div>
</section>

<!-- DESIGN TOKENS -->
<section id="tokens" class="py-20 px-6 lg:px-10 border-t border-[var(--color-border)]">
  <div class="max-w-[1400px] mx-auto">
    <div class="flex items-end justify-between mb-12 reveal">
      <div>
        <p class="text-[11px] font-mono uppercase tracking-[0.14em] text-[var(--color-accent)] mb-3">§01 — Foundation</p>
        <h2 class="text-4xl md:text-5xl tracking-[-0.02em] font-medium">Design Tokens</h2>
      </div>
    </div>

    <!-- Color swatches -->
    <div class="mb-16">
      <h3 class="text-[11px] font-mono uppercase tracking-[0.14em] text-[var(--color-fg-subtle)] mb-5">Palette</h3>
      <div class="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-5 gap-4 stagger">
        <!-- Repeat for each color token -->
        <div class="rounded-xl border border-[var(--color-border)] overflow-hidden bg-white">
          <div class="h-20" style="background: var(--color-bg);"></div>
          <div class="p-4">
            <div class="text-xs font-semibold mb-1">bg</div>
            <div class="text-[11px] font-mono text-[var(--color-fg-muted)]">#FAFAFA</div>
          </div>
        </div>
        <!-- ... more swatches -->
      </div>
    </div>

    <!-- Typography -->
    <div class="mb-16 reveal">
      <h3 class="text-[11px] font-mono uppercase tracking-[0.14em] text-[var(--color-fg-subtle)] mb-5">Typography</h3>
      <div class="border border-[var(--color-border)] rounded-2xl overflow-hidden bg-white p-8 md:p-12">
        <!-- Show each type scale level at actual size -->
      </div>
    </div>

    <!-- Primitives (buttons, inputs, badges) -->
    <div class="reveal border border-[var(--color-border)] rounded-2xl p-8 md:p-12 bg-white">
      <h3 class="text-[11px] font-mono uppercase tracking-[0.14em] text-[var(--color-fg-subtle)] mb-5">Primitives</h3>
      <!-- Interactive buttons, badges, inputs -->
    </div>
  </div>
</section>

<!-- SCREEN MOCKUPS (add as many as needed) -->
<section id="screen-1" class="py-20 px-6 lg:px-10 border-t border-[var(--color-border)]">
  <div class="max-w-[1400px] mx-auto">
    <div class="flex items-end justify-between mb-8 reveal">
      <div>
        <p class="text-[11px] font-mono uppercase tracking-[0.14em] text-[var(--color-accent)] mb-3">§02 — Screen Name</p>
        <h2 class="text-4xl md:text-5xl tracking-[-0.02em] font-medium">Screen Title</h2>
      </div>
      <p class="hidden md:block text-sm text-[var(--color-fg-muted)] max-w-sm text-right leading-[1.6]">Brief description</p>
    </div>
  </div>

  <div class="max-w-[1400px] mx-auto px-6 lg:px-10">
    <!-- Framed mockup -->
    <div class="rounded-2xl overflow-hidden border border-[var(--color-border)] bg-white" style="box-shadow: var(--shadow-xl);">
      <!-- Screen content here -->
    </div>
    <p class="mt-4 text-xs text-[var(--color-fg-subtle)] text-center font-mono">Annotation describing what this screen shows</p>
  </div>
</section>

<!-- FOOTER -->
<footer class="py-14 px-6 lg:px-10 border-t border-[var(--color-border)]">
  <div class="max-w-[1400px] mx-auto text-center">
    <p class="text-[11px] font-mono uppercase tracking-[0.14em] text-[var(--color-fg-subtle)]">
      {{PROJECT}} Design Showcase · {{DATE}}
    </p>
  </div>
</footer>

<!-- INTERSECTION OBSERVER -->
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
        if (entry.isIntersecting) { reveal(entry.target); io.unobserve(entry.target); }
      }
    },
    { threshold: 0.12, rootMargin: '0px 0px -40px 0px' }
  );
  document.querySelectorAll('.reveal, .stagger').forEach((el) => io.observe(el));
})();
</script>

</body>
</html>
```

## Placeholder variables

Replace these in the template:
- `{{PROJECT}}` — project/brand name
- `{{DESCRIPTION}}` — one-line description of the design showcase
- `{{DATE}}` — creation date

## Adding more sections

Copy the "SCREEN MOCKUPS" section block for each screen. Increment the section number (§02, §03, etc.) and update the `id`, title, and content.

## Multi-version navigation

When building multiple versions (v1, v2, v3...), add cross-links in the top nav:

```html
<div class="flex items-center gap-1 text-xs">
  <span class="px-3 py-1.5 rounded-lg text-[var(--color-accent)] font-semibold bg-[var(--color-accent-subtle)]">v1</span>
  <a href="./design-showcase-v2.html" class="px-3 py-1.5 rounded-lg text-[var(--color-fg-subtle)] hover:text-[var(--color-fg)]">v2</a>
  <a href="./design-showcase-v3.html" class="px-3 py-1.5 rounded-lg text-[var(--color-fg-subtle)] hover:text-[var(--color-fg)]">v3</a>
</div>
```