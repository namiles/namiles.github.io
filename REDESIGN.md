# Redesign — "Topology"

A dark, network-engineering-themed redesign of the personal site, built as a single
self-contained file: [`redesign.html`](redesign.html). No external fonts, scripts, or
assets beyond the existing favicons/manifest — it drops straight into GitHub Pages next
to `index.html`.

Preview it (once pushed) at `nickmiles.io/redesign.html`, or open the file locally.

## Concept

The site is styled after a network operator's world: a live topology graph, terminal
panels, monospace data, and connection-themed motion. Committed to a **single dark
theme** by design (no light mode).

## Design system

- **Palette** (CSS custom properties in `:root`)
  - Ground: `--bg #080b12`, panels `--panel #10192b` / `--panel-2 #0c1424`
  - Text: `--ink #d3dcec`, `--ink-dim #8996ac`, `--ink-faint #5b687e`
  - Accent: `--accent #2fe0c0` (teal), `--accent-2 #17b9d8` (cyan)
  - Status/highlight: `--up #46e08a` (green — pulse dot & graph packets)
  - Hairlines: `--line` / `--line-2` (teal-tinted, low alpha)
- **Type**: system sans for display/body, monospace (`--mono`) for all technical/data
  bits (status line, labels, chips, terminal, buttons).
- **Layout**: full-viewport sections that **scroll-snap** one screen at a time.

## Structure

1. **Hero** — animated canvas network graph (drifting nodes, links that light near the
   cursor, traveling packets). Status line, `Hi, I'm Nick.`, `// Network Engineer`,
   LinkedIn + GitHub icons, scroll-cue arrow.
2. **01 — About** — a terminal panel titled `rtr1.nickmiles.io`. A `cat about.txt`
   command prompt sits above the bio. Contains the **View My Resume** (Google Drive) and
   **View My Certifications** (Credly) buttons.
3. **02 — Ping Me** — two-column: heading + TCP-handshake animation on the left, email
   address + **Email Me** button on the right. Footer lives inside this section.

## Key interactions / animations

- **Scroll snapping** — `scroll-snap-type: y mandatory`; each section is a full-height
  snap stop. Guarded to viewports ≥ 680px tall and disabled under reduced-motion.
- **Hero load-in** — staggered fade-up cascade (status → name → role → socials → cue).
- **Live topology** — `<canvas>` graph in the hero; reacts to the pointer, draws one
  static frame under reduced-motion.
- **`cat about.txt` typing** — types out character-by-character when About scrolls into
  view; caret is solid while typing, then blinks.
- **TCP three-way handshake** — under the "establish a connection?" heading: `SYN →
  SYN-ACK → ACK → connection established`, with endpoint dots lighting up. Replays each
  time the section enters view.

## Responsiveness & accessibility

- Hero content centers on mobile (≤ 640px); contact columns stack (≤ 800px).
- Every animation has a `prefers-reduced-motion: reduce` fallback (static final states).
- `:focus-visible` outlines, `aria-label`s on icon links, decorative graphics marked
  `aria-hidden`.

## Content sources (unchanged from original site)

- Resume: Google Drive link
- Certifications: `https://www.credly.com/users/nicholasamiles/badges/credly`
- Email: `nick@nickmiles.io` · LinkedIn `/in/nickamiles` · GitHub `@namiles`

## Promoting to the live homepage (not yet done)

`redesign.html` is a preview only; `index.html` is still the live site. When ready:

1. Back up the current homepage: `index.html` → `index-old.html`.
2. Rename `redesign.html` → `index.html`.
3. Commit & push (GitHub Pages + `CNAME` continue to work unchanged).

## Notes / open decisions

- Accent color: experimented with blue (`#3d9bff`) and orange (`#ff8a3d`); reverted to
  the original teal/green.
- About bio paragraphs currently span the full panel width (no max-width cap).
