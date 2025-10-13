<h1 align="center">📚 学术主页 / Academic Homepage</h1>

<p align="center">✨ 纯静态个人学术主页（英文 / 中文）</p>
<p align="center">✨ A pure static personal academic homepage (EN / ZH)</p>

[![Homepage Screenshot](https://cdn.jsdelivr.net/gh/gone1724/academic-sources@master/Screenshot/homepage_rounded.png "web preview")](https://academic-24s.pages.dev/)

## 📋 概览 Overview

- 🚀 纯静态站点，无构建流程与包管理器（HTML + CSS）。
- 🌐 双语内容：英文（`/`）与中文（`/zh/`）。
- ☁️ 云端托管：Cloudflare Pages, Vercel 等。
- 🎨 模块化：CSS 架构  `base → layout → components`。
- 🔒 安全性：不依赖 JavaScript，保证隐私。

## 📂 目录结构 Project Structure

```
academic-pages/
├── index.html                  # English homepage
├── zh/
│   └── index.html              # Chinese homepage
├── css/
│   ├── main.css                # Imports all CSS modules
│   ├── base/
│   │   └── base.css            # Variables, resets, typography
│   ├── layout/
│   │   ├── layout.css          # Page container & responsive spacing
│   │   └── footer.css          # Footer layout & breakpoints
│   ├── components/
│   │   ├── profile.css         # Avatar, title, intro text
│   │   ├── tags.css            # Research-interest tags
│   │   ├── panels.css          # Card wrapper styles
│   │   ├── list.css            # List patterns + panel overrides
│   │   ├── social.css          # Social/contact badges
│   │   ├── language-switch.css # Language toggle button
│   │   └── lightbox.css        # Pure CSS lightbox
│   └── style_prompt.md         # UI spec for AI agents
├── images/                     # Avatar, awards, logos, QR codes
├── sitemap.xml
├── robots.txt
└── google46a1fac61800863f.html # Google site verification
```
## 🚀 部署 Deployment

分支：`master` 自动部署；根目录：`/`；无需构建命令。

[![Deploy to Cloudflare Pages](https://deploy.workers.cloudflare.com/button)](https://dash.cloudflare.com/?to=/:account/pages)

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/gone1724/academic-pages&project-name=academic-pages&repository-name=academic-pages)

## 📄 许可证 License

本项目使用 GNU GPL v3.0 开源许可证，详见 `LICENSE`。

This project is licensed under the GNU General Public License v3.0. See `LICENSE` for details.
