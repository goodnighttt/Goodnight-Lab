# 良夜突围

这是「良夜突围」的个人博客，使用 Hexo + Butterfly 构建，通过 GitHub Pages 发布。

线上地址：

```text
https://goodnighttt.github.io/Goodnight-Lab/
```

## 本地使用

安装依赖：

```bash
npm install
```

本地预览：

```bash
npm run server
```

生成静态文件：

```bash
npm run build
```

新建文章：

```bash
npx hexo new "文章标题"
```

## 从 Obsidian 迁移笔记

把适合公开的 Markdown 笔记复制到 `source/_posts/`，并在文件顶部补上 Hexo front matter：

```yaml
---
title: 文章标题
date: 2026-06-30 19:20:00
categories:
  - 分类
tags:
  - 标签
description: 文章摘要
---
```

Obsidian 的图片语法建议改成标准 Markdown 图片语法：

```markdown
![图片说明](https://example.com/image.png)
```

## 发布到 GitHub Pages

推送到 `main` 分支后，GitHub Actions 会自动构建并发布：

```bash
git push
```

如果第一次发布，在 GitHub 仓库 `Settings -> Pages` 中把 Source 设置为 `GitHub Actions`。
