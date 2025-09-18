<h1 align="center">
Academic Homepage
</h1>

<p align="center">一个纯粹的静态个人学术主页。</p>
<p align="center">A pure and static personal academic homepage.</p>

## Solusion 解决方案

自购域名 + Cloudflare DNS 解析 + Github 仓库管理 + Cloudflare Pages 托管

Self-purchased domain + Cloudflare DNS resolution + GitHub repository management + Cloudflare Pages hosting

* README.md:1 概述站点定位为纯静态学术主页，并明确 Cloudflare+GitHub Pages 的部署方案及 GPLv3 许可信息。
* index.html:1 为英文主页，内嵌语言切换、头像与教育/研究/奖励等板块的完整静态内容。
* zh/index.html:1 提供中文镜像页，结构与英文版一致，通过顶部语言切换互相跳转，并引用相同样式与资源。
* css/main.css:1 汇总导入 base/layout/components 模块化样式文件，**css/** 目录下按照基础变量、布局、组件分别组织子样式。
* robots.txt:1 与 sitemap.xml:1 已配置基础爬虫策略和中英双首页入口，有利于 SEO；根目录还包含 google46a1fac61800863f.html 用于站点验证。
* **image/** 目录分组存放头像、奖项、Logo、二维码等资源，支撑页面展示。

## License 许可证

该项目使用 GNU 通用公共许可证 v3.0 授权 - 有关详细信息，请参阅 [LICENSE](./LICENSE) 文件。

This project is licensed under the GNU General Public License v3.0 - see the [LICENSE](./LICENSE) file for details.
