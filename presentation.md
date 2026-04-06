# Introduction to Reveal.js

**HTML Presentations Made Beautiful**

slides | Markdown | themes | plugins | speaker notes | PDF export

---

## Table of Contents

1. [Agenda](#slide-02--agenda)
2. [What Is Reveal.js?](#slide-03--what-is-revealjs)
3. [Getting Started](#slide-04--getting-started)
4. [Slide Structure](#slide-05--slide-structure)
5. [Markdown Support](#slide-06--markdown-support)
6. [Transitions & Animations](#slide-07--transitions--animations)
7. [Fragments](#slide-08--fragments)
8. [Code Highlighting](#slide-09--code-highlighting)
9. [Themes](#slide-10--themes)
10. [Layout & Styling](#slide-11--layout--styling)
11. [Media & Backgrounds](#slide-12--media--backgrounds)
12. [Speaker Notes](#slide-13--speaker-notes)
13. [Configuration Options](#slide-14--configuration-options)
14. [Plugins](#slide-15--plugins)
15. [PDF Export](#slide-16--pdf-export)
16. [Multiplexing & Remote Control](#slide-17--multiplexing--remote-control)
17. [Embedding & iframes](#slide-18--embedding--iframes)
18. [Hosting & Deployment](#slide-19--hosting--deployment)
19. [Summary & Next Steps](#slide-20--summary--next-steps)

---

## Slide 02 — Agenda

### Foundations

- What is Reveal.js & its history
- Getting started — CDN, npm, CLI
- Slide structure & navigation
- Markdown support

### Visual Design

- Transitions & animations
- Fragments & step-through reveals
- Code highlighting with highlight.js
- Themes & custom styling

### Advanced Features

- Layout & responsive design
- Media & backgrounds
- Speaker notes & presenter view
- Configuration options

### Production

- Plugins & extensibility
- PDF export & printing
- Multiplexing & remote control
- Hosting & deployment

---

## Slide 03 — What Is Reveal.js?

Reveal.js is an **open-source HTML presentation framework** created by **Hakim El Hattab** in 2011. It transforms standard HTML into beautiful, interactive slide decks that run directly in the browser.

With over **67,000 GitHub stars**, it powers millions of presentations worldwide — including talks at major tech conferences, university lectures, and corporate training.

### Key Features

- Nested slides (horizontal + vertical navigation)
- Markdown support (inline and external files)
- Syntax-highlighted code with line numbers
- Speaker notes with timer and preview
- PDF export, touch support, and rich plugin API

### Who Uses It?

- Google, Mozilla, Microsoft
- University lecturers worldwide
- Conference speakers (JSConf, CSSConf)
- Developer advocates & trainers
- Open-source project maintainers

### Timeline

- **2011** — First release by Hakim El Hattab
- **2013** — Plugin ecosystem grows
- **2020** — v4.0 rewrite (ES modules)
- **2023** — v4.6 with improved accessibility

---

## Slide 04 — Getting Started

Three ways to set up a Reveal.js presentation:

### CDN (Simplest)

Link directly to hosted files. Zero setup, single HTML file, works offline once cached.

### npm Install

Full development environment with live reload, Sass compilation, and plugin management.

### CLI (create-reveal)

Scaffold a new presentation with `npx create-reveal`. Templates and configuration included.

### Minimal CDN Boilerplate

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reveal.js@4.6.1/dist/reveal.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reveal.js@4.6.1/dist/theme/black.css">
</head>
<body>
  <div class="reveal">
    <div class="slides">
      <section>Slide 1</section>
      <section>Slide 2</section>
    </div>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/reveal.js@4.6.1/dist/reveal.js"></script>
  <script>Reveal.initialize();</script>
</body>
</html>
```

---

## Slide 05 — Slide Structure

Every slide is a `<section>` element inside `.slides`. Reveal.js supports **horizontal** (left/right) and **vertical** (up/down) navigation by nesting sections.

```html
<div class="reveal">
  <div class="slides">
    <!-- Horizontal slide 1 -->
    <section>Slide 1</section>

    <!-- Vertical stack -->
    <section>
      <section>Vertical 1</section>
      <section>Vertical 2</section>
    </section>

    <!-- Horizontal slide 3 -->
    <section id="named"
             data-background="#4ecb8d"
             data-transition="zoom">
      Custom slide
    </section>
  </div>
</div>
```

### Data Attributes

- `data-background` — colour, image, video, iframe
- `data-transition` — per-slide transition
- `data-auto-animate` — morph between slides
- `data-visibility` — hidden or uncounted
- `id` — deep-linkable URL hash

### Navigation Model

- **Horizontal** = chapters or main topics
- **Vertical** = sub-topics or detail drilldowns
- Press **Esc** for the overview grid, **O** for overview mode

---

## Slide 06 — Markdown Support

Write slides in Markdown instead of HTML. Reveal.js uses the **marked** parser and supports both inline and external file Markdown.

### Inline Markdown

```html
<section data-markdown>
  <textarea data-template>
    ## Slide Title

    - Bullet one
    - Bullet two

    ```js
    console.log('Hello');
    ```
  </textarea>
</section>
```

### External Markdown File

```html
<section data-markdown="slides.md"
         data-separator="^---$"
         data-separator-vertical="^--$"
         data-separator-notes="^Notes:">
</section>
```

### Element Attributes

Add HTML attributes via special comments:

```markdown
Item 1 <!-- .element: class="fragment" -->
Item 2 <!-- .element: class="fragment" -->
```

---

## Slide 07 — Transitions & Animations

Control how slides enter and exit with transition effects. Set globally in config or per-slide with `data-transition`.

| Transition | Description |
|------------|-------------|
| `none` | Instant switch, no animation |
| `fade` | Cross-fade between slides |
| `slide` | Slide in from the right |
| `convex` | Slide with 3D convex curve |
| `concave` | Slide with 3D concave curve |
| `zoom` | Zoom in to the next slide |

```html
<!-- Per-slide transition -->
<section data-transition="zoom">
  Zooms in!
</section>

<!-- Mixed in/out -->
<section data-transition="fade-in slide-out">
  Fades in, slides out
</section>
```

### Auto-Animate

Automatically animate matching elements between consecutive slides:

```html
<section data-auto-animate>
  <h1>Hello</h1>
</section>
<section data-auto-animate>
  <h1 style="color:red;">Hello</h1>
  <p>World</p>
</section>
```

### Auto-Animate Options

- `data-auto-animate-easing` — CSS easing function
- `data-auto-animate-duration` — seconds (default 1.0)
- `data-auto-animate-unmatched` — fade or hide
- `data-id` — explicitly match elements across slides

---

## Slide 08 — Fragments

Fragments reveal elements step-by-step within a single slide. Add the `fragment` class and optionally a style class.

| Class | Effect |
|-------|--------|
| `fade-in` | Fades in (default) |
| `fade-out` | Starts visible, fades out |
| `fade-up` | Slides up while fading in |
| `fade-down` | Slides down while fading in |
| `highlight-red` | Text turns red |
| `highlight-green` | Text turns green |
| `highlight-blue` | Text turns blue |
| `grow` | Scales up |
| `shrink` | Scales down |
| `strike` | Strikethrough text |
| `semi-fade-out` | Fades to 50% opacity |

### Basic Usage

```html
<p class="fragment">Appears first</p>
<p class="fragment fade-up">Slides up</p>
<p class="fragment highlight-red">Turns red</p>
```

### Ordering & Nesting

```html
<!-- Custom order with data-fragment-index -->
<p class="fragment" data-fragment-index="2">Second</p>
<p class="fragment" data-fragment-index="1">First</p>

<!-- Nested: fade in, then highlight -->
<span class="fragment fade-in">
  <span class="fragment highlight-green">
    Two-step reveal
  </span>
</span>
```

---

## Slide 09 — Code Highlighting

Reveal.js integrates **highlight.js** for syntax highlighting across 190+ languages. Line numbers and step-through highlighting make code walkthroughs powerful.

### Basic Code Block

```html
<pre><code class="language-javascript">
function greet(name) {
  return `Hello, ${name}!`;
}
</code></pre>
```

### Line Numbers

```html
<!-- Show all line numbers -->
<pre><code data-line-numbers>
const x = 1;
const y = 2;
const z = x + y;
</code></pre>

<!-- Highlight specific lines -->
<pre><code data-line-numbers="1|3|5-7">
// Step through highlighted lines
// using the pipe separator
</code></pre>
```

### Step-Through Example

Use `data-line-numbers="1-2|3-4|5-6"` to walk through code in stages. Each pipe creates a new fragment step.

### Plugin Setup

```javascript
Reveal.initialize({
  plugins: [RevealHighlight],
  highlight: { theme: 'monokai' }
});
```

---

## Slide 10 — Themes

Reveal.js ships with **12 built-in themes**. Switch themes by changing one CSS import, or build a fully custom theme using CSS custom properties.

| Theme | Style |
|-------|-------|
| `black` | Dark background, white text (default) |
| `white` | Light background, dark text |
| `league` | Grey textured background |
| `beige` | Warm beige tones |
| `sky` | Light blue gradient |
| `night` | Dark blue background |
| `serif` | Serif fonts, cappuccino feel |
| `simple` | Minimal white design |
| `solarized` | Solarized colour scheme |
| `moon` | Dark with muted blue |
| `dracula` | Dracula colour palette |
| `blood` | Dark with red accents |

### Switching Themes

```html
<!-- Just change the CSS file -->
<link rel="stylesheet" href="dist/theme/dracula.css">
```

### Custom Theme (CSS Variables)

```css
:root {
  --r-background-color: #0a0a0f;
  --r-main-font: 'DM Sans', sans-serif;
  --r-main-color: #e8e8f0;
  --r-heading-font: 'Playfair Display', serif;
  --r-heading-color: #f5a623;
  --r-link-color: #60a5fa;
  --r-link-color-hover: #a78bfa;
  --r-selection-background-color: #f5a623;
}
```

Themes are Sass files in `css/theme/source/`. Compile with `npm run build` or write plain CSS overrides.

---

## Slide 11 — Layout & Styling

Reveal.js uses a **fixed viewport** model. Slides are authored at a reference size and scaled to fit the display. CSS Grid and Flexbox work normally inside slides.

### Viewport Configuration

```javascript
Reveal.initialize({
  width: 1100,    // Reference width in pixels
  height: 900,    // Reference height in pixels
  margin: 0.04,   // Margin around slides (fraction)
  minScale: 0.2,  // Minimum scale factor
  maxScale: 2.0   // Maximum scale factor
});
```

### CSS Grid in Slides

```css
/* Two-column layout */
.cols-2 {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0.5em;
}

/* Asymmetric 60/40 split */
.cols-6040 {
  grid-template-columns: 6fr 4fr;
}
```

### Responsive Tips

- Use **em** units for font sizes — they scale with the viewport
- Avoid fixed pixel widths; use **percentages** or **fr** units
- Test at different aspect ratios with `width` and `height`
- The `r-stretch` class auto-sizes images and media to fill available space

### Useful CSS Classes

- `r-stretch` — stretch element to fill space
- `r-fit-text` — auto-size text to fit slide
- `r-stack` — stack children on top of each other
- `r-frame` — add a thin border frame
- `r-hstack` / `r-vstack` — flex row/column

---

## Slide 12 — Media & Backgrounds

Each slide can have its own full-bleed background — colours, images, videos, or even live iframes.

### Background Types

```html
<!-- Solid colour -->
<section data-background-color="#4ecb8d">

<!-- Image -->
<section data-background-image="bg.jpg"
         data-background-size="cover"
         data-background-opacity="0.3">

<!-- Video -->
<section data-background-video="bg.mp4"
         data-background-video-loop
         data-background-video-muted>

<!-- Gradient -->
<section data-background-gradient=
  "linear-gradient(to right, #0a0a0f, #1a1a3f)">

<!-- Live iframe -->
<section data-background-iframe=
  "https://revealjs.com"
  data-background-interactive>
```

### Inline Media

```html
<!-- Auto-play video on slide enter -->
<video data-autoplay src="demo.mp4"></video>

<!-- Lazy-loaded iframe -->
<iframe data-src="https://example.com"
        width="800" height="500">
</iframe>

<!-- Stretch image to fill -->
<img class="r-stretch" src="chart.png">
```

### Background Transitions

```javascript
Reveal.initialize({
  backgroundTransition: 'fade' // or slide, convex, concave, zoom
});
```

---

## Slide 13 — Speaker Notes

Press **S** to open the **speaker view** in a new window. It shows your notes, a timer, the current slide, and a preview of the upcoming slide.

### Adding Notes in HTML

```html
<section>
  <h2>My Slide</h2>
  <p>Visible content</p>

  <aside class="notes">
    These notes are only visible
    in the speaker view.
    - Remember to mention X
    - Demo the feature live
  </aside>
</section>
```

### Notes in Markdown

```markdown
## My Slide

Visible content here.

Notes:
These notes are only visible
in the speaker view.
```

### Speaker View Features

- **Current slide** — what the audience sees
- **Next slide** — preview of what comes next
- **Notes pane** — your speaker notes (HTML supported)
- **Timer** — elapsed time since start
- **Clock** — current wall-clock time

### Plugin Setup

```javascript
import RevealNotes from 'reveal.js/plugin/notes/notes';

Reveal.initialize({
  plugins: [RevealNotes]
});
```

Speaker view works cross-window. Open it on your laptop screen while projecting the main presentation on the big screen.

---

## Slide 14 — Configuration Options

Reveal.js exposes dozens of configuration properties. Pass them to `Reveal.initialize()` to customise every aspect of behaviour.

| Option | Default | Description |
|--------|---------|-------------|
| `controls` | `true` | Show navigation arrows |
| `progress` | `true` | Show progress bar |
| `hash` | `false` | Update URL hash on slide change |
| `history` | `false` | Push slide changes to browser history |
| `keyboard` | `true` | Enable keyboard navigation |
| `touch` | `true` | Enable touch/swipe navigation |
| `loop` | `false` | Loop the presentation |
| `autoSlide` | `0` | Auto-advance interval (ms) |
| `center` | `true` | Vertically centre slide content |
| `embedded` | `false` | Run inside an iframe |

### Full Example

```javascript
Reveal.initialize({
  hash: true,
  history: true,
  transition: 'fade',
  transitionSpeed: 'fast',
  controls: true,
  progress: true,
  center: false,
  slideNumber: 'c/t',
  width: 1100,
  height: 900,
  margin: 0.04,
  autoSlide: 0,
  autoSlideStoppable: true,
  plugins: [RevealHighlight, RevealNotes, RevealMarkdown]
});
```

---

## Slide 15 — Plugins

Reveal.js has a modular plugin system. Built-in plugins ship with the framework; third-party plugins extend it further.

### Built-in Plugins

- **RevealHighlight** — syntax highlighting
- **RevealMarkdown** — Markdown slide authoring
- **RevealNotes** — speaker notes + presenter view
- **RevealMath** — LaTeX / MathJax / KaTeX rendering
- **RevealSearch** — Ctrl+Shift+F search within slides
- **RevealZoom** — Alt+click zoom into elements

### Popular Third-Party Plugins

- **reveal-plantuml** — UML diagrams from text
- **reveal.js-menu** — hamburger slide menu
- **reveal.js-copycode** — copy button for code blocks
- **reveal-sampler** — embed code from external files

### Writing a Custom Plugin

```javascript
const MyPlugin = {
  id: 'my-plugin',

  init: (reveal) => {
    console.log('Slides:', reveal.getTotalSlides());

    reveal.on('slidechanged', (event) => {
      console.log('Now on slide', event.indexh);
    });

    reveal.getSlides().forEach(slide => {
      // Modify slides programmatically
    });
  },

  destroy: () => {
    // Cleanup when plugin is removed
  }
};

Reveal.initialize({
  plugins: [MyPlugin]
});
```

---

## Slide 16 — PDF Export

Reveal.js supports PDF export through a special print stylesheet. Append `?print-pdf` to your URL, then use the browser's Print dialog.

### Browser Export (Built-in)

1. Navigate to `presentation.html?print-pdf`
2. Open Print dialog (Ctrl+P / Cmd+P)
3. Set paper size to match slide dimensions
4. Enable "Background graphics"
5. Save as PDF

### Print-Specific CSS

```css
@media print {
  .reveal .slides section {
    page-break-after: always;
    min-height: 100%;
  }
  .no-print { display: none; }
}
```

### Decktape (CLI Tool)

For reliable, automated PDF export, use **Decktape** — a headless Chrome-based tool designed for slide decks.

```bash
# Install globally
npm install -g decktape

# Export to PDF
decktape reveal http://localhost:8000 output.pdf

# Custom page size
decktape reveal --size 1100x900 presentation.html slides.pdf
```

### Tips for Good PDFs

- Fragments become separate pages (each step = one page)
- Backgrounds and gradients export correctly
- Test with `?print-pdf` before your talk
- Use `pdfSeparateFragments: false` to collapse fragments

---

## Slide 17 — Multiplexing & Remote Control

The **multiplex plugin** lets a presenter control slide navigation across multiple client browsers in real time via **Socket.io**.

### How It Works

- **Master** — presenter's browser broadcasts slide changes
- **Client** — audience browsers receive and follow along
- Communication via a **Socket.io server** (self-hosted or public)
- Secret token prevents audience from hijacking navigation

### Master Configuration

```javascript
Reveal.initialize({
  multiplex: {
    secret: 'your-secret-token',
    id: 'presentation-id',
    url: 'https://reveal-multiplex.glitch.me'
  },
  plugins: [RevealMultiplex]
});
```

### Client Configuration

```javascript
Reveal.initialize({
  multiplex: {
    id: 'presentation-id',
    url: 'https://reveal-multiplex.glitch.me'
  },
  plugins: [RevealMultiplex]
});
```

### Alternatives

- **reveal-remote** — mobile phone remote control
- **Spotlight plugin** — laser pointer via mouse
- **Presentation API** — W3C standard for dual-screen
- **WebRTC-based** — peer-to-peer without a server

---

## Slide 18 — Embedding & iframes

Reveal.js presentations can embed external content and also be embedded inside other pages. Lazy loading ensures performance stays snappy.

### Embedding Content in Slides

```html
<!-- Lazy-loaded iframe -->
<iframe data-src="https://codepen.io/..."
        width="100%" height="500">
</iframe>

<!-- Background iframe (full slide) -->
<section data-background-iframe=
           "https://threejs.org/examples/"
         data-background-interactive>
</section>

<!-- Auto-play media on slide enter -->
<video data-autoplay data-src="demo.mp4"
       width="800"></video>
```

### Embedding a Reveal Deck in a Page

```html
<iframe src="slides.html"
        width="800" height="600"
        frameborder="0">
</iframe>
```

```javascript
Reveal.initialize({
  embedded: true,
  keyboardCondition: 'focused'
});
```

### Post-Message API

Control an embedded deck from the parent page:

```javascript
const iframe = document.querySelector('iframe');
iframe.contentWindow.postMessage(
  JSON.stringify({ method: 'slide', args: [2, 0] }),
  '*'
);
```

---

## Slide 19 — Hosting & Deployment

Reveal.js presentations are **static HTML** — deploy them anywhere you can serve files. No server-side runtime required.

### GitHub Pages

- Push your `index.html` to a repo
- Enable Pages in repo Settings > Pages
- Available at `username.github.io/repo`
- Free HTTPS, custom domains supported

### Static Hosting Platforms

- **Netlify** — drag-and-drop or Git deploy
- **Vercel** — zero-config static hosting
- **Cloudflare Pages** — fast edge CDN
- **AWS S3 + CloudFront** — scalable and cheap
- **Surge.sh** — `npx surge .` one-liner deploy

### Single-File Approach

Load Reveal.js from a CDN — your entire presentation is a single `index.html` file. No build step, no dependencies. Email it, put it on a USB stick, or host it anywhere.

### CI/CD Pipeline

```yaml
# .github/workflows/deploy.yml
name: Deploy Slides
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v4
      - uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
      - uses: actions/deploy-pages@v4
```

---

## Slide 20 — Summary & Next Steps

### What We Covered

- Reveal.js fundamentals — HTML slide structure
- Markdown authoring & external files
- Transitions, fragments, auto-animate
- Code highlighting with line step-through
- 12 built-in themes & custom CSS variables
- Layout, media, and backgrounds
- Speaker notes & presenter view
- Plugin architecture & custom plugins
- PDF export, multiplexing, embedding
- Deployment to GitHub Pages & static hosts

### Recommended Next Steps

- Build a presentation from scratch using CDN
- Try Markdown mode with external `.md` files
- Experiment with auto-animate and fragments
- Write a custom plugin using the API
- Deploy to GitHub Pages for free hosting

### Essential Resources

- **revealjs.com** — official docs & live demos
- **github.com/hakimel/reveal.js** — source code
- **revealjs.com/plugins** — plugin directory
- **slides.com** — visual editor built on Reveal.js
- **github.com/hakimel** — Hakim El Hattab's projects

**Thank you!** — Built with Reveal.js · Single self-contained HTML file
