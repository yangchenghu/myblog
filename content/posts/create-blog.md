---
title: "从零开始：用 Hugo + GitHub Pages + 自定义域名搭建技术博客（SEO 友好版）"
date: 2025-10-03
description: "手把手教你如何使用 Hugo + PaperMod + GitHub Pages + 自定义域名，打造一个样式美观、Google 搜索引擎友好的技术博客。"
tags: ["Hugo", "GitHub Pages", "SEO", "技术博客"]
categories: ["Blog"]
cover:
  image: "/cover.jpg"
  alt: "Hugo + GitHub Pages 博客封面"
---

# 为什么选择 Hugo + GitHub Pages

作为开发者，写技术博客时我们通常希望：

- **Markdown 写作**（简洁高效）
- **GitHub 仓库存储与托管**
- **自定义域名**（例如 `blog.example.com`）
- **对 Google SEO 友好**
- **样式美观，可定制**

基于这些目标，我推荐 **Hugo + PaperMod 主题 + GitHub Pages** 的组合方案。

---

# 搭建步骤

## 1. 安装 Hugo 并初始化站点

```bash
# 安装 Hugo（macOS）
brew install hugo

# 创建站点
hugo new site myblog && cd myblog

# 添加主题（PaperMod）
git init
git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod

# 启用主题
echo 'theme = "PaperMod"' >> hugo.toml
```

## 2. 创建文章

```bash
hugo new posts/hello-world.md
```

将 `draft: true` 改为 `false`，用 Markdown 写正文即可。

---

# SEO 友好配置

在 `hugo.toml` 中添加以下配置：

```toml
baseURL = "https://blog.example.com/"
title = "我的技术博客"
languageCode = "zh-cn"
hasCJKLanguage = true
enableRobotsTXT = true

[params]
  description = "iOS / Android / RN / KMP / DevOps 实战记录"
  author = "你的名字"
  ShowReadingTime = true
  ShowBreadCrumbs = true
  ShowToc = true
  defaultTheme = "auto"

[sitemap]
  changefreq = "weekly"
  priority = 0.5
  filename = "sitemap.xml"

[outputs]
  home = ["HTML", "RSS", "JSON"]
```

这样会自动生成：

- `robots.txt`
- `sitemap.xml`
- 文章的 canonical 链接、meta 描述

---

# JSON-LD 结构化数据

新建 `layouts/partials/head.html`，添加：

```html
{{ if .IsPage -}}
<script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "BlogPosting",
    "headline": {{ .Title | jsonify }},
    "datePublished": "{{ .Date.Format "2006-01-02T15:04:05Z07:00" }}",
    "dateModified": "{{ .Lastmod.Format "2006-01-02T15:04:05Z07:00" }}",
    "author": {
      "@type": "Person",
      "name": {{ .Param "author" | default site.Params.author | jsonify }}
    },
    "mainEntityOfPage": {
      "@type": "WebPage",
      "@id": {{ .Permalink | jsonify }}
    },
    "image": {{ with .Params.cover.image }}{{ $.Site.BaseURL | printf "%s%s" . | jsonify }}{{ else }}"{{ .Site.BaseURL }}cover.jpg"{{ end }},
    "publisher": {
      "@type": "Organization",
      "name": {{ site.Title | jsonify }}
    },
    "description": {{ .Description | default .Summary | plainify | jsonify }}
  }
</script>
{{- end }}
```

---

# 部署到 GitHub Pages 并绑定自定义域名

## GitHub Actions 部署配置

在 `.github/workflows/deploy.yml` 添加：

```yaml
name: Deploy Hugo site to Pages

on:
  push:
    branches: ["main"]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          submodules: true
          fetch-depth: 0
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: "0.135.0"
          extended: true
      - name: Build
        run: hugo --minify
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

## 自定义域名

1. 仓库 `static/` 下新建 `CNAME` 文件，写入：
   ```
   blog.example.com
   ```
2. 在域名解析商添加记录：
   - 子域名：
     ```
     CNAME blog → yourname.github.io
     ```
   - 根域名：
     ```
     A 185.199.108.153
     A 185.199.109.153
     A 185.199.110.153
     A 185.199.111.153
     ```
3. GitHub Pages → Settings → Pages → 自定义域名，填入 `blog.example.com`，开启 HTTPS。

---

# Google SEO 优化清单

1. 在 **Google Search Console** 验证站点，提交 `sitemap.xml`。
2. 每篇文章添加 **meta description** 和封面图，优化 OG/Twitter 分享。
3. 确保 `baseURL` 与访问域一致，避免重复收录。
4. 打开 PaperMod 的 `ShowBreadCrumbs` 和 `ShowToc`，利于结构化抓取。

---

# 效果展示

搭建完成后，你将得到：

- 自定义域名 `https://blog.example.com`
- 支持 Markdown 写作的技术博客
- 样式美观（PaperMod 支持暗黑模式切换）
- 完全 SEO 友好，Google 能快速收录

---

# 总结

如果你想快速上线技术博客，推荐的组合是：

- **框架**：Hugo
- **主题**：PaperMod
- **托管**：GitHub Pages
- **域名**：自定义域名（支持 HTTPS）
- **SEO**：sitemap、robots、JSON-LD、OG、RSS

这样不仅写作体验好，还能让 Google 搜索结果更漂亮、更靠前。
