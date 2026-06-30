# 我的 GitHub 博客

这是一个基于 Hexo、Butterfly 和 GitHub Pages 的个人博客模板。

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

## 发布到 GitHub Pages

1. 在 GitHub 新建仓库，个人主页仓库通常命名为 `你的用户名.github.io`。
2. 把 `_config.yml` 里的 `your-github-username` 改成你的 GitHub 用户名。
3. 把 `_config.butterfly.yml` 里的 GitHub 链接也改成你的用户名。
4. 推送到 GitHub 后，在仓库 `Settings -> Pages` 中选择 `GitHub Actions`。

如果你使用个人主页仓库，站点地址通常是：

```text
https://你的用户名.github.io
```

如果你使用普通项目仓库，记得把 `_config.yml` 的 `url` 和 `root` 按 GitHub Pages 项目站点规则调整。

