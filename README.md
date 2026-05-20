# SlideFlare Slides — AI Agent Skill

> Create and edit SlideFlare presentations with AI. Write markdown-based slides with LaTeX math, HTML components, Tailwind CSS styling, and embedded media.

[SlideFlare](https://github.com/MeatyAri/slideflare) is a blazing-fast, interactive presentation tool built with Rust + SvelteKit. This agent skill enables AI agents to produce complete slide decks, individual slides, or modify existing presentations — all in plain markdown.

## ✨ What You Can Do

- **Generate full slide decks** from a topic description
- **Edit existing slides** — update content, add/remove slides, tweak styling
- **Write LaTeX math** — inline `$E = mc^2$` and display `$$\int f(x)dx$$`
- **Build custom HTML components** — cards, grids, callouts, animated elements
- **Style everything with Tailwind CSS** — backgrounds, typography, layouts
- **Embed media** — images and videos (auto-embedded as Base64)

## Quick Start

### Create a Slide

```markdown
---
bg_color: bg-gradient-to-br from-indigo-900 to-purple-900
text_color: text-white
title: Hello World
---

# Welcome to SlideFlare

- Beautiful markdown presentations
- LaTeX math support
- Custom HTML components
- Powered by Tailwind CSS

---
bg_color: bg-slate-800
text_color: text-white
---

## Math in Action

The quadratic formula:

$$x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$

---
```

### File Format

Each slide is a markdown section separated by `---`, with YAML frontmatter controlling styling:

| Field | Description |
|-------|-------------|
| `bg_color` | Tailwind background class (e.g. `bg-blue-600`) |
| `text_color` | Tailwind text class (e.g. `text-white text-center`) |
| `title` | Slide title for navigation |

## Features

| Feature | Syntax | Example |
|---------|--------|---------|
| **Headings** | `# H1` `## H2` | Section titles |
| **Math** | `$...$` / `$$...$$` | `$\sum_{i=1}^n i$` |
| **Lists** | `- item` / `1. step` | Bullet and numbered lists |
| **Code** | `` `code` `` / fenced blocks | Syntax-highlighted snippets |
| **Images** | `![alt](path)` | Auto-embedded Base64 |
| **Videos** | `<video src="...">` | Auto-embedded Base64 |
| **Cards** | `<div class="card ...">` | Glassmorphism panels |
| **Grids** | `<div class="grid ...">` | Multi-column layouts |

## Examples

### Tech Talk Deck

```markdown
---
bg_color: bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900
text_color: text-white
title: Rust for Web Dev
---

# Rust for the Web 🦀

Building fast, safe, and beautiful web applications

---
bg_color: bg-slate-800
text_color: text-white text-center
title: Why Rust?
---

<div class="grid grid-cols-3 gap-6 max-w-4xl mx-auto">

<div class="p-6 bg-white/5 rounded-xl text-center">
## ⚡ Speed
Near C-level performance
</div>

<div class="p-6 bg-white/5 rounded-xl text-center">
## 🛡️ Safety
Memory safety without GC
</div>

<div class="p-6 bg-white/5 rounded-xl text-center">
## 🧩 Concurrency
Fearless parallelism
</div>

</div>
```

### Math Lecture

```markdown
---
bg_color: bg-white
text_color: text-gray-900
title: Linear Algebra
---

# Eigenvalues & Eigenvectors

For a square matrix $A$, an eigenvector $v$ satisfies:

$$Av = \lambda v$$

where $\lambda$ is the eigenvalue.
```

### Product Pitch

```markdown
---
bg_color: bg-gradient-to-br from-violet-600 via-purple-600 to-indigo-700
text_color: text-white text-center
title: SlideDeck AI
---

<div class="flex flex-col items-center">

<span class="text-9xl mb-6">📊</span>

<h1 class="text-6xl font-black mb-4">SlideDeck AI</h1>

<p class="text-2xl text-white/80">
Create stunning presentations in seconds
</p>

</div>
```

## Installation

Drop the `slideflare-slides` folder into your agent's skills directory:

```bash
# For AI agents that support skills directories
cp -r slideflare-slides ~/.agents/skills/

# Or wherever your agent reads skills from
```

The agent will automatically pick up the skill and use it when you ask about slides, presentations, or SlideFlare.

## File Extension

SlideFlare presentations use the `.md` extension — they're just markdown files. Drag and drop them into the SlideFlare app to view them.

## License

[Apache 2.0](../../LICENSE) — Part of the SlideFlare ecosystem.
