<h1 align="center">Academic Homepage / 学术主页</h1>

<p align="center">纯静态学术个人主页（EN/中文双语）</p>
<p align="center">A pure static personal academic homepage (EN/ZH bilingual)</p>

## 概览 Overview

- 纯静态站点，无构建流程与包管理器（HTML + CSS）。
- 双语内容：英文（根目录）与中文（`zh/`）。
- 云端托管：Cloudflare Pages（仓库：GitHub）。
- 模块化 CSS 架构：`base → layout → components`。

## 目录结构 Project Structure

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
│   │   ├── components.css  # Component module aggregator
│   │   ├── dashboard.css   # Dashboard section styles
│   │   ├── language-switch.css
│   │   ├── contact.css
│   │   └── list.css
│   └── style_prompt.md     # UI spec for AI agents
├── images/                 # Avatar, awards, logos, QR codes
├── sitemap.xml
├── robots.txt
└── google46a1fac61800863f.html  # Google site verification
```

## 部署 Deployment

- 分支：`master` 自动部署；根目录：`/`；无需构建命令。（推荐Cloudflare Pages）

## 许可证 License

本项目使用 GNU GPL v3.0 开源许可证，详见 `LICENSE`。

This project is licensed under the GNU General Public License v3.0. See `LICENSE` for details.
