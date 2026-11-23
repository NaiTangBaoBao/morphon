# Morphon 项目约定

本文件面向所有 AI 编码工具，自包含。`CLAUDE.md` 通过 `@AGENTS.md` 导入本文件，不重复正文。

## 这是什么仓库

**产品材料与发布仓库。** 放 README、`RELEASES.md`、`demo/`、`assets/`、`docs/install.md`。

源代码在 [`morphon-core`](../morphon-core)，**不要把源码或技术文档放进本仓库**。

## 工作区布局（tower）

| 位置 | 分支 | 职责 |
| --- | --- | --- |
| `/workspaces/projects/morphon` | `main` | 本仓库主仓 |
| `/workspaces/projects/morphon-core` | `main` | 源码主仓（只做集成与推送） |
| `/workspaces/projects/_worktrees/morphon-core/<任务名>` | `task/<任务名>` | 源码功能工作树 |

源码的 worktree 约定、分支与合入流程见 `morphon-core/AGENTS.md`（用 `scripts/dev start|sync|check|integrate`）。本仓库自身改动以文字/素材为主，通常直接在 `main` 提交；需要多步并行时同样在 `/workspaces/projects/_worktrees/morphon/<任务名>` 开 worktree。

## 内容规则

- 对外表述与 `morphon-core` 的实际行为一致，不承诺未实现的能力。
- `RELEASES.md` 按版本追加，不改写已发布的历史条目。
- 素材放 `assets/`、`demo/`，不引用个人机器路径。
- 安装说明改 `docs/install.md`。

## 提交

完成并验证一处改动后及时提交并推送。一个提交做一件事，写清改了什么、为什么。不擅自提交无关的用户改动；受阻时说明原因。不对 `main` 强推。
