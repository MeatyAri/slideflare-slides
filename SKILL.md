---
name: slideflare-slides
description: >
  Create and edit SlideFlare slides — a markdown-based presentation tool with LaTeX math,
  HTML components, Tailwind CSS styling, and embedded media. Agents can produce complete
  slide decks, individual slides, or modify existing `.md` slide files.
  Supports custom components via HTML + Tailwind, math via $...$ (inline) and $$...$$ (display),
  images, videos, and any Tailwind utility class.
  Use when user asks to create slides, presentations, slide decks, or edit SlideFlare .md files.
---

# SlideFlare Slides Agent Skill

SlideFlare presentations are plain Markdown files with YAML frontmatter per slide, separated by `---` dividers. Each slide renders as a full-viewport section with Tailwind CSS styling, Markdown content, LaTeX math, and arbitrary HTML.

## File Format

### Slide Structure

```markdown
---
bg_color: bg-slate-900
text_color: text-white
title: Slide Title (optional)
---

# Heading

Content goes here with **bold**, *italic*, lists, etc.

---
bg_color: bg-gradient-to-br from-blue-600 to-purple-700
text_color: text-white
title: Next Slide
---

More content...
```

### Frontmatter Fields (per slide)

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `bg_color` | string | `""` | Tailwind background class (e.g., `bg-blue-600`, `bg-gradient-to-r from-cyan-500 to-blue-500`) |
| `text_color` | string | `""` | Tailwind text class (e.g., `text-white`, `text-center`, `text-xl`) |
| `title` | string | `"Untitled"` | Slide title shown in navigation |

### Slide Separators

- Slides are separated by `---` on its own line
- Each slide section has `---` opening and closing the frontmatter block
- The last slide does **not** need a trailing `---` divider — the end of file marks the end of the last slide
- Minimum: one `---` pair per slide (opening frontmatter + closing divider)

## Markdown Support

Full GitHub Flavored Markdown:

- **Headings**: `# H1`, `## H2`, `### H3`
- **Emphasis**: `**bold**`, `*italic*`, `~~strikethrough~~`
- **Lists**: ordered, unordered, task lists (`- [ ]`, `- [x]`)
- **Code**: inline `` `code` `` and fenced code blocks with language
- **Tables**: GFM tables
- **Links & Images**: `[text](url)`, `![alt](path)`
- **Blockquotes**: `> quote`
- **Footnotes**: `[^1]`

## LaTeX Math

Inline math: `$E = mc^2$`
Display math: `$$\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}$$`

Renders to MathML via pulldown-latex. Use `$$...$$` for centered display equations.

## Tailwind CSS

Every slide gets a Tailwind-enabled `<article>` with `prose prose-invert lg:prose-xl` base styling. You have full access to:

- **All Tailwind utility classes** on the slide container via `bg_color` and `text_color`
- **All Tailwind utility classes** inside HTML blocks using `<div class="...">`
- **Custom styling** via inline Tailwind classes in any HTML markup

### Background & Text Classes

```markdown
---
bg_color: bg-gradient-to-br from-indigo-900 via-purple-900 to-slate-900
text_color: text-white text-center
---

# Centered on gradient background
```

### Common Patterns

```markdown
---
bg_color: bg-slate-900
text_color: text-white
---

# Dark slide with white text

---
bg_color: bg-gradient-to-r from-amber-400 to-orange-500
text_color: text-white text-center
---

# Warm gradient with centered text

---
bg_color: bg-gray-100
text_color: text-gray-900
---

# Light slide with dark text
```

## HTML Components

You can embed arbitrary HTML for custom layouts and components. Tailwind classes work inside HTML.

### Blank Line Rule

**Always place a blank line between an opening HTML tag and the first Markdown element inside it, and between the last Markdown element and the closing HTML tag.** This ensures the Markdown parser correctly detects headings, lists, and other block-level elements.

```markdown
<!-- ❌ WRONG — Markdown headings won't be detected -->
<div class="p-6 bg-white/10 rounded-xl">
## Left Column
Content here
</div>

<!-- ✅ CORRECT — blank lines separate HTML from Markdown -->
<div class="p-6 bg-white/10 rounded-xl">

## Left Column
Content here

</div>
```

### Cards

```markdown
<div class="card bg-white/10 backdrop-blur-sm p-8 rounded-2xl border border-white/20 max-w-2xl">

## Card Title

Content inside a glassmorphism card.

</div>
```

### Grid Layouts

```markdown
<div class="grid grid-cols-2 gap-8 max-w-4xl">

<div class="p-6 bg-white/10 rounded-xl">

## Left Column
Content here

</div>

<div class="p-6 bg-white/10 rounded-xl">

## Right Column
Content here

</div>

</div>
```

### Flexbox Layouts

```markdown
<div class="flex items-center justify-between gap-4 max-w-5xl">

<div class="flex-1">

## Section A
Content

</div>

<div class="flex-1 text-right">

## Section B
Content

</div>

</div>
```

### Custom Styled Elements

```markdown
<div class="flex flex-col items-center justify-center text-center">

<span class="text-8xl font-bold bg-gradient-to-r from-cyan-400 to-purple-500 bg-clip-text text-transparent">
🔥 SlideFlare
</span>

<p class="mt-4 text-xl text-gray-300">Beautiful slides, powered by markdown</p>

</div>
```

### Animated / Interactive Elements

```markdown
<div class="space-y-4 max-w-3xl">

<div class="p-4 bg-blue-500/20 border-l-4 border-blue-400 rounded-r-lg">

**Key Insight:** This is a highlighted callout box.

</div>

<div class="p-4 bg-green-500/20 border-l-4 border-green-400 rounded-r-lg">

**Example:** Code or data example goes here.

</div>

</div>
```

### Tables with Custom Styling

```markdown
<div class="overflow-x-auto">

| Feature | Status | Priority |
|---------|--------|----------|
| Markdown | ✅ Done | High |
| Math | ✅ Done | High |
| Animations | 🚧 WIP | Medium |

</div>
```

## Media

### Images

```markdown
![Description](./path/to/image.png)

<div class="text-center">
![Hero Image](./images/hero.webp)
</div>
```

Images are embedded as Base64 data URLs by the parser. Supports PNG, JPG, GIF, SVG, WebP.

### Videos

```markdown
<video controls width="600" class="rounded-xl">
  <source src="./videos/demo.mp4" type="video/mp4">
</video>

<video autoplay loop muted width="80%">
  <source src="./videos/background.mp4" type="video/mp4">
</video>
```

Supports MP4, WebM, AVI, MOV, OGV. Videos are embedded as Base64 data URLs.

## Complete Slide Deck Examples

### Example 1: Tech Talk Deck

```markdown
---
bg_color: bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900
text_color: text-white
title: Rust for Web Development
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

---
bg_color: bg-slate-900
text_color: text-white
title: Performance Comparison
---

## Benchmark Results

$$
T(n) = O(n \log n) \text{ comparison sort}
$$

| Language | Time (ms) | Memory (MB) |
|----------|-----------|-------------|
| Rust | 12.4 | 4.2 |
| Go | 18.7 | 6.1 |
| Python | 142.3 | 28.5 |

---
bg_color: bg-gradient-to-r from-emerald-600 to-teal-700
text_color: text-white text-center
title: Thank You!
---

<div class="flex flex-col items-center justify-center">

<span class="text-6xl mb-4">🚀</span>

## Questions & Discussion

<div class="mt-6 space-x-4">
<span class="text-2xl">📧 email@example.com</span>
<span class="text-2xl">🐦 @username</span>
</div>

</div>
```

### Example 2: Math Lecture

```markdown
---
bg_color: bg-white
text_color: text-gray-900
title: Linear Algebra
---

# Eigenvalues & Eigenvectors

For a square matrix $A$, an eigenvector $v$ satisfies:

$$
A v = \lambda v
$$

where $\lambda$ is the eigenvalue.

---
bg_color: bg-blue-50
text_color: text-gray-900
title: Characteristic Equation
---

## Finding Eigenvalues

The characteristic equation:

$$
\det(A - \lambda I) = 0
$$

For a $2 \times 2$ matrix:

$$
\begin{vmatrix}
a - \lambda & b \\
c & d - \lambda
\end{vmatrix}
= (a - \lambda)(d - \lambda) - bc = 0
$$

---
bg_color: bg-gray-900
text_color: text-white
title: Power Method
---

## Iterative Eigenvalue Computation

$$
x_{k+1} = \frac{A x_k}{\|A x_k\|}
$$

Converges to the dominant eigenvector when:

- $|\lambda_1| > |\lambda_2| \geq \cdots \geq |\lambda_n|$
- $x_0$ has a nonzero component in the direction of $v_1$

---
bg_color: bg-gradient-to-br from-indigo-100 to-purple-100
text_color: text-gray-900 text-center
title: Summary
---

<div class="max-w-2xl mx-auto space-y-4">

## Key Takeaways

1. Eigenvalues reveal the "scaling factors" of a linear transformation
2. Characteristic equation: $\det(A - \lambda I) = 0$
3. Power method converges to the dominant eigenpair
4. Applications in PCA, Google PageRank, vibration analysis

</div>
```

### Example 3: Product Pitch Deck

```markdown
---
bg_color: bg-gradient-to-br from-violet-600 via-purple-600 to-indigo-700
text_color: text-white text-center
title: SlideDeck AI
---

<div class="flex flex-col items-center justify-center text-center">

<span class="text-9xl mb-6">📊</span>

<h1 class="text-6xl font-black mb-4">SlideDeck AI</h1>

<p class="text-2xl text-white/80 mb-8">
Create stunning presentations in seconds with AI
</p>

<div class="flex gap-4">
<span class="px-6 py-3 bg-white/20 backdrop-blur rounded-full text-lg">🎨 Beautiful Templates</span>
<span class="px-6 py-3 bg-white/20 backdrop-blur rounded-full text-lg">⚡ Instant Generation</span>
</div>

</div>

---
bg_color: bg-slate-900
text_color: text-white
title: The Problem
---

## The Problem

<div class="space-y-6 max-w-3xl">

<div class="flex items-start gap-4">
<span class="text-3xl">😤</span>
<div>
<h3 class="text-xl font-bold mb-1">Hours wasted on slides</h3>
<p class="text-gray-400">Professionals spend 6+ hours per week on presentations</p>
</div>
</div>

<div class="flex items-start gap-4">
<span class="text-3xl">😵</span>
<div>
<h3 class="text-xl font-bold mb-1">Inconsistent design</h3>
<p class="text-gray-400">Most slides look unprofessional and messy</p>
</div>
</div>

<div class="flex items-start gap-4">
<span class="text-3xl">📉</span>
<div>
<h3 class="text-xl font-bold mb-1">Lost opportunities</h3>
<p class="text-gray-400">Poor slides = poor impressions = lost deals</p>
</div>
</div>

</div>

---
bg_color: bg-slate-800
text_color: text-white
title: Our Solution
---

## How It Works

<div class="grid grid-cols-3 gap-6 max-w-4xl mx-auto">

<div class="p-6 bg-white/5 rounded-2xl border border-white/10">

### 1️⃣ Describe

Share your topic and key points in plain language

</div>

<div class="p-6 bg-white/5 rounded-2xl border border-white/10">

### 2️⃣ Generate

AI creates a polished, on-brand presentation

</div>

<div class="p-6 bg-white/5 rounded-2xl border border-white/10">

### 3️⃣ Present

Export or present directly from the app

</div>

</div>

---
bg_color: bg-gradient-to-r from-emerald-500 to-teal-600
text_color: text-white text-center
title: Growth Metrics
---

## Traction

<div class="grid grid-cols-2 gap-8 max-w-3xl mx-auto">

<div class="p-8 bg-white/10 backdrop-blur rounded-2xl">
<h2 class="text-5xl font-bold mb-2">10K+</h2>
<p class="text-lg text-white/80">Active Users</p>
</div>

<div class="p-8 bg-white/10 backdrop-blur rounded-2xl">
<h2 class="text-5xl font-bold mb-2">2M+</h2>
<p class="text-lg text-white/80">Slides Created</p>
</div>

</div>

---
bg_color: bg-gradient-to-br from-amber-400 via-orange-500 to-red-500
text_color: text-white text-center
title: Join Us
---

<div class="flex flex-col items-center">

<span class="text-8xl mb-6">🚀</span>

## Join the Revolution

<p class="text-2xl mb-8">Transform how the world creates presentations</p>

<div class="flex gap-6 text-xl">
<span>📧 founders@sidedeck.ai</span>
<span>🌐 sidedeck.ai</span>
</div>

</div>
```

## Agent Workflow

### Creating a New Slide Deck

1. **Understand the topic** — what's the subject, audience, and purpose?
2. **Plan the structure** — decide on slide count (typically 5-15 slides), flow, and key messages
3. **Write the markdown** — follow the slide format with frontmatter and content
4. **Add visual variety** — use different backgrounds, layouts, and media to keep engagement
5. **Include math** — use `$...$` for inline and `$$...$$` for display equations where applicable
6. **Use HTML components** — create cards, grids, callouts, and custom layouts with Tailwind
7. **No trailing divider** — the last slide ends at EOF; no trailing `---` is needed

### Editing Existing Slides

1. **Read the existing file** — understand current structure and content
2. **Identify changes needed** — update content, add slides, modify styling
3. **Preserve format** — maintain the `---` divider structure and frontmatter
4. **Validate syntax** — ensure balanced `---` pairs and valid YAML in frontmatter

### Best Practices

- **Use `text-center`** for title slides and impact moments
- **Limit text per slide** — 3-5 bullet points, one main idea
- **Contrast is key** — light text on dark backgrounds or vice versa
- **Gradient backgrounds** add visual interest: `bg-gradient-to-br from-X to-Y`
- **Use cards** (`bg-white/10 rounded-xl p-6`) for grouped content
- **Grid layouts** for comparing items side by side
- **Callout boxes** for highlighting key insights: `border-l-4 border-X`
- **Large emojis** as visual anchors: `text-6xl` or `text-8xl`
- **Math for technical content** — always render equations properly
- **No trailing divider** — the last slide ends at EOF; do not add a trailing `---`

### Color Scheme Reference

| Theme | bg_color | text_color |
|-------|----------|------------|
| Dark default | `bg-slate-900` | `text-white` |
| Blue accent | `bg-blue-800` | `text-white` |
| Green success | `bg-emerald-600` | `text-white` |
| Warm gradient | `bg-gradient-to-r from-amber-400 to-orange-500` | `text-white` |
| Purple creative | `bg-gradient-to-br from-violet-600 to-purple-800` | `text-white` |
| Light clean | `bg-gray-50` | `text-gray-900` |
| Red alert | `bg-red-600` | `text-white` |
| Teal calm | `bg-teal-700` | `text-white` |

### Tailwind Tips for Slides

- Use `max-w-4xl` or `max-w-5xl` to constrain content width
- Use `mx-auto` to center constrained containers
- Use `space-y-4` for vertical spacing between elements
- Use `gap-6` or `gap-8` for grid/flex spacing
- Use `backdrop-blur-sm` and `bg-white/10` for glassmorphism effects
- Use `rounded-2xl` for large rounded corners on cards
- Use `border-white/20` for subtle borders on dark backgrounds
- Use `text-6xl` through `text-9xl` for large impact numbers/emojis
