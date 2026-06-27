# Step 9：生成所有文件

仅在用户于 Step 8 确认后执行。按以下顺序生成：

## 9.1 CLAUDE.md

根据用户选择构建。仅包含用户选择启用的规则。

模板结构：
```markdown
# CLAUDE.md

## Project: {{NAME}}

{{DESCRIPTION}}

---

## 核心行为准则 (Karpathy's Rules)

（仅包含用户在 Step 2 中选择启用的规则）
（用户若未选任何规则，跳过整个章节）

### 1. Think Before Coding（编码前先思考）
...

### 2. Simplicity First（简单优先）
...

（以此类推 — 仅包含选中的规则）

---

## 项目特定规则

（仅包含用户在 Step 3 中选择启用的规则）

### 工作目录约束
（若选中）

### 用户建议的审查机制
（若选中）

### Context Map 更新
（若选中）

### {{用户自定义规则}}
（若有）

---

## Context Map

- {{DATE}}: 项目初始化。核心行为准则确立。
```

## 9.2 .claude/ 目录结构

根据 Step 7 的选择创建目录并放置 `.gitkeep` 文件。

## 9.3 .claude/settings.json

根据 Step 4-5 的选择生成。平台感知的黑名单规则。

重要：不要硬编码黑名单 — 应根据以下因素推导：
- 项目所在盘符（Windows）或文件系统根路径（Unix）
- 用户在 Step 5.3 中的选择

## 9.4 .claude/settings.local.json

根据 Step 5.4 的选择生成。

## 9.5 MEMORY.md + memory/ 文件

根据 Step 6 的选择生成。若选择本地记忆，创建 `./memory/` 并包含每条启用规则对应的记忆文件。若选择全局记忆，通过 Write 工具写入全局记忆目录。若两者都选，两边都写。

## 9.6 验证

生成所有文件后：

1. 确认 CLAUDE.md 仅包含选中的规则
2. 确认 settings.json 与用户的安全选择一致
3. 确认目录结构与 Step 7 的选择一致
4. 确认无文件写入到项目根目录之外
