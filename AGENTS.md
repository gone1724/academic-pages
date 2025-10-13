# AGENTS.md

Guidance for AI coding agents working on the Academic Homepage project.

## Project Overview
- **Type**: Pure static academic personal homepage
- **Tech Stack**: HTML + modular CSS (no build tools)
- **Hosting**: Cloudflare Pages (GitHub connected)
- **Languages**: English (`/index.html`) and Chinese (`/zh/index.html`)
- **Build**: None — static assets only

## Project Structure
```
academic-pages/
├── index.html                  # English homepage
├── zh/
│   └── index.html              # Chinese homepage
├── css/
│   ├── main.css                # Imports every CSS module
│   ├── base/
│   │   └── base.css            # Variables, resets, typography
│   ├── layout/
│   │   ├── layout.css          # Page container, responsive spacing
│   │   └── footer.css          # Footer layout & breakpoints
│   └── components/
│       ├── profile.css         # Avatar, title, intro text
│       ├── tags.css            # Research-interest keyword pills
│       ├── panels.css          # Core card shell for each section
│       ├── list.css            # List layout + panel-specific overrides
│       ├── social.css          # Social/contact badges
│       ├── language-switch.css # Language toggle button
│       └── lightbox.css        # Pure CSS lightbox for QR / awards
├── images/                     # Avatars, awards, logos, QR codes
├── sitemap.xml
├── robots.txt
├── google46a1fac61800863f.html # Google site verification
└── .vscode/settings.json       # Live Server on port 5503
```

## Development Tips

### Local Preview
- Use VS Code Live Server (port 5503) or any static server: `python -m http.server 5503`
- Entry points:
  - English: `http://localhost:5503/index.html`
  - Chinese: `http://localhost:5503/zh/index.html`

### File Navigation
- CSS hierarchy: `base/` → `layout/` → `components/`
- Every HTML change must be reflected in **both** language versions
- Assets live under `images/`; keep thumbnails (`*-lite.webp`) and originals together

### Style Architecture
- **Never** add inline styles or `<style>` blocks inside HTML
- Add new rules to the module that owns the component:
  - Theme tokens & resets → `base/base.css`
  - Page shell & responsive padding → `layout/layout.css`
  - Footer → `layout/footer.css`
  - Hero/profile area → `components/profile.css`
  - Tag clouds → `components/tags.css`
  - Section wrappers → `components/panels.css`
  - Content lists (including panel variants) → `components/list.css`
  - Social badges / contact buttons → `components/social.css`
  - Language switch → `components/language-switch.css`
  - Lightbox interactions → `components/lightbox.css`
- Update `css/main.css` whenever you add or remove component modules.

## Testing Checklist

### Visual
1. Load both language pages.
2. Confirm the language switch works bidirectionally.
3. Check key breakpoints: 320 / 375 / 414 / 768 / 1024 / 1280 / 1920.

### Functional
- Validate all social links, mailto, downloads, and QR lightboxes.
- Ensure images load (full + lite versions).
- Optional: `https://validator.w3.org/` (HTML) and `https://jigsaw.w3.org/css-validator/` (CSS).

### Cross-Browser
- Chrome / Edge
- Firefox
- Safari (desktop & iOS if available)
- Mobile Chrome / Mobile Safari

### SEO & Metadata
- Keep `sitemap.xml` updated (`lastmod`) when content changes.
- Ensure `robots.txt` reflects deploy intent.
- Maintain accurate `<title>` and `<meta name="description">` in both languages.
- Preserve Google verification file.

## Commit & PR Guidelines

### Before Committing
- [ ] Test both EN and ZH pages in the browser
- [ ] Spot-check responsive breakpoints
- [ ] Verify links, downloads, and images
- [ ] Review `git diff` for unintended changes

### Commit Message Convention
```
<type>: <description>

Examples:
feat: 新增科研项目卡片
fix: 修复移动端语言切换遮挡
style: 优化社交徽章的阴影
docs: 更新部署说明
refactor: 调整CSS模块结构
```

### Pull Requests
- **Title**: `<type>: <brief description>`
- Include screenshots for visual updates.
- List touched pages (EN / ZH / both).
- Call out any structural or styling regressions.
- Prefer a clean history (squash if needed).

## Common Tasks

### Adding a New Content Section
1. Add matching HTML to `index.html` and `zh/index.html`.
2. If styles are reusable, create a new file under `css/components/` (or extend an existing module).
3. Import the module inside `css/main.css`.
4. Verify responsive behaviour across breakpoints.
5. Update `sitemap.xml` if a new page/route is created.
6. Document new reusable patterns in `css/style_prompt.md`.

### Modifying Styles
1. Locate the relevant module (see **Style Architecture** above).
2. For shared components reuse existing rules before adding new ones.
3. Use `rg` to search for selectors (e.g., `.panel`, `.social-item`) and prevent duplicates.
4. Check both pages after changes; avoid cascading regressions.
5. Re-test mobile widths (400 / 600 / 1024).

### Adding Images
1. Save in `images/` (group by type).
2. Default to WebP; include lightweight `-lite.webp` for list thumbnails/lightbox triggers.
3. Always set descriptive `alt` text and `loading="lazy"`.
4. Keep file sizes optimized.

### Lightbox Usage
- Uses a checkbox trigger (`.lightbox__trigger`) + label pattern for zero-JS modal.
- Follow existing HTML template in the pages.
- Styling is provided by `css/components/lightbox.css`; avoid inline tweaks.

## Deployment Notes
- Cloudflare Pages auto-deploys from `master`.
- No build command; output directory is repo root.
- Preview deployments available via PRs.
- DNS managed through Cloudflare; TLS mode should remain “Full” or “Full (strict)”.

## Best Practices
- Lean CSS: remove dead rules, keep selectors purpose-driven.
- Accessibility: semantic HTML, meaningful alt text, keyboard-friendly interactions.
- Internationalization: ensure parity between EN and ZH content and layout.
- Maintain consistency with `css/style_prompt.md` when introducing new UI patterns.

## License
GNU General Public License v3.0 (see root LICENSE if present).
