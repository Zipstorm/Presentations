---
paths:
  - "presentations/**"
  - "index.html"
---

# Presentation Repository Conventions

## Directory Structure

Each presentation lives in its own folder under `presentations/`:

```
presentations/<slug>/
├── index.html   # Reveal.js presentation (required)
├── slides.md    # Companion markdown with slide content and notes (required)
└── <assets>     # Images, gifs, or other media (as needed)
```

Slugs are **kebab-case** (e.g. `jobpilot`, `quarterly-review`, `product-roadmap`).

## Reveal.js Setup

- Version: **5.1.0** via CDN
- CSS: `https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/dist/reveal.css`
- Theme: `https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/dist/theme/black.css`
- JS: `https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/dist/reveal.js`

Standard initialization:

```javascript
Reveal.initialize({
  hash: true,
  slideNumber: true,
  width: 1280,
  height: 720,
  margin: 0.04,
  transition: 'slide',
  transitionSpeed: 'default',
  backgroundTransition: 'fade',
  center: true,
  controls: true,
  progress: true,
  history: true,
});
```

## Brand / Shared CSS Variables

All presentations should use these CSS custom properties for consistency:

```css
:root {
  --seekout-blue: #4A90D9;
  --seekout-teal: #2DD4BF;
  --accent-purple: #A78BFA;
  --accent-orange: #FB923C;
  --bg-dark: #0f172a;
  --bg-card: rgba(255, 255, 255, 0.05);
  --text-muted: #94a3b8;
}
```

Font: **Inter** from Google Fonts.

## Adding a New Presentation

After creating the presentation folder and files, **always register it** in the root `index.html` by adding an entry to the `presentations` array:

```javascript
{
  slug: '<folder-name>',
  title: '<Presentation Title>',
  description: '<One-line description>',
  date: 'YYYY-MM-DD',
  authors: '<Author names>',
  project: 'Helix',         // see Vocabulary below
  type: 'Wireframes',       // see Vocabulary below
  tags: ['Tag1', 'Tag2'],   // free-form, secondary metadata
}
```

### Vocabulary

The index page uses `project` as the primary grouping (sidebar) and `type` as a small chip on each row. Keep these stable so the sidebar doesn't fragment.

**`project`** — controlled vocab:

- `Helix` — also covers SeekOut.ai work (Helix is the internal name; SeekOut.ai is the external name for the same product)
- `SPOT`
- `Other` — for one-off or hackathon work that doesn't have enough volume to deserve its own sidebar entry

Add a new top-level project only when there's enough work to justify a sidebar entry; otherwise use `Other`. Missing/unknown values fall back to `Other`.

**`type`** — controlled vocab:

- `Wireframes` — wireframes, user flows, UX specs
- `Deck` — slide decks, presentations
- `Proposal` — proposals
- `Spec` — written specifications

Topic-style labels (e.g. `Metrics`, `Strategy`, `Hackathon`, `Chrome Extension`) belong in `tags`, not `type`. Missing `type` simply renders no chip.
