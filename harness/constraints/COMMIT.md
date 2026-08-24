# 提交约束

## 分支职责

- `blog`：只承载文章、草稿、配图和文章排版调整，不修改工具或站点配置。
- `main`：只保留完整文章或完整功能；一篇文章在 `main` 中对应一个完整提交。
- `feat/*`：从 `main` 切出，用于工具或配置开发；完成后 squash 合入 `main`。

## 提交格式

写作提交建议使用：

- `blog(posts/draft): 添加文章「标题」`
- `blog(posts/draft): 修订「标题」`
- `blog(posts/publish): 发布文章「标题」`
- `blog(posts/publish): 修订文章「标题」`

发布提交正文根据被 squash 的写作提交概括修改历史，每行记录一项实质变化。

## 写作与发布

1. 在 `blog` 上写作并允许多次小提交；每个提交只涉及一篇文章。
2. 草稿阶段保持 `draft: true`，不执行发布动作。
3. `main` 出现完整功能后，定期把 `blog` rebase 到 `main`；不要在 `blog` 上 merge `main`。
4. 发布前，在 `blog` 上把同一篇文章的提交 squash 为一个发布提交，并确认文章完整且 `draft: false`。
5. 将这个发布提交 cherry-pick 到 `main`；不要把 `blog` 的整段草稿历史合入 `main`。

## 功能开发

1. 从 `main` 创建 `feat/*` 分支。
2. 完成功能和验证后，将功能提交 squash 合入 `main`。
3. 再把 `blog` rebase 到更新后的 `main`，使写作分支获得新功能并保持线性历史。
