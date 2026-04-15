# 青年晚报 · 项目手册

## 项目信息

| 项 | 值 |
|---|---|
| 本地路径 | `/Users/jiangxinji/Documents/青年晚报/` |
| GitHub 仓库 | `3egirlsdream/home` |
| Git 地址 | `git@github.com:3egirlsdream/home.git` |
| 线上地址 | https://3egirlsdream.github.io/home/ |
| 引擎 | Jekyll (kramdown + GFM) |
| 时区 | Asia/Shanghai |

## 目录结构

```
青年晚报/
├── _config.yml          # Jekyll 配置
├── _layouts/
│   ├── default.html     # 基础布局（报头、导航、页脚、全部CSS）
│   └── post.html        # 文章页布局（继承 default）
├── _posts/              # 文章目录（57篇，.markdown 格式）
├── _includes/           # （空）
├── _sass/               # （空）
├── index.html           # 首页（Jekyll 模板，自动渲染文章）
├── posts.html           # 全部文章列表页
├── about.md             # 关于页
├── export_articles.py   # MySQL 导出脚本
└── DEPLOY.md            # 本文件
```

## 发布新文章

### 1. 创建文件

在 `_posts/` 下新建文件，文件名格式：

```
_posts/YYYY-MM-DD-文章简称.markdown
```

示例：`_posts/2026-04-15-春天来了.markdown`

> 文件名日期必须是 `YYYY-MM-DD` 格式，后缀用 `.markdown`。

### 2. 写入内容

```markdown
---
layout: post
title: 文章完整标题
category: 分类名
tags: [标签1, 标签2, 标签3]
date: YYYY-MM-DD
---

正文内容，支持 Markdown 语法。

## 二级标题

普通段落、引用、列表、代码块等。
```

**Front matter 字段说明：**

| 字段 | 必填 | 说明 |
|---|---|---|
| `layout` | 是 | 固定写 `post` |
| `title` | 是 | 文章标题 |
| `category` | 是 | 所属分类（如：生活感悟、读书笔记） |
| `tags` | 否 | 标签列表，格式 `[标签1, 标签2]` |
| `date` | 是 | 发布日期，格式 `YYYY-MM-DD` |

### 3. 提交并推送

```bash
cd /Users/jiangxinji/Documents/青年晚报/
git add _posts/YYYY-MM-DD-文章简称.markdown
git commit -m "发布：文章完整标题"
git push origin main
```

推送后 GitHub Pages 自动构建，约 1-2 分钟后文章上线。

### 4. 验证

访问线上地址确认文章显示正常：
- 首页：https://3egirlsdream.github.io/home/
- 文章页：`https://3egirlsdream.github.io/home/{文件名中日期后的部分}.html`

## 从数据库批量导出

如果需要从 MySQL 重新导出文章：

```bash
cd /Users/jiangxinji/Documents/青年晚报/
python3 export_articles.py
```

> 需要安装 `mysql-connector-python`：`pip3 install mysql-connector-python`

## 常用命令速查

```bash
# 发布新文章（完整流程）
cd /Users/jiangxinji/Documents/青年晚报/
# → 创建 _posts/YYYY-MM-DD-标题.markdown 并写入内容
git add .
git commit -m "发布：文章标题"
git push origin main

# 查看构建状态
gh api repos/3egirlsdream/home/pages/builds/latest

# 查看最近提交
git log --oneline -5

# 文章总数
ls _posts/ | wc -l
```

## 注意事项

- 文件名和 front matter 中的 `date` 保持一致
- 正文第一段会作为摘要显示在首页列表中（以空行分隔）
- 分类和标签首页会自动统计展示，无需手动维护
- 所有 CSS 样式在 `_layouts/default.html` 的 `<style>` 块中
- 文章页额外样式在 `_layouts/post.html` 中
