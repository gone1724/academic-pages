# Reusable UI Spec – Soft Dashboard + Hard-Edge Shadow

Shared design language for the Academic Homepage. Use this document to reproduce the same look across new sections or pages.

## 1. Visual Language

- **Palette**: Warm neutral background `#F7F3EE`, white cards, strong black outlines. Accent pastels come from project variables (`--blue`, `--green`, `--pink`, `--yellow`, etc.).
- **Typography**: Source Sans Pro (fall back to system UI). Body copy ~17px, section titles semi-bold.
- **Corners**: Cards ~22px radius; buttons/pills ~16px.
- **Shadows**: Prefer hard-edge shadows. Default `box-shadow: 2px 2px 0 #000`; hover `3px 3px 0 #000`; active `1px 1px 0 #000`.
- **Borders**: 2px black for major components. Secondary items (lists, thumbnails, tags) use 1px outlines.

## 2. Layout Rules

- `.container` stays frameless and centered with transparent background. Spacing is handled inside panels.
- Every content block lives inside a `.panel`: white fill, 2px black border, hard-edge shadow.
- `h2` headers are left-aligned with a subtle left indent (`padding-left: 1ch` or `2ch`).
- **No summary metrics grid** is present in this build; keep sections card-based.

## 3. Components

### 3.1 Profile
- Avatar width: 132px (140px on small devices).
- Rounded rectangle (`border-radius: 20px`), no visible border, multi-layer shadow stack:
  - `0 6px 12px rgba(0, 0, 0, 0.08)`
  - `0 0 10px rgba(255, 255, 255, 0.6)`
  - `inset 0 1px 2px rgba(255, 255, 255, 0.4)`
- Hover: raise by 4px (`translateY(-4px)`) and increase outer shadow.
- `display: block` with centered margin.
- Accompanying `.title` and `.desc` are centered with gentle spacing.

### 3.2 Social Badges
- Container: `.social-row` (flex, centered, wraps with 10px gap).
- Each link: `.social-item` → inline-flex, padding `8px 10px`, white background, 2px border, 16px radius, hard-edge shadow transitions.
- Badge: `.badge` is 28px rounded square with 1.5px border and colored background.
- Ordering handled via CSS (`.email`, `.orcid`, GitHub, `.oshwhub`, Bilibili, WeChat).
- Brand colors (actual implementations):
  - Email: `#d1c0f1`
  - ORCID: `#c9e67b`
  - OSHWHUB: `#9cb9ec`
  - Defaults use global pastel variables (`--blue`, `--green`, `--pink`, `--yellow`, `--orange`, `--purple`).

### 3.3 Language Switch
- `.language-switch` sits at `top: 20px; right: 20px; position: absolute`.
- Links are pills (`padding: 8px 14px`, radius 16px) with the same hard-edge hover/active transitions and background `#f7f1f0`.

### 3.4 Panels & Lists
- `.panel`: margin `16px 0 24px`, padding `6px 18px`, white background, black border, hard-edge shadow.
- Nested panels are flattened (no double borders).
- Legacy plain sections (`h2 + ul`) inherit the same card styling for consistency.
- `.list-container`: zeroed list, items stacked vertically.
- `.list-item`: flex row, 1px border, `border-radius: var(--button-radius)`, background `var(--background-color)`.
- `.panel .list-item`: elevated version with white background, 14px radius, soft shadow.
- `.list-image`: 50–56px wide thumbnails, 1px outline (`rgba(0, 0, 0, 0.25)` inside panels) with small radius.
- `.list-text strong`: slightly larger weight (600–700) without breaking line-height.

### 3.5 Tag Container
- `.tag-container`: flex, wrap, 10px gap, margin `12px 0`.
- Each tag (`span`): padding `6px 14px`, font-size `0.9em`, 1px border, 12px radius, soft box shadow, hover lift (`translateY(-2px)`).

### 3.6 Lightbox
- Checkbox technique:
  - Hidden trigger `input.lightbox__trigger`.
  - Adjacent `.lightbox` overlay appears when checked.
- Overlay uses `backdrop-filter: blur(2px)` with `rgba(0, 0, 0, 0.65)` background.
- Content constrained to `80vw/80vh`, animated zoom-in (`0.18s ease-out`).
- Close button: circular (`var(--lightbox-button-radius)`) with `var(--lightbox-button-size)`, hard-edge shadow from `--lightbox-button-shadow`.
- Thumbnails/labels: hover lift with soft box shadow.

## 4. CSS Variables Reference

- Core: `--background-color`, `--container-bg`, `--border-color`, `--text-color`, `--heading-color`
- Pastel accents: `--blue`, `--green`, `--pink`, `--yellow`, `--orange`, `--purple`, `--lavender`, `--tangerine`, `--rose`
- Geometry: `--border-radius`, `--button-radius`
- Shadows: `--soft-shadow`, `--lightbox-button-shadow`
- Lightbox sizing: `--lightbox-button-size`, `--lightbox-button-radius`

## 5. HTML Skeleton

```html
<div class="container">
  <div class="language-switch">
    <a href="/zh/index.html">中文</a>
  </div>

  <img class="avatar" src="/images/avatar/avatar.webp" alt="avatar" />
  <h1>...</h1>
  <p class="title">...</p>
  <p class="desc">...</p>

  <div class="social-row">
    <a class="social-item email" href="mailto:...">
      <span class="badge"><img src="/images/logo/email.svg" alt="Email" /></span>
      <span>Email</span>
    </a>
    <!-- other social items -->
  </div>

  <div class="panel">
    <h2>Section Title</h2>
    <ul class="list-container">
      <li class="list-item">
        <img class="list-image" src="..." alt="..." />
        <div class="list-text"><strong>Heading</strong><br />Description</div>
      </li>
    </ul>
  </div>

  <div class="panel">
    <h2>Research Interests</h2>
    <div class="tag-container">
      <span>Tag 1</span>
      <span>Tag 2</span>
    </div>
  </div>
</div>
```

## 6. Prompt Snippets

- “Create a frameless beige page with centered white cards (`.panel`) that have 2px black borders and hard-edge shadows (2px 2px 0 #000). Headings are left-aligned with a subtle indent. Add a social badge row of rounded-square buttons with brand colors (email #d1c0f1, orcid #c9e67b, oshwhub #9cb9ec) and the same hover shadow pattern.”
- “Use flex-based tag pills (white background, 1px black border, light shadow, `translateY(-2px)` on hover) and panel lists where thumbnails have a faint rgba outline and 8px radius.”

## 7. Notes

- Keep new patterns aligned with existing modules; add styles to the matching `.css` file under `css/components/`.
- Prefer CSS ordering tricks (e.g., `order`) over HTML rearrangement to support bilingual layouts.
- Avoid gradients, glassmorphism, or heavy blur. This design relies on flat fills and crisp borders.
