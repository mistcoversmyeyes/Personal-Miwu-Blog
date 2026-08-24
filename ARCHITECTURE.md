# 架构地图

## 系统概览

MiWu Blog 是 Astro 5 静态站点。文章和 reference docs 由 Astro Content Collections 读取；Astro 页面、布局及组件在构建时生成站点。仓库的 `pnpm build` 会继续为 `dist/` 建立 Pagefind 搜索索引；生产部署 workflow 当前只执行 Astro build，并在 `blog` 分支更新时把结果发布到 GitHub Pages。

站点界面以 Astro 组件为主，局部交互使用 Svelte，样式由 Tailwind CSS 与仓库内样式文件共同提供。代码源自 Fuwari 主题并在本仓库中继续定制。

## 源码布局

```text
astro.config.mjs             ← Astro 集成、Markdown 管线与构建配置
src/
├── config.ts                ← 站点、导航、作者资料与代码高亮配置
├── content/
│   ├── config.ts            ← Content Collections 及 Frontmatter schema
│   ├── posts/               ← 博客文章；每篇文章使用目录内的 index.md
│   └── spec/                ← About 页面使用的内容文档
├── pages/                   ← Astro 文件路由与静态路径生成入口
├── layouts/                 ← 页面级布局和全局 HTML 外壳
├── components/              ← Astro/Svelte 展示组件与交互组件
├── plugins/                 ← 本地 Remark、Rehype 与 Expressive Code 插件
├── utils/                   ← 内容查询、日期、设置及 URL 工具
├── constants/               ← 页面尺寸、主题值与图标等常量
├── i18n/                    ← 翻译键和语言资源
├── styles/                  ← 全局、Markdown、过渡与组件样式
└── types/                   ← 站点配置等共享类型
scripts/new-post.js          ← 文章目录及 Frontmatter 脚手架
public/                      ← CNAME、favicon 等原样复制的静态资源
.github/workflows/           ← 检查、构建与 GitHub Pages 部署
```

## 模块层级与依赖方向

- `astro.config.mjs` 组装 Astro/Svelte/Tailwind 集成及 Markdown 处理管线，并消费 `src/config.ts` 和 `src/plugins/` 中的本地配置或插件。
- `src/pages/` 是路由入口，向下组合 `src/layouts/`、`src/components/`，并通过 `src/utils/content-utils.ts` 读取 Content Collections。
- `src/layouts/` 与 `src/components/` 可依赖 `config`、`constants`、`i18n`、`types`、`utils` 和 `styles`；内容文件不反向依赖页面或组件。
- `src/content/config.ts` 定义内容边界。生产模式下，内容查询会过滤 `draft: true` 的文章；文章列表按 `published` 降序排列。
- `scripts/new-post.js` 是独立的写作辅助入口，只向 `src/content/posts/` 写入文章骨架，不参与站点运行时。

## 架构约束

- 博客文章采用目录模式：`src/content/posts/<slug>/index.md`；目录名形成文章 slug。嵌套目录由脚本支持。
- 内容字段类型以 `src/content/config.ts` 为实现来源；新文章的字段顺序和默认值以 `scripts/new-post.js` 为实现来源。
- `draft: true` 的文章只在开发环境中可见，生产内容查询必须排除草稿。
- reference docs 的公开 URL 以 Astro 实际生成的 slug 为准；包含空格或大写字符的路径不得直接假定为最终 URL。

## 外部依赖及其范围

- Node.js 与 pnpm：安装依赖并执行本地开发、检查和构建；锁定的包管理器版本见 `package.json`。
- Astro、Svelte、Tailwind CSS 及 Markdown/代码高亮生态：构建站点和渲染内容，具体版本见 `package.json` 与 `pnpm-lock.yaml`。
- PlantUML 公共服务：`src/plugins/remark-plantuml.ts` 默认生成指向 `https://www.plantuml.com/plantuml` 的图片 URL；只有文章包含 `puml` 或 `plantuml` 代码块时使用。
- GitHub Actions 与 GitHub Pages：执行 CI，并把 `blog` 分支通过 `pnpm astro build` 生成的 `dist/` 部署为站点；当前部署 workflow 不执行 Pagefind 步骤。

## 配置与启动

- `src/config.ts` 配置站点标题、语言、主题、导航、作者资料和许可；`astro.config.mjs` 配置站点 URL、集成、Markdown 插件与 Vite 构建行为。
- `pnpm dev` 启动 Astro 开发服务器；`pnpm check` 执行 Astro 检查；`pnpm build` 先生成 `dist/`，再建立 Pagefind 索引；`pnpm preview` 预览构建结果。
- `.github/workflows/build.yml` 在 `main` 的 push 和 pull request 上执行 Astro check/build；`.github/workflows/deploy.yml` 在 `blog` 更新或手动触发时部署 GitHub Pages。
