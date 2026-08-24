# 强制约束

## 文档维护

- `AGENTS.md` 只维护 Harness 文档地图；源码布局归入 `ARCHITECTURE.md`，作者定位与写作风格归入 `PRODUCT_SENSE.md`，Git 规则归入 `harness/constraints/COMMIT.md`。
- 修改规则时更新对应的唯一权威文档，并同步复核 `AGENTS.md` 中的路径；不要在多个 Harness 文档中复制完整规则。
- 文档中的命令、路径、分支和生成路由必须与当前仓库实现核对。无法验证的内容应明确保留为 gap，不得写成现状。

## 文章结构与 Frontmatter

- 每篇文章必须位于 `src/content/posts/<slug>/index.md`；默认使用 `pnpm new-post "标题"` 创建，不采用单文件模式。
- Frontmatter 字段按以下顺序书写：`title`、`published`、`description`、`image`、`tags`、`category`、`draft`、`lang`。
- 字符串使用双引号；`published` 使用 `YYYY-MM-DD`；`tags` 使用数组；`draft` 使用布尔值。
- 草稿阶段保持 `draft: true`。只有准备公开发布的完整文章才设置 `draft: false`。
- 文章内图片优先放在文章目录并以 `./image.png` 引用；公共资源放在 `public/` 后以根路径引用。
- reference docs 链接必须以实际构建路由为准；路径含空格或大写字符时，先通过构建结果确认规范化后的 slug。

## 发布前检查

- 检查 Frontmatter 的字段、类型、顺序和 `draft` 状态。
- 检查代码块、数学公式和图片链接的渲染结果。
- 运行 `pnpm check` 与 `pnpm build`；需要人工检查布局时再运行 `pnpm dev` 或 `pnpm preview`，并覆盖移动端视图。

## 提交约束

遵循 [`harness/constraints/COMMIT.md`](harness/constraints/COMMIT.md)。
