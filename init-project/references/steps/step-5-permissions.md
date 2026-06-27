# Step 5：安全配置 — 权限控制

## 5.1 权限模型解释

**解释（先教）：**

> **配置：权限控制（Permissions）**
>
> Claude Code 的权限模型是 **allow/deny 名单制**：
>
> - **allow 名单**：列出"允许执行"的工具+路径组合。不在名单里的 → 每次执行前弹确认框。
> - **deny 名单**：列出"禁止执行"的工具+路径组合。在名单里的 → 直接拒绝。
> - **优先级**：deny 优先于 allow。两个名单都匹配时，deny 胜出。
>
> 权限条目格式：`工具名(路径模式)`，比如 `Read(C:/**)` = 禁止读取 C 盘所有文件。
>
> 我们要配两块：**Bash 命令白名单**（哪些命令可以直接跑、不用确认）和**文件访问黑名单**（哪些路径绝对不准碰）。

## 5.2 Bash 命令白名单

**解释：**

> **Bash 命令白名单**
>
> 默认预置了常用开发命令：`git`、`npm`、`python`、`docker`、`curl`、`ssh` 等（完整清单见下方）。
>
> 不在白名单里的命令每次执行前会弹确认框——这是安全机制，不是 bug。比如 `rm -rf /` 这种危险命令，不在名单里就会拦住问你。
>
> ```
> 预置白名单：
> git, ls, cd, cat, head, tail, wc, find, grep, sort, uniq,
> mkdir, touch, cp, mv, echo, date, python, python3, pip,
> npm, npx, node, curl, wget, ssh, gh, docker, chmod, chown,
> rm, code, cursor
> ```
>
> ---
>
> - **A) 用预置清单（推荐）** — 覆盖 90% 场景
> - **B) 在预置基础上增减** — 告诉我加/减哪些命令
> - **C) 空白名单** — 每个 Bash 命令都手动确认（最安全但最烦）

等待回答。记录选择。

## 5.3 文件访问黑名单

**解释：**

> **文件访问黑名单**
>
> 阻止 AI 读写其他盘符/系统目录。这是**平台相关的**。
>
> **Windows（你当前的环境）**：
> 当前项目在 `E:` 盘。建议 deny 所有其他常见盘符（`C:`、`D:`、`F:`、`G:`、`H:`）以及 Unix 风格系统路径（防御纵深）。**E 盘不 deny**——deny 了就没法干活了。
>
> **Unix（Linux/macOS）**：
> Deny 系统目录：`/etc`、`/home`、`/usr`、`/var`、`/root`、`/tmp`、`/opt`、`/boot`、`/dev`、`/proc`、`/sys`。
>
> ⚠️ **限制**：deny 名单无法穷举所有可能路径（比如用户插个 U 盘变成 `Z:`）。这是一种"合理的最大约束"，配合 sandbox 和 additionalDirectories 构成三层防护。
>
> ---
>
> - **A) 用推荐 deny 规则（推荐）** — 平台感知，自动排除项目盘符
> - **B) 自定义** — 你有额外的路径要封堵或放行
> - **C) 不配 deny** — 靠 sandbox + additionalDirectories 就够了
> - **D) 更严格的 deny** — 连 E 盘的非项目路径也封堵

等待回答。记录选择。

## 5.4 MCP 与额外权限

**解释：**

> **MCP 服务器与额外权限**
>
> - **`enableAllProjectMcpServers: true`** → 自动启用项目中配置的所有 MCP 服务器。
> - **`enabledMcpjsonServers`** → 指定启用的特定 MCP 服务器。
> - **settings.local.json** → 本地专属配置，不会提交到 git。适合放 Workflow、WebSearch 等个人偏好的权限。
>
> 默认会在 `settings.local.json` 中预置 `Workflow(deep-research)` 和 `WebSearch` 两项权限。
>
> ---
>
> - **A) 用默认（推荐）** — 项目 MCP 全开 + local 有 deep-research 和 WebSearch
> - **B) 调整** — 增减 MCP 或额外权限

等待回答。记录选择。

## 5.5 Git 提交归属（attribution）

**解释：**

> **配置：Git 提交归属标记（attribution）**
>
> **它做什么**：当 Claude Code 生成 commit message 或 PR 描述时，自动添加归属标记，用于区分 AI 生成和人工编写的提交。
>
> **默认值**：不设置（无归属标记）。
>
> **`attribution.commit`** → 自动在 AI 生成的 commit message 末尾追加标记，如 `🤖 Generated with Claude Code`。
> **`attribution.pr`** → 自动在 AI 生成的 PR 描述中追加标记。
> **`attribution.sessionUrl`** → 在提交中附上对话 session 链接，方便回溯上下文。
>
> **为什么需要它**：团队协作时，代码 reviewer 看到 AI 生成的 commit 可以调整审查策略——AI 代码可能需要更仔细地验证逻辑，人工代码可能更关注命名和风格。
>
> ---
>
> - **A) 不加（默认）** — 不区分 AI 和人工提交
> - **B) 加 commit 标记（推荐团队项目）** — `🤖 Generated with Claude Code`
> - **C) 加 commit + session 链接** — 方便回溯对话上下文

等待回答。记录选择。
