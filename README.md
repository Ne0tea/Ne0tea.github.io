# Kai · 黄毓杰 — 个人学术主页

基于 [Hugo](https://gohugo.io/) + [Stack](https://github.com/CaiJimmy/hugo-theme-stack) theme 的双语学术博客。

- 主页：`Ne0tea.github.io`
- 邮箱：yujiehuang@zju.edu.cn
- ORCID：[0000-0002-7310-6178](https://orcid.org/0000-0002-7310-6178)

## 内容分区

| Section | 中文路径 | 英文路径 | 用途 |
|---------|---------|---------|------|
| 杂谈 / Posts | `/posts/` | `/en/posts/` | 对科学问题的思考、随笔 |
| 科研成果 / Publications | `/publications/` | `/en/publications/` | 论文 / 项目条目 |
| 文献讨论 / Literature | `/literature/` | `/en/literature/` | 对近期文献的精读与点评 |
| 关于 / About | `/about/` | `/en/about/` | 个人简介 |

## 本地开发

### 一次性准备

1. 安装 Hugo extended（≥ v0.166.0）：

   ```bash
   # Linux
   curl -fsSL -o hugo.tar.gz https://github.com/gohugoio/hugo/releases/download/v0.166.0/hugo_extended_0.166.0_linux-amd64.tar.gz
   tar -xzf hugo.tar.gz && mv hugo ~/bin/

   # macOS
   brew install hugo

   # Windows (scoop)
   scoop install hugo-extended
   ```

2. 初始化子模块：

   ```bash
   git submodule update --init --recursive
   ```

### 日常命令

```bash
# 本地预览（含草稿）
hugo server -D

# 构建
hugo --gc --minify

# 新建内容
hugo new posts/2026-01-01-my-thought.md
hugo new publications/2026-my-paper.md
hugo new literature/2026-discuss-x.md
```

预览默认地址：http://localhost:1313

## 部署

`.github/workflows/deploy.yml` 在每次推送到 `master` / `main` 时自动构建并发布到 GitHub Pages。

### 首次启用 Pages

1. 把仓库 push 到 GitHub（`Ne0tea/Ne0tea.github.io`）。
2. 打开仓库 **Settings → Pages**，把 **Source** 设为 `GitHub Actions`。
3. 等待首个 workflow run 完成。

### 自定义域名（可选）

在 `static/CNAME` 写入你的域名，提交即可。

## 评论（Giscus）启用步骤

1. 在 GitHub 上新建一个公开仓库用于存放评论（也可以复用本仓库的 Discussions）。
2. 在该仓库的 **Settings → General → Features** 中勾选 **Discussions**。
3. 打开 [giscus.app](https://giscus.app/zh-CN) 配置：
   - 选仓库：`Ne0tea/Ne0tea.github.io`
   - Discussion 分类：推荐 `Announcements`
   - 复制 **仓库 ID**、**分类 ID** 等参数。
4. 把这些参数填入 `hugo.toml` 的 `[params.comments.giscus]` 表：

   ```toml
   [params.comments.giscus]
     repo = "Ne0tea/Ne0tea.github.io"
     repoID = "R_xxx"
     category = "Announcements"
     categoryID = "DIC_xxx"
     # 其余按需修改
   ```

5. 推送一次以触发部署，评论区会自动出现在每篇文章底部。

## 个性化

- **个人信息**：编辑 `hugo.toml` 中的 `params.author`、`params.social`、`params.description`。
- **侧边栏头像 / 简介**：编辑 `content/about.md` 和 `content/en/about.md`，并在 `static/images/` 放头像。
- **导航菜单**：修改 `hugo.toml` 的 `[[languages.zh-cn.menu.main]]` 与 `[[languages.en.menu.main]]` 块。
- **首页置顶**：在文章 frontmatter 设 `weight: 1`。

## 目录结构

```
.
├── archetypes/           # 文章模板
├── content/
│   ├── about.md          # 中文 About
│   ├── posts/            # 中文杂谈
│   ├── publications/     # 中文科研成果
│   ├── literature/       # 中文文献讨论
│   └── en/               # 英文版（结构同上）
├── static/
│   ├── images/           # 图片 / 头像
│   ├── pdf/              # 论文 PDF
│   └── CNAME             # 自定义域名（可选）
├── themes/
│   └── hugo-theme-stack/ # 主题（git submodule）
├── .github/workflows/    # GitHub Actions
└── hugo.toml             # 站点主配置
```

## License

- 博客内容（`content/`）：CC BY 4.0（除非另有声明）。
- 主题：GNU GPL v3.0（详见 [themes/hugo-theme-stack/LICENSE](themes/hugo-theme-stack/LICENSE)）。