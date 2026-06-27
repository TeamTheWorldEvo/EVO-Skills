# Step 7：.claude/ 目录结构

**解释：**

> **`.claude/` 目录结构**
>
> Claude Code 识别 `.claude/` 下的这些子目录：
>
> | 目录 | 用途 | 创建？ |
> |------|------|--------|
> | `agents/` | 自定义 Agent 定义（如 code-reviewer） | 空目录 + .gitkeep |
> | `commands/` | 自定义斜杠命令 | 空目录 + .gitkeep |
> | `skills/` | **仅放 meta-skill**（辅助开发的 skill），不是 skill 产出物 | 空目录 + .gitkeep |
> | `workflows/` | 自定义 Workflow 脚本 | 空目录 + .gitkeep |
> | `settings.json` | 项目级配置（会提交 git） | 前面 Step 4-5 配的内容写在这里 |
> | `settings.local.json` | 本地配置（不提交 git） | 个人偏好权限 |
>
> **关于 skills/ 的重要区分**：如果你这个项目本身是在开发 skill（就像本项目 `prd-expert/` 和 `init-project/`），产出物放在项目根目录作为独立子目录，**不要**放进 `.claude/skills/`。`.claude/skills/` 只放开发过程中辅助你写代码的 meta-skill。
>
> ---
>
> - **A) 全建（推荐）** — 四个空目录 + settings.json + settings.local.json
> - **B) 只要部分** — 告诉我哪些不需要

等待回答。记录选择。
