# Practices Landing Page Design

## Overview

Reorganize the flat `claude_code_practices` repo into a structured multi-practice site with a landing page. Each practice is a self-contained reveal.js presentation in its own directory. The landing page serves as a personal tech portfolio entry point.

## Directory Structure (Approach A: per-topic isolation)

```
claude_code_practices/
├── index.html                        # Landing page
├── assets/
│   ├── css/
│   │   └── landing.css               # Landing page styles
│   └── images/
│       └── avatar.jpeg               # Profile avatar
├── practices/
│   └── claude-code/
│       ├── index.html                # Migrated from presentation.html
│       ├── styles.css                # Migrated from root styles.css
│       └── images/
│           ├── img1.png
│           ├── img2.png
│           └── bash_mode.png         # Renamed from bash_mdoe.png
├── README.md
└── .gitignore
```

### Migration actions

1. `presentation.html` → `practices/claude-code/index.html` (update internal image paths: `img1.png` → `images/img1.png`, `img2.png` → `images/img2.png`, `bash_mdoe.png` → `images/bash_mode.png`)
2. `styles.css` → `practices/claude-code/styles.css`
3. `img1.png`, `img2.png`, `bash_mdoe.png` → `practices/claude-code/images/` (rename bash_mdoe → bash_mode)
4. `avart.jpeg` → `assets/images/avatar.jpeg`
5. Remove old root-level symlink `index.html` and replace with new landing page

## Landing Page Design

### Personal info

- Name: maodf
- Bio: A Carbon-based Token Generator
- Contact: mdengfeng@gmail.com
- Avatar: avart.jpeg (Shaun the Sheep style AI engineer character)

### Visual style

- **Theme**: Dark, modern, glassmorphism cards
- **Background**: `#0a0a0f` → `#1a1a2e` subtle gradient
- **Primary color**: `#6366f1` (indigo-purple)
- **Accent color**: `#22d3ee` (cyan) for hover/emphasis
- **Card background**: `rgba(255,255,255,0.05)` + `backdrop-filter: blur`
- **Text**: `#e2e8f0` (primary) / `#94a3b8` (secondary)
- **Fonts**: Inter + JetBrains Mono (Google Fonts CDN, consistent with presentations)

### Page layout (single page, top to bottom)

1. **Hero section**: Circular avatar (120px) with gradient border (indigo→cyan), name in large text, bio in muted small text, email with envelope icon (mailto: link)
2. **Practices grid**: CSS Grid, responsive (1 column mobile, 2-3 columns desktop)
   - Each card: glassmorphism style, icon/emoji + title (Chinese) + English subtitle + date + short description
   - Hover: slight lift (`translateY(-4px)`) + border glow
   - Entire card is a clickable link to `practices/xxx/index.html`
3. **Placeholder card**: Dashed border, low opacity, `+` icon with "more coming soon / 更多即将到来"
4. **Footer**: Minimal — `© 2026 maodf` + optional "Built with Claude Code"

### Language

Bilingual Chinese/English — Chinese titles with English subtitles, UI chrome in both languages.

### Technical constraints

- Pure HTML + CSS, zero JS dependencies
- CSS Grid for card layout
- Google Fonts (Inter, JetBrains Mono) via CDN
- Fully responsive
- No build step, no framework

## Adding a new practice

Two steps only:

1. Create `practices/<topic>/` with `index.html` + assets
2. Add a card to `index.html`:

```html
<a href="practices/<topic>/" class="card">
  <span class="card-icon">🔧</span>
  <h3>中文标题</h3>
  <p class="card-subtitle">English Subtitle</p>
  <p class="card-desc">一句话描述</p>
  <time>YYYY/MM/DD</time>
</a>
```

No JSON config or JS rendering — manual HTML cards, sufficient for the expected scale (single digits to low dozens).
