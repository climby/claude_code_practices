# Practices Landing Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Reorganize the flat repo into a per-topic directory structure and create a polished landing page as a personal tech portfolio.

**Architecture:** Pure static site. Each practice lives in its own `practices/<topic>/` directory with all assets self-contained. Root `index.html` is a handcrafted landing page with glassmorphism card grid linking to each practice. Zero JS dependencies for the landing page.

**Tech Stack:** HTML5, CSS3 (Grid, backdrop-filter, custom properties), Google Fonts (Inter, JetBrains Mono) via CDN.

---

### Task 1: Create directory structure and migrate existing files

**Files:**
- Create: `practices/claude-code/images/` (directory)
- Create: `assets/css/` (directory)
- Create: `assets/images/` (directory)
- Move: `presentation.html` → `practices/claude-code/index.html`
- Move: `styles.css` → `practices/claude-code/styles.css`
- Move: `img1.png` → `practices/claude-code/images/img1.png`
- Move: `img2.png` → `practices/claude-code/images/img2.png`
- Move: `bash_mdoe.png` → `practices/claude-code/images/bash_mode.png` (rename fix)
- Move: `avart.jpeg` → `assets/images/avatar.jpeg`
- Remove: `index.html` (symlink)

- [ ] **Step 1: Create target directories**

```bash
mkdir -p practices/claude-code/images
mkdir -p assets/css
mkdir -p assets/images
```

- [ ] **Step 2: Remove the symlink**

```bash
rm index.html
```

- [ ] **Step 3: Move presentation files into practices/claude-code/**

```bash
mv presentation.html practices/claude-code/index.html
mv styles.css practices/claude-code/styles.css
```

- [ ] **Step 4: Move images into practices/claude-code/images/ (rename bash_mdoe)**

```bash
mv img1.png practices/claude-code/images/img1.png
mv img2.png practices/claude-code/images/img2.png
mv bash_mdoe.png practices/claude-code/images/bash_mode.png
```

- [ ] **Step 5: Move avatar**

```bash
mv avart.jpeg assets/images/avatar.jpeg
```

- [ ] **Step 6: Verify directory structure**

```bash
find . -not -path './.git/*' -not -path './.git' | sort
```

Expected output includes:
```
./assets/css
./assets/images/avatar.jpeg
./practices/claude-code/images/bash_mode.png
./practices/claude-code/images/img1.png
./practices/claude-code/images/img2.png
./practices/claude-code/index.html
./practices/claude-code/styles.css
```

- [ ] **Step 7: Commit**

```bash
git add -A
git commit -m "refactor: reorganize flat repo into per-topic directory structure

Move presentation and assets into practices/claude-code/.
Move avatar to assets/images/.
Rename bash_mdoe.png to bash_mode.png."
```

---

### Task 2: Update image paths in practices/claude-code/index.html

**Files:**
- Modify: `practices/claude-code/index.html` (3 image src attributes)

- [ ] **Step 1: Update img1.png path**

In `practices/claude-code/index.html`, change:
```html
<img src="img1.png" alt="Pod 管理主页"
```
to:
```html
<img src="images/img1.png" alt="Pod 管理主页"
```

- [ ] **Step 2: Update img2.png path**

Change:
```html
<img src="img2.png" alt="资源规格页面"
```
to:
```html
<img src="images/img2.png" alt="资源规格页面"
```

- [ ] **Step 3: Update bash_mdoe.png path (with rename)**

Change:
```html
<img src="bash_mdoe.png" alt="Bash Mode 截图"
```
to:
```html
<img src="images/bash_mode.png" alt="Bash Mode 截图"
```

- [ ] **Step 4: Verify the presentation loads correctly**

```bash
python3 -m http.server 8080 --directory practices/claude-code/ &
sleep 1
curl -s http://localhost:8080/ | grep -c 'images/img1.png'
curl -s http://localhost:8080/ | grep -c 'images/img2.png'
curl -s http://localhost:8080/ | grep -c 'images/bash_mode.png'
kill %1
```

Expected: Each grep returns `1`.

- [ ] **Step 5: Commit**

```bash
git add practices/claude-code/index.html
git commit -m "fix: update image paths for new directory structure"
```

---

### Task 3: Create landing page CSS

**Files:**
- Create: `assets/css/landing.css`

- [ ] **Step 1: Write the complete landing page stylesheet**

Create `assets/css/landing.css` with these sections:

```css
/* === CSS Custom Properties === */
:root {
  --bg-primary: #0a0a0f;
  --bg-secondary: #1a1a2e;
  --color-primary: #6366f1;
  --color-accent: #22d3ee;
  --color-text: #e2e8f0;
  --color-text-muted: #94a3b8;
  --color-card-bg: rgba(255, 255, 255, 0.05);
  --color-card-border: rgba(255, 255, 255, 0.08);
  --color-card-hover-border: rgba(99, 102, 241, 0.4);
  --font-body: 'Inter', system-ui, -apple-system, sans-serif;
  --font-mono: 'JetBrains Mono', 'Fira Code', monospace;
}

/* === Reset & Base === */
*, *::before, *::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: var(--font-body);
  background: linear-gradient(160deg, var(--bg-primary) 0%, var(--bg-secondary) 100%);
  color: var(--color-text);
  min-height: 100vh;
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
}

/* === Layout === */
.container {
  max-width: 960px;
  margin: 0 auto;
  padding: 0 24px;
}

/* === Hero Section === */
.hero {
  text-align: center;
  padding: 80px 0 60px;
}

.avatar {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid transparent;
  background-image: linear-gradient(var(--bg-primary), var(--bg-primary)),
                    linear-gradient(135deg, var(--color-primary), var(--color-accent));
  background-origin: border-box;
  background-clip: padding-box, border-box;
  margin-bottom: 20px;
}

.hero h1 {
  font-size: 2rem;
  font-weight: 700;
  letter-spacing: -0.02em;
  margin-bottom: 8px;
}

.hero .bio {
  font-family: var(--font-mono);
  font-size: 0.95rem;
  color: var(--color-text-muted);
  margin-bottom: 16px;
}

.hero .contact a {
  color: var(--color-text-muted);
  text-decoration: none;
  font-size: 0.875rem;
  transition: color 0.2s;
}

.hero .contact a:hover {
  color: var(--color-accent);
}

/* === Section Header === */
.section-header {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 32px;
}

.section-header h2 {
  font-size: 1.25rem;
  font-weight: 600;
}

.section-header::after {
  content: '';
  flex: 1;
  height: 1px;
  background: linear-gradient(90deg, var(--color-card-border), transparent);
}

/* === Practices Grid === */
.practices-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 20px;
  padding-bottom: 80px;
}

/* === Practice Card === */
.card {
  display: flex;
  flex-direction: column;
  padding: 28px 24px;
  background: var(--color-card-bg);
  border: 1px solid var(--color-card-border);
  border-radius: 12px;
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  text-decoration: none;
  color: inherit;
  transition: transform 0.25s ease, border-color 0.25s ease, box-shadow 0.25s ease;
}

.card:hover {
  transform: translateY(-4px);
  border-color: var(--color-card-hover-border);
  box-shadow: 0 8px 32px rgba(99, 102, 241, 0.1);
}

.card-icon {
  font-size: 1.75rem;
  margin-bottom: 16px;
  display: block;
}

.card h3 {
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 4px;
}

.card .card-subtitle {
  font-size: 0.85rem;
  color: var(--color-text-muted);
  margin-bottom: 12px;
}

.card .card-desc {
  font-size: 0.875rem;
  color: var(--color-text-muted);
  line-height: 1.5;
  flex: 1;
}

.card time {
  font-family: var(--font-mono);
  font-size: 0.75rem;
  color: var(--color-text-muted);
  margin-top: 16px;
  opacity: 0.7;
}

/* === Placeholder Card === */
.card-placeholder {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 28px 24px;
  border: 1px dashed rgba(255, 255, 255, 0.12);
  border-radius: 12px;
  text-align: center;
  min-height: 200px;
}

.card-placeholder .plus {
  font-size: 2rem;
  color: rgba(255, 255, 255, 0.15);
  margin-bottom: 12px;
}

.card-placeholder p {
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.25);
}

/* === Footer === */
.footer {
  text-align: center;
  padding: 32px 0;
  border-top: 1px solid var(--color-card-border);
  font-size: 0.8rem;
  color: var(--color-text-muted);
  opacity: 0.6;
}

/* === Responsive === */
@media (max-width: 640px) {
  .hero {
    padding: 48px 0 40px;
  }

  .hero h1 {
    font-size: 1.5rem;
  }

  .practices-grid {
    grid-template-columns: 1fr;
  }
}
```

- [ ] **Step 2: Commit**

```bash
git add assets/css/landing.css
git commit -m "feat: add landing page stylesheet with glassmorphism theme"
```

---

### Task 4: Create landing page HTML

**Files:**
- Create: `index.html`

- [ ] **Step 1: Write the landing page HTML**

Create `index.html` at the project root:

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>maodf — Practices</title>
  <meta name="description" content="A collection of tech practices and presentations by maodf.">

  <!-- Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&family=JetBrains+Mono:wght@400&display=swap" rel="stylesheet">

  <!-- Styles -->
  <link rel="stylesheet" href="assets/css/landing.css">
</head>
<body>
  <div class="container">

    <header class="hero">
      <img src="assets/images/avatar.jpeg" alt="maodf" class="avatar">
      <h1>maodf</h1>
      <p class="bio">A Carbon-based Token Generator</p>
      <p class="contact">
        <a href="mailto:mdengfeng@gmail.com">&#9993; mdengfeng@gmail.com</a>
      </p>
    </header>

    <main>
      <div class="section-header">
        <h2>Practices / 实践</h2>
      </div>

      <div class="practices-grid">

        <a href="practices/claude-code/" class="card">
          <span class="card-icon">&#129302;</span>
          <h3>Claude Code 落地实践</h3>
          <p class="card-subtitle">AI-Powered Full-Stack Development</p>
          <p class="card-desc">以 ZPod 项目为例，从 PRD 到上线的 AI 全栈开发实践。涵盖 PRD 驱动开发、分阶段实现、远程部署闭环等核心工作流。</p>
          <time>2026/04/29</time>
        </a>

        <div class="card-placeholder">
          <span class="plus">+</span>
          <p>More coming soon<br>更多即将到来</p>
        </div>

      </div>
    </main>

    <footer class="footer">
      <p>&copy; 2026 maodf &middot; Built with Claude Code</p>
    </footer>

  </div>
</body>
</html>
```

- [ ] **Step 2: Verify the landing page serves correctly**

```bash
python3 -m http.server 8080 &
sleep 1
curl -s http://localhost:8080/ | grep -c 'maodf'
curl -s http://localhost:8080/ | grep -c 'practices/claude-code/'
kill %1
```

Expected: Both return at least `1`.

- [ ] **Step 3: Verify the practice link works (card click-through)**

```bash
python3 -m http.server 8080 &
sleep 1
curl -s -o /dev/null -w "%{http_code}" http://localhost:8080/practices/claude-code/
kill %1
```

Expected: `200`.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: create landing page with hero section and practices card grid"
```

---

### Task 5: Update README.md

**Files:**
- Modify: `README.md`

- [ ] **Step 1: Write an updated README**

Replace the contents of `README.md`:

```markdown
# Practices

A collection of tech practices and presentations by maodf.

## Structure

```
practices/
└── claude-code/    # Claude Code 落地实践 — AI full-stack dev with ZPod
```

## View

Open `index.html` in a browser, or serve with any static file server:

```bash
python3 -m http.server 8080
```

## Add a new practice

1. Create `practices/<topic>/` with `index.html` + assets
2. Add a card to root `index.html`
```

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "docs: update README with new structure and usage instructions"
```

---

### Task 6: Clean up and final verification

**Files:**
- Verify: all old root-level files are gone
- Verify: landing page and practice presentation both load

- [ ] **Step 1: Verify no stale files remain at root**

```bash
ls -la *.png *.css *.jpeg 2>/dev/null | wc -l
```

Expected: `0` (all moved to subdirectories).

- [ ] **Step 2: Verify presentation.html symlink is gone**

```bash
test -L presentation.html && echo "SYMLINK EXISTS" || echo "CLEAN"
test -f presentation.html && echo "FILE EXISTS" || echo "CLEAN"
```

Expected: Both output `CLEAN`.

- [ ] **Step 3: Start server and verify full site**

```bash
python3 -m http.server 8080 &
PID=$!
sleep 1

echo "--- Landing page ---"
curl -s -o /dev/null -w "%{http_code}" http://localhost:8080/
echo ""

echo "--- Practice page ---"
curl -s -o /dev/null -w "%{http_code}" http://localhost:8080/practices/claude-code/
echo ""

echo "--- Avatar image ---"
curl -s -o /dev/null -w "%{http_code}" http://localhost:8080/assets/images/avatar.jpeg
echo ""

echo "--- Practice images ---"
curl -s -o /dev/null -w "%{http_code}" http://localhost:8080/practices/claude-code/images/img1.png
echo ""
curl -s -o /dev/null -w "%{http_code}" http://localhost:8080/practices/claude-code/images/img2.png
echo ""
curl -s -o /dev/null -w "%{http_code}" http://localhost:8080/practices/claude-code/images/bash_mode.png
echo ""

kill $PID
```

Expected: All return `200`.

- [ ] **Step 4: Open in browser for visual verification**

Serve the site and open in a browser to check:
- Landing page loads with dark gradient background
- Avatar displays correctly (sheep character)
- Card hover effect works (lift + glow)
- Clicking the Claude Code card navigates to the presentation
- Presentation images all display correctly
- Responsive layout works on narrow viewport

- [ ] **Step 5: Final commit if any cleanup needed**

```bash
git status
```

If clean, no commit needed. If any unstaged changes remain, stage and commit.
