---
title: 用 Obsidian + Enveloppe + Jekyll + GitHub Pages 搭建个人博客
date: 2026-09-15
filename: 2026-09-15-obsidian-to-github-pages
category: 教程
tags:
  - Obsidian
  - GitHubPages
  - 教程
share: true
---
这套方案的目标是：使用 Obsidian 作为日常写作工具，将其中指定的文章发布为一个基于 Jekyll 的个人博客，并通过 GitHub Pages 托管。

整个系统由四部分组成：

- **Obsidian**：写作和管理文章。
- **Enveloppe**：将指定的 Obsidian 文章发布到 Jekyll 项目。
- **Jekyll**：将 Markdown 文章生成静态网页。
- **GitHub Pages**：托管最终的网站。

## 一、创建 GitHub Pages 仓库

在 GitHub 创建一个 Repository，名称使用：

```text
用户名.github.io
```

这个仓库同时作为 Jekyll 网站的源码仓库和 GitHub Pages 的发布仓库。

最终网站地址为：

```text
https://用户名.github.io
```

## 二、建立 Jekyll 项目

在本地建立 Jekyll 项目，并将它与 GitHub Pages 仓库关联。

Jekyll 项目的基本结构包括：

```text
_posts/
_layouts/
assets/
_config.yml
index.md
```

其中 `_posts` 用于保存博客文章。

Jekyll 的文章文件采用：

```text
YYYY-MM-DD-title.md
```

的形式。

例如：

```text
2026-09-15-obsidian-to-github-pages.md
```

## 三、选择并配置主题

使用默认主题或任何Jekyll支持的主题（本网站使用 Cayman）作为网站的基础主题。

通过 `_layouts/default.html` 和 `_layouts/post.html` 调整页面结构，通过：

```text
assets/css/style.scss
```

覆盖主题样式。

主题本身只是网站的显示层，文章内容仍然以 Markdown 文件保存。

## 四、在 Obsidian 中安装 Enveloppe

在 Obsidian 中安装 **Enveloppe** 插件。

Enveloppe 的作用是：

> 将 Obsidian 中指定的文章转换并发布到 Jekyll 项目的 `_posts` 目录。

文章是否发布，由 Front Matter 中的：

```yaml
share: true
```

控制。

例如：

```yaml
title: "文章标题"
date: 2026-09-15
filename: "2026-09-15-example"
category: "历史"
tags:
  - 中国
  - 历史
share: true
```

## 五、使用 Templater 自动生成文章模板

在 Obsidian 中安装 **Templater**，建立统一的文章模板。

模板自动生成：

- `title`
- `date`
- `filename`
- `category`
- `tags`
- `share`

创建新文章时填写标题、英文 slug、分类和标签即可。

这样可以保证所有公开文章拥有统一的 Front Matter 格式。

## 六、统一使用英文 slug 作为文件名

文章的标题和文件名分开管理。

例如：

```yaml
title: "用 Obsidian + Enveloppe + Jekyll + GitHub Pages 搭建个人博客"
filename: "2026-09-15-obsidian-to-github-pages"
```

文章标题可以正常使用中文和中文标点，而文件名 ***必须使用简单的英文 slug。*** 否则Obsidian内引用的链接不会正常转换。

已经发布的文章尽量不要修改 slug，因为 slug 会影响文章 URL。

## 七、使用 Obsidian 内部链接

正文中继续使用 Obsidian 原生 WikiLink：

```markdown
[[另一篇文章]]
```

不需要手动填写网站 URL，也不需要加入 category。

Enveloppe 会将内部链接转换成 Markdown 相对链接，Jekyll 再将这些链接转换为最终网页链接。

因此不同分类的文章也可以互相链接。

需要注意：

**被引用的文章必须已经存在于公开的 Jekyll 仓库中。**

不存在的 WikiLink 不会被转换成有效的网站链接。

## 八、使用外部图片

博客图片使用标准 Markdown 外链：

```markdown
![图片说明](https://example.com/image.jpg)
```

图片本身不进入 Jekyll 仓库，由外部图片托管服务或公开图片来源提供。

这种方式可以避免让博客仓库承担大量图片文件。

使用公共图片时还需要注意版权和图片来源的稳定性。

## 九、文章分类和标签

使用 Front Matter 管理分类和标签：

```yaml
category: "历史"
tags:
  - 中国
  - 政治
  - 1949
```

分类用于组织文章的大类，标签用于描述具体主题。

## 十、发布文章

完成文章后，将：

```yaml
share: true
```

然后使用 Enveloppe 发布。

完整流程：

```text
Obsidian 中写文章
        ↓
Enveloppe
        ↓
Jekyll 项目的 _posts
        ↓
提交并推送 GitHub
        ↓
GitHub Pages 自动构建
        ↓
网站更新
```

## 十一、修改已经发布的文章

已经发布的文章可以继续在 Obsidian 中修改。

保持：

```yaml
share: true
```

再次使用 Enveloppe 发布即可更新网站。

标题、正文、分类和标签都可以修改。

如果希望保持 URL 稳定，应尽量保持原来的 slug 不变。

## 十二、取消文章发布

需要注意：

```yaml
share: false
```

不会删除已经发布到 GitHub Pages 的文章。

它只表示 Enveloppe 不再发布或更新这篇文章。

如果需要真正撤下文章，需要手动删除 Jekyll 仓库中的对应 `_posts` 文件，然后重新提交。

## 十三、最终的日常工作流

以后写博客时，只需要：

```text
1. 在 Obsidian 新建文章
2. 使用 Templater 创建 Front Matter
3. 设置中文标题
4. 设置英文 slug
5. 设置 category 和 tags
6. 正常使用 WikiLink
7. 图片使用外部 URL
8. 完成文章
9. 设置 share: true
10. 使用 Enveloppe 发布
11. 推送 GitHub
12. 等待 GitHub Pages 构建完成
```

这样，Obsidian 负责写作，Enveloppe 负责发布，Jekyll 负责生成网站，GitHub Pages 负责托管网站。

后续可以继续在这个基础上完善网站的首页、分类、标签、文章目录、搜索、字体、排版和移动端样式。