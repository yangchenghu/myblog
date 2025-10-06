# Sam 的博客

一个基于 Hugo + PaperMod 主题构建的个人技术博客，记录技术探索和日常生活。

## 🌟 博客特色

- **简洁美观**：使用 PaperMod 主题，支持明暗主题切换
- **SEO 友好**：完整的 meta 标签、sitemap.xml、结构化数据
- **响应式设计**：完美适配桌面端和移动端
- **快速加载**：Hugo 静态站点生成器，极致的访问速度
- **易于维护**：Markdown 写作，Git 版本控制

## 🚀 技术栈

- **静态站点生成器**：[Hugo](https://gohugo.io/)
- **主题**：[PaperMod](https://github.com/adityatelange/hugo-PaperMod)
- **托管平台**：GitHub Pages
- **自定义域名**：blog.chenghu.me
- **语言**：简体中文

## 📝 内容分类

### 技术探索

- iOS/Android 开发
- React Native
- Kotlin Multiplatform
- DevOps 实践
- 开发工具和技巧

### 日常生活

- 学习笔记
- 生活感悟
- 读书分享

## 🛠️ 本地开发

### 环境要求

- Hugo Extended 版本
- Git

### 安装和运行

```bash
# 克隆项目
git clone https://github.com/yourusername/myblog.git
cd myblog

# 初始化子模块（主题）
git submodule update --init --recursive

# 启动本地开发服务器
hugo server -D

# 访问 http://localhost:1313 查看效果
```

### 🚀 常用启动命令

```bash
# 基础启动（只显示已发布文章）
hugo server

# 启动并显示草稿文章
hugo server -D

# 启动并显示未来日期的文章
hugo server -F

# 启动并显示草稿和未来日期的文章
hugo server -DF

# 指定端口启动（默认1313）
hugo server -D --port 8080

# 绑定到所有网络接口（局域网访问）
hugo server -D --bind 0.0.0.0

# 启动并禁用实时重载
hugo server -D --disableLiveReload

# 启动并指定构建目录
hugo server -D --destination public

# 启动时显示详细日志
hugo server -D --verbose
```

### 📝 创建新文章命令

```bash
# 基础创建命令
hugo new posts/文章标题.md

# 创建带中文标题的文章（推荐）
hugo new posts/技术探索-React-Native性能优化.md

# 创建特定目录下的文章
hugo new posts/技术/iOS开发/UIKit进阶技巧.md

# 使用自定义模板创建文章
hugo new --kind post posts/新文章标题.md

# 创建文章并指定作者
hugo new posts/文章标题.md --editor code

# 批量创建文章（通过脚本）
for title in "文章1" "文章2" "文章3"; do
  hugo new "posts/${title}.md"
done
```

### 📋 文章管理命令

```bash
# 列出所有文章
hugo list all

# 列出草稿文章
hugo list drafts

# 列出未来日期的文章
hugo list future

# 检查文章语法
hugo server -D --navigateToChanged

# 预览特定文章
hugo server -D --navigateToChanged posts/文章标题.md
```

### 🚀 构建和部署命令

```bash
# 基础构建命令
hugo

# 构建并压缩（推荐用于生产环境）
hugo --minify

# 构建并清理缓存
hugo --gc

# 构建时显示详细信息
hugo --verbose

# 构建特定环境的配置
hugo --environment production

# 构建并禁用某些功能（加快构建速度）
hugo --disableKinds=sitemap

# 预览构建结果
hugo server --environment production

# 构建到指定目录
hugo --destination ./dist

# 完整的生产环境构建命令
hugo --minify --gc --environment production
```

### 📦 部署到 GitHub Pages

```bash
# 1. 构建静态文件
hugo --minify

# 2. 进入 public 目录
cd public

# 3. 初始化 git 仓库（如果还没有）
git init

# 4. 添加文件并提交
git add .
git commit -m "Deploy blog $(date)"

# 5. 推送到 GitHub Pages 分支
git push origin gh-pages

# 或者使用 GitHub Actions 自动部署（推荐）
# 将构建的文件推送到 main 分支，GitHub Actions 会自动部署
```

## 📁 项目结构

```
myblog/
├── archetypes/          # 文章模板
├── content/            # 文章内容
│   └── posts/          # 博客文章
├── layouts/            # 自定义布局
├── static/             # 静态资源
├── themes/             # 主题文件
│   └── PaperMod/       # PaperMod 主题
├── hugo.toml          # Hugo 配置文件
├── .gitmodules        # Git 子模块配置
└── README.md          # 项目说明
```

## ⚙️ 配置说明

主要配置在 `hugo.toml` 文件中：

- **baseURL**: 博客的访问地址
- **title**: 博客标题
- **theme**: 使用的主题
- **params**: 主题相关配置
  - `description`: 站点描述
  - `author`: 作者名称
  - `ShowReadingTime`: 显示阅读时间
  - `ShowShareButtons`: 显示分享按钮
  - `defaultTheme`: 默认主题（支持 light/dark）

## 🎨 主题特性

PaperMod 主题提供以下功能：

- ✅ 明暗主题切换
- ✅ 响应式设计
- ✅ 搜索功能
- ✅ 目录导航
- ✅ 面包屑导航
- ✅ 社交分享
- ✅ RSS 订阅
- ✅ 标签和分类
- ✅ 代码高亮

## 📖 写作指南

### 🛠️ 写作工作流

```bash
# 1. 创建新文章
hugo new posts/我的新文章.md

# 2. 启动开发服务器预览
hugo server -D

# 3. 编辑文章内容（使用您喜欢的编辑器）
code content/posts/我的新文章.md

# 4. 实时预览效果（浏览器会自动刷新）
# 访问 http://localhost:1313

# 5. 检查文章状态
hugo list drafts  # 查看草稿
hugo list future  # 查看未来发布文章

# 6. 发布文章（将 draft: true 改为 draft: false）
# 7. 构建最终版本
hugo --minify
```

### Front Matter 模板

```yaml
---
title: "文章标题"
date: 2024-01-01
description: "文章描述"
tags: ["标签1", "标签2"]
categories: ["分类"]
draft: false
cover:
  image: "/cover.jpg" # 可选封面图片
  alt: "封面描述"
---
```

### 图片处理

- 将图片放在 `static/` 目录下
- 在文章中引用：`![图片描述](/images/filename.jpg)`

### 代码块

使用三个反引号包围代码，并指定语言：

````markdown
```bash
# 示例命令
hugo server -D
```
````

```

## 🔧 自定义配置

### 添加自定义 CSS

在 `static/css/` 目录下添加自定义样式文件，并在 `hugo.toml` 中引入。

### 修改主题

如需深度自定义，可以：
1. Fork PaperMod 主题
2. 在 `layouts/` 目录下覆盖主题模板
3. 在 `static/` 目录下添加自定义资源

## 📈 SEO 优化

博客已配置以下 SEO 功能：

- ✅ 自动生成 sitemap.xml
- ✅ Meta 标签优化
- ✅ Open Graph 支持
- ✅ Twitter Cards 支持
- ✅ 结构化数据（JSON-LD）
- ✅ 面包屑导航
- ✅ 规范链接（Canonical URL）

## 🤝 贡献

欢迎提交 Issue 和 Pull Request 来改进这个项目。

## 📄 许可证

本项目采用 MIT 许可证，详见 [LICENSE](LICENSE) 文件。

## 📞 联系方式

- **博客地址**：https://blog.chenghu.me/
- **GitHub**：[@yourusername](https://github.com/yourusername)

---

⭐ 如果这个项目对您有帮助，请给个 Star 支持一下！
```
