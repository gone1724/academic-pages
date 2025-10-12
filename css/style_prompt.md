# Reusable UI Spec – Soft Dashboard + Hard-Edge Shadow

This document describes the styling rules used in this repo so an AI agent can quickly reproduce the same look-and-feel in other projects. It favors a clean dashboard style, rounded cards, clear black outlines, and hard-edge shadows (no blur).

## 1. Visual Language

- Palette: neutral beige background (#F7F3EE) with white cards. Strong black outlines. Accent pastels for badges and buttons.
- Typography: Source Sans Pro (or system UI), 16–18px body, semi-bold section titles.
- Corners: cards 20–22px, buttons/badges 14–18px.
- Shadow (hard edge): `box-shadow: 2px 2px 0 #000` default; hover `3px 3px 0 #000`; active `1px 1px 0 #000`.
- Borders: 2px solid black for most components; list items 1px; thumbnails 1px very light (`rgba(0,0,0,.25)`).

## 2. Layout Rules

- Page container `.container` is frameless: centered, transparent background, no outer border/shadow. Spacing comes from internal cards.
- Sections are wrapped by `.panel` cards (white background, 2px black border, hard-edge shadow). Each section starts with `h2`.
- `h2` alignment: left-aligned, with `padding-left: 2ch` for a subtle indent; no border around the title itself.
- There is no “summary grid” metrics row in this style.

## 3. Components

### 3.1 Avatar
- Size: 132px width
- Border: 3px solid white (`#fff`)
- Border-radius: 20px (rounded rectangle)
- Shadow: multi-layer for 3D floating effect
  - Outer shadow: `0 6px 12px rgba(0, 0, 0, 0.08)`
  - White glow: `0 0 10px rgba(255, 255, 255, 0.6)`
  - Inner highlight: `inset 0 1px 2px rgba(255, 255, 255, 0.4)`
- Hover effect: lifts up 4px (`translateY(-4px)`) with enhanced shadow
- Transition: smooth 0.3s ease for transform and box-shadow
- Positioning: `display: block; margin: 0 auto 1em auto`
- Image fit: `object-fit: cover` to ensure proper cropping

### 3.2 Social Badges (contact shortcuts)
- Markup: `.social-row` contains multiple `.social-item` links.
- Structure: `a.social-item > span.badge > img + span(label)`
- Styles:
  - Outline: `border: 2px solid #000` with rounded corners (16px).
  - Shadow: hard-edge shadow as in Visual Language.
  - Badge shape: rounded-square 28×28, own outline (2px) and colored fill.
  - Ordering (CSS only, HTML order optional):
    1) `.email` 2) `.orcid` 3) link to `github.com` 4) `.oshwhub` 5) link to `bilibili.com` 6) link to `/images/QRcode` (WeChat).
- Brand colors (badge background):
  - Email `.email`: `#aa96da`
  - ORCID `.orcid`: `#a6ce39`
  - OSHWHUB `.oshwhub`: `#6e9df1`
  - Others may use repo variables (`--blue`, `--green`, `--pink`, `--yellow`).

### 3.3 Language Switch
- `.language-switch` positioned absolutely at top-right corner (`position: absolute; top: 20px; right: 20px`).
- `.language-switch a` is a colored pill with hard-edge shadow.
- Background: `#f7f1f0`; border: 2px solid black; radius: 16px; same hover/active shadow pattern as social badges.

### 3.4 Panels, Lists and Media
- Section card `.panel`: white background, 2px black border, hard-edge shadow.
- List item `.panel .list-item`: 1px black border, rounded 16px, inner spacing 10px.
- Thumbnail `.panel .list-image`: width ≈56px, 1px `rgba(0,0,0,.25)` border, 8px radius, subtle shadow.

### 3.5 Tag Container
- `.tag-container`: flexible container for displaying tags/keywords in pill format.
- Structure: `div.tag-container > span` (each span is a tag)
- Styles:
  - Container: `display: flex; flex-wrap: wrap; gap: 10px; margin-top: 12px`
  - Tags: white background, 2px black border, fully rounded (`border-radius: 999px`)
  - Padding: `6px 14px`, font-size: `0.9em`
  - Shadow: same hard-edge shadow pattern as other components
  - Hover effect: slight lift (`translateY(-2px)`) with background color change

## 4. CSS Variable Hints

Recommended variables (already used in this repo):

- Core: `--background-color: #F7F3EE`, `--container-bg: #fffefb`, `--border-color: #121212`
- Pastels: `--blue: #7db8ff`, `--green: #8ed7b0`, `--pink: #f59abc`, `--yellow: #f6cf66`
- Extra accents: `--lavender: #aa96da`, `--tangerine: #ffaa64`, `--rose: #c06c84`
- Radii: `--border-radius: 22px`, `--button-radius: 16px`

## 5. Minimal HTML Skeleton

```
<div class="container">
  <div class="language-switch"><a href="/zh/index.html">中文</a></div>
  <img class="avatar" ... />
  <h1>...</h1>
  <p class="title">...</p>

  <div class="social-row">
    <a class="social-item email"><span class="badge"><img ... /></span><span>Email</span></a>
    <a class="social-item orcid"><span class="badge"><img ... /></span><span>ORCID</span></a>
    <!-- github / oshwhub / bilibili / wechat -->
  </div>

  <div class="panel">
    <h2>Section Title</h2>
    <ul class="list-container">
      <li class="list-item"><img class="list-image" ... /><div class="list-text">...</div></li>
    </ul>
  </div>

  <div class="panel">
    <h2>Interests</h2>
    <div class="tag-container">
      <span>Tag 1</span>
      <span>Tag 2</span>
      <span>Tag 3</span>
    </div>
  </div>
</div>
```

## 6. Prompt Snippets (for LLM/UI generators)

- “Create a frameless page with transparent container and multiple rounded section cards. Each card uses white background, 2px black outline, and a hard-edge shadow (2px 2px 0 #000). Headings are left-aligned with a 2ch left indent. Add a social row of rounded-square badges with brand colors (email #aa96da, orcid #a6ce39, oshwhub #6e9df1). Language switch is a colored pill (#f7f1f0) with the same hard-edge shadow.”

- “List items inside a card have a thinner 1px outline and thumbnails have a nearly invisible 1px rgba(0,0,0,0.25) border with 8px radius. Preserve ample whitespace and simple, readable typography.”

## 7. Notes

- Reuse these classes to port the UI quickly.
- Prefer CSS ordering for social badges so HTML order is flexible across languages.
- Avoid gradients and heavy glass effects; rely on flat fills and crisp outlines.

— End of spec —
