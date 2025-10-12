# AGENTS.md

This file provides guidance for AI coding agents working on the Academic Homepage project.

## Project Overview
- **Type**: Pure static academic personal homepage
- **Tech Stack**: HTML, CSS (modular architecture)
- **Hosting**: Cloudflare Pages + GitHub
- **Languages**: English (root) and Chinese (zh/)
- **Structure**: Static files with no build process or package manager

## Project Structure
```
academic-pages/
├── index.html              # English homepage
├── zh/
│   └── index.html          # Chinese homepage
├── css/
│   ├── main.css            # Entry point importing all modules
│   ├── base/
│   │   └── base.css        # Variables, resets, typography
│   ├── layout/
│   │   ├── layout.css      # Grid, container, spacing
│   │   └── footer.css      # Footer-specific styles
│   ├── components/
│   │   ├── components.css  # Component module aggregator (includes tag container, responsive avatar)
│   │   ├── dashboard.css   # Main dashboard styles (avatar, panels, social badges, lists)
│   │   ├── language-switch.css
│   │   ├── contact.css
│   │   ├── list.css
│   │   └── lightbox.css    # Pure CSS lightbox for image zoom
│   └── style_prompt.md     # UI spec for AI agents
├── images/                 # Avatar, awards, logos, QR codes
├── .vscode/
│   └── settings.json       # Live Server on port 5503
├── sitemap.xml
├── robots.txt
└── google46a1fac61800863f.html  # Google site verification
```

## Development Environment Tips

### Local Development
- Open with VS Code Live Server (configured on port 5503)
- Or use any static file server: `python -m http.server 5503`
- Main entry points:
  - English: `index.html`
  - Chinese: `zh/index.html`

### File Navigation
- CSS modules follow a clear hierarchy: base → layout → components
- Always check both `index.html` and `zh/index.html` when modifying content
- Images are organized by type in the `images/` directory

### Style Architecture
- **DO NOT** add inline styles or `<style>` tags in HTML files
- Import new CSS modules through the appropriate parent:
  - Base styles → `css/base/base.css`
  - Layout styles → `css/layout/layout.css`
  - Component styles → `css/components/components.css`
- Main CSS entry is `css/main.css` (imported by both HTML files)
- **CSS Cascade Priority**:
  - `dashboard.css` loads AFTER `components.css` and contains the primary styles for: avatar, panels, social badges, action buttons, pills
  - `components.css` contains: responsive overrides for avatar, tag containers, summary cards
  - **IMPORTANT**: When modifying shared components (avatar, panel, btn, pill), edit `dashboard.css` first; only add responsive or specialized overrides to `components.css`

## Testing Instructions

### Visual Testing
1. Open both language versions in browser:
   - `http://localhost:5503/index.html`
   - `http://localhost:5503/zh/index.html`
2. Test language switch links work bidirectionally
3. Verify responsive design at breakpoints:
   - Mobile: 320px, 375px, 414px
   - Tablet: 768px, 1024px
   - Desktop: 1280px, 1920px

### Content Validation
- Check all links (social media, email, external resources)
- Verify all images load correctly
- Test print styles (if applicable)
- Validate HTML: `https://validator.w3.org/`
- Validate CSS: `https://jigsaw.w3.org/css-validator/`

### Cross-Browser Testing
- Chrome/Edge (Chromium)
- Firefox
- Safari (if available)
- Mobile browsers (Chrome Mobile, Safari iOS)

### SEO & Metadata
- Verify `sitemap.xml` includes all pages with correct lastmod dates
- Check `robots.txt` allows/disallows correct paths
- Validate meta descriptions and title tags in both languages
- Ensure Open Graph tags are present (if added)

## Commit & PR Instructions

### Before Committing
- [ ] Test both English and Chinese pages in browser
- [ ] Validate HTML and CSS through W3C validators
- [ ] Check responsive design on at least 3 breakpoints
- [ ] Verify all images load and links work
- [ ] Review git diff to avoid committing unintended changes

### Commit Message Format
```
<type>: <description>

Examples:
feat: 添加新的研究项目展示区域
fix: 修复移动端语言切换按钮对齐问题
style: 优化卡片组件的阴影效果
docs: 更新README中的部署说明
refactor: 重构CSS模块化结构
```

### PR Guidelines
- **Title format**: `<type>: <brief description>`
- Include screenshots for visual changes
- List affected pages (EN/ZH/both)
- Note any breaking changes to styles or structure
- Ensure clean commit history (squash if needed)

## Common Tasks

### Adding New Content Section
1. Add HTML structure to both `index.html` and `zh/index.html`
2. Create new component CSS file in `css/components/` OR add styles to `components.css`
3. Import in `css/components/components.css` (if new file created)
4. Test responsive behavior
5. Update sitemap if new page route
6. Document in `css/style_prompt.md` if creating reusable UI pattern

### Modifying Styles
1. Identify correct CSS module (base/layout/components)
2. For shared components (avatar, panel, btn, pill, social-item):
   - Primary styles → `css/components/dashboard.css`
   - Responsive/mobile overrides → `css/components/components.css`
3. **CRITICAL**: Check for duplicate definitions across files before adding new styles
   - Use grep/search to find existing definitions: `.avatar`, `.panel`, `.btn`, etc.
   - Remove or consolidate duplicates to avoid cascade conflicts
4. Make changes in the appropriate module only
5. Test cascade effects on both language pages
6. Check mobile responsiveness at breakpoints: 400px, 600px, 1024px

### Adding Images
1. Place in appropriate `images/` subdirectory
2. Use WebP format when possible for performance
3. Provide both lite (thumbnail) and full-size versions for images with lightbox
4. Include alt text in HTML for accessibility
5. Add `loading="lazy"` attribute for performance optimization
6. Optimize file size before committing
7. Update both language versions if content image

### Lightbox Image Gallery
The project uses pure CSS checkbox technique for image zoom functionality:
- **Thumbnails**: Use `-lite.webp` suffix, add `loading="lazy"`
- **Lightbox HTML structure**:
  ```html
  <!-- Trigger (thumbnail or social link) -->
  <label for="lightbox-id" aria-label="View image">
    <img src="thumb-lite.webp" alt="Description" class="list-image" loading="lazy" />
  </label>

  <!-- Lightbox modal -->
  <input type="checkbox" id="lightbox-id" class="lightbox__trigger" />
  <div class="lightbox" aria-modal="true" role="dialog">
    <div class="lightbox__content">
      <img class="lightbox__img" src="full-image.webp" alt="Description" loading="lazy" />
      <label class="lightbox__close" for="lightbox-id" aria-label="Close">×</label>
    </div>
  </div>
  ```
- **Features**: Click thumbnail/label to open, click close button or background to dismiss
- **Advantages**: No browser history pollution (unlike `:target`), better UX on mobile
- **Performance**: All lightbox images use lazy loading
- **Accessibility**: Includes ARIA attributes (aria-modal, aria-label, role)
- **Styling**: Defined in `css/components/lightbox.css`

### Updating Metadata
- Sitemap: Update `lastmod` date when content changes
- HTML meta: Keep descriptions under 160 characters
- Title tags: Keep unique and descriptive per page
- Verify Google verification file remains in root

## Deployment Notes

### Cloudflare Pages
- Auto-deploys from `master` branch
- No build command needed (static files)
- Root directory: `/`
- Preview deployments on PRs

### DNS & Domain
- Managed through Cloudflare DNS
- Ensure CNAME/A records point correctly
- SSL/TLS should be "Full" or "Full (strict)"

## Best Practices

### Performance
- Minimize CSS file size (avoid unused rules)
- Optimize images before adding
- Leverage browser caching via Cloudflare
- Use preload for critical fonts/resources

### Accessibility
- Maintain semantic HTML structure
- Include alt text for all images
- Ensure sufficient color contrast
- Test keyboard navigation

### Maintainability
- Keep CSS modular and organized
- Use consistent naming conventions
- Comment complex style rules
- Avoid magic numbers (use CSS variables)

### Internationalization
- Always update both EN and ZH versions
- Keep content structure parallel
- Use language-appropriate fonts
- Test character encoding (UTF-8)

## License
This project is licensed under GNU General Public License v3.0.
