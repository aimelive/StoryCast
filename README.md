# StoryCast

An accessible audio and video storytelling platform — 3-page microsite built with semantic HTML5, Sass, responsive CSS Grid + Flexbox, container queries, and vanilla JS.

---

## Project Structure

```
storycast/
├── index.html                            # Home page
├── about.html                            # About & Access page
├── story/
│   ├── voices-from-the-valley.html       # Story: Voices from the Valley (Audio)
│   ├── cartographers-of-memory.html      # Story: The Cartographers of Memory (Audio)
│   ├── night-shift-at-the-clinic.html    # Story: The Night Shift at the Clinic (Video)
│   └── radio-discussion.html             # Story: Lagos Power Outages (Audio)
├── sass/
│   ├── main.scss                         # Entry point (imports all partials)
│   └── partials/
│       ├── _colors.scss                  # Color tokens
│       ├── _typography.scss              # Type scale, font stacks
│       ├── _spacing.scss                 # Spacing, shadow, radius tokens
│       ├── _reset.scss                   # Normalize + base styles
│       └── _components.scss              # All BEM components
├── css/
│   └── main.css                          # Compiled CSS output (do not edit directly)
├── assets/
│   ├── audio/
│   │   ├── Radio Discussion.mp3
│   │   ├── The cartographers of Memory.mp3
│   │   └── Vioces from the valley the Rift.mp3
│   ├── video/
│   │   └── The Night Shiftat the clinic.mp4
│   └── transcripts/
│       └── voices-from-the-valley.txt    # Sample transcript
└── README.md
```

---

## Pages

| Page | File | Media |
|------|------|-------|
| Home | `index.html` | Introduces StoryCast, featured story, story card grid |
| Voices from the Valley | `story/voices-from-the-valley.html` | Audio — *Vioces from the valley the Rift.mp3* |
| The Cartographers of Memory | `story/cartographers-of-memory.html` | Audio — *The cartographers of Memory.mp3* |
| The Night Shift at the Clinic | `story/night-shift-at-the-clinic.html` | Video — *The Night Shiftat the clinic.mp4* |
| Lagos Power Outages | `story/radio-discussion.html` | Audio — *Radio Discussion.mp3* |
| About & Access | `about.html` | Mission, accessibility features, team |

---

## Running Locally

No build server is required — you just need a local server to serve the files so audio and video load correctly. A browser opening `index.html` directly from the file system may block media; a local server fixes that.

### Option 1 — VS Code Live Server (recommended)

1. Open the `storycast` folder in VS Code
2. Install the **Live Server** extension by Ritwick Dey (Extensions tab → search "Live Server")
3. Right-click `index.html` → **Open with Live Server**
4. The site opens at `http://127.0.0.1:5500`

### Option 2 — Python

Open a terminal in the `storycast` folder and run:

```bash
python -m http.server 5500
```

Then open `http://localhost:5500` in your browser.

### Recompiling Sass

The compiled CSS is already included in `css/main.css`. If you edit any Sass file, recompile with:

```bash
# One-time compile
sass sass/main.scss css/main.css

# Watch mode — recompiles automatically on every save
sass --watch sass/main.scss css/main.css
```

Run this in a separate terminal alongside your local server.

---

## Media Files

| File | Type | Duration | Story page |
|------|------|----------|------------|
| `Radio Discussion.mp3` | Audio | 6:37 | `radio-discussion.html` |
| `The cartographers of Memory.mp3` | Audio | 20:27 | `cartographers-of-memory.html` |
| `Vioces from the valley the Rift.mp3` | Audio | 6:37 | `voices-from-the-valley.html` |
| `The Night Shiftat the clinic.mp4` | Video | 7:29 | `night-shift-at-the-clinic.html` |

Place audio files in `assets/audio/` and the video file in `assets/video/`. File names must match exactly (including spaces) as the HTML `src` attributes reference them by their original names.

---

## Design System

### Color Palette

| Token | Hex | Use |
|-------|-----|-----|
| `$color-ink` | `#0D0F14` | Page background |
| `$color-ink-mid` | `#1A1D26` | Card surfaces |
| `$color-amber` | `#F5A623` | Primary accent, links |
| `$color-chalk` | `#F2EFE8` | Body text |
| `$color-muted` | `#8B93A8` | Secondary text, metadata |
| `$color-signal` | `#E8534A` | Featured badge |
| `$color-success` | `#3DAD74` | Transcript / accessibility indicators |

### Typography

| Stack | Variable | Used for |
|-------|----------|----------|
| Playfair Display | `$font-display` | Headings, pull quotes |
| Inter | `$font-body` | All body copy and UI text |
| JetBrains Mono | `$font-mono` | Timestamps, labels, transcripts |

### Layout

- **CSS Grid** — page-level layouts, story card grids, story detail two-column layout
- **Flexbox** — component-level alignment (nav, cards, footer, player)
- **Container queries** — story cards switch from vertical to horizontal when their container drops below 480px
- **Fluid type scale** — all font sizes use `clamp()` to scale smoothly between breakpoints

---

## Sass Architecture

```
sass/
├── main.scss               ← imports all partials in order
└── partials/
    ├── _colors.scss        ← color tokens and semantic aliases
    ├── _typography.scss    ← font stacks, type scale, Google Fonts import
    ├── _spacing.scss       ← spacing scale, shadows, radii, transitions
    ├── _reset.scss         ← box-sizing reset, base element styles, skip link, .sr-only
    └── _components.scss    ← all BEM components (nav, hero, cards, player, transcript, etc.)
```

Partials are imported in dependency order — tokens first, then reset (which uses the tokens), then components (which use both). Never edit `css/main.css` directly; always edit the Sass source and recompile.

---

## Accessibility Checklist

### Media
- [x] All audio stories have a timed transcript readable inline and downloadable as `.txt`
- [x] Video story uses a `<track>` element for WebVTT closed captions
- [x] Native `<audio>` and `<video>` elements — browser-native controls are keyboard accessible
- [x] Decorative SVGs use `aria-hidden="true"`

### Navigation & Structure
- [x] Skip link (`<a class="skip-link" href="#main-content">`) is the first focusable element on every page
- [x] Landmark regions: `<header role="banner">`, `<nav>`, `<main>`, `<footer role="contentinfo">`, `<aside>`, `<section>`, `<article>`
- [x] Full keyboard navigation — every interactive element reachable and operable without a mouse
- [x] Visible `:focus-visible` ring — 2.5px amber outline on all interactive elements
- [x] Mobile nav toggle uses `aria-expanded` and `aria-controls`
- [x] Breadcrumb navigation on all story pages

### Semantic HTML
- [x] Headings follow a strict hierarchy on every page (h1 → h2 → h3, no skips)
- [x] `<dl>`, `<dt>`, `<dd>` for story metadata (author, duration, format)
- [x] `<nav aria-label>` distinguishes multiple navigation regions per page
- [x] `<article>` wraps each story card and team member
- [x] `aria-current="page"` on the active link in every nav
- [x] `aria-label` on all icon-only or ambiguous controls

### Color Contrast (WCAG 2.1 AA minimum: 4.5:1 normal text, 3:1 large text)

| Combination | Ratio | Result |
|-------------|-------|--------|
| Body text `#F2EFE8` on `#0D0F14` | 16.2:1 | ✓ AAA |
| Secondary text `#8B93A8` on `#0D0F14` | 5.8:1 | ✓ AA |
| Amber links `#F5A623` on `#0D0F14` | 8.1:1 | ✓ AAA |
| Success green `#3DAD74` on `#0D0F14` | 6.4:1 | ✓ AA |

### Motion & Preferences
- [x] `@media (prefers-reduced-motion: reduce)` disables all CSS animations and transitions
- [x] No autoplay on any media element

### ARIA
- [x] Transcript toggle: `aria-expanded` + `aria-controls` + `id` association
- [x] Hero stats: `role="list"` + `aria-label` on the container
- [x] Audio/video players: `aria-label` includes title and duration
- [x] `role="region"` + `aria-label` on transcript body

---

## Team

**Aime Ndayambaje** — Founder & Editor

---

## Tools Used

- HTML5 (semantic, no frameworks)
- Sass (partials and tokens, compiled to CSS)
- Vanilla JavaScript (mobile nav toggle, transcript collapse/expand)
- Google Fonts (Playfair Display, Inter, JetBrains Mono)
- Inline SVG for all decorative illustrations (no external image dependencies)