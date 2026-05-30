# Chat Saver 🗂️

把跟 AI 的聊天对话保存为结构化的 markdown 文档。

## 为什么需要它

和 AI 的对话里经常有有价值的分析、决策、代码方案，但对话一关就没了。Chat Saver 把对话完整保存下来——顶部有摘要方便快速了解内容，下方是原汁原味的对话记录，方便日后反复查阅和回顾。

## 功能特性

- **完整保存**：原样保留用户和 AI 的对话内容，不做精炼、不做省略
- **自动摘要**：生成主题摘要和关键要点，方便快速判断是否需要展开全文
- **智能触发**：只在用户明确要求保存时才执行，不会干扰日常对话
- **结构化存储**：统一保存到项目 `chats/` 目录下，文件名包含日期和主题
- **多语言支持**：中文对话输出中文文档，英文对话输出英文文档

## 安装

> **兼容 55+ 种 AI 编程工具** — Claude Code、Codex、Cursor、OpenCode、Windsurf 等。

### 方式一：skills CLI（推荐）

安装 [vercel-labs/skills](https://github.com/vercel-labs/skills)，然后一行命令搞定：

```bash
# 项目级（仅当前项目可用）
npx skills add ethanhome/chat-saver

# 全局（所有项目可用）
npx skills add ethanhome/chat-saver -g
```

会自动安装到各工具对应的目录（`.claude/skills/`、`.agents/skills/`、`.windsurf/skills/` 等）。

### 方式二：手动克隆

```bash
git clone https://github.com/ethanhome/chat-saver.git ~/.claude/skills/chat-saver
```

> 其他工具请克隆到对应目录（如 `~/.codex/skills/chat-saver`、`.agents/skills/chat-saver`）。

## 使用方法

安装完成后，在支持的 AI 工具中用自然语言触发：

- 「保存对话」
- 「把聊天存下来」
- 「导出对话」
- 「写个记录」
- 「把对话整理成文档存下来」

**不会触发的情况**：当你只是想口头回顾对话，如「帮我总结一下」「我们聊了什么」——这些会直接在对话中回答，不会创建文件。

## 输出示例

保存后的文件存放在 `<项目根目录>/chats/` 目录下，格式为 `YYYY-MM-DD-主题.md`：

```markdown
# React Hooks 优化

> 2026-05-30

## 摘要

讨论了 React Hooks 在大型项目中的性能优化策略，包括 useMemo 和 useCallback 的使用场景分析，以及如何避免不必要的重渲染。

## 关键要点

- useMemo 应该只用于计算成本高的场景
- useCallback 需要配合 memo 组件才有意义
- 自定义 Hook 可以封装复杂的状态逻辑

---

## 对话

### 用户

帮我看看这段代码有什么性能问题...

### AI

这段代码主要有以下几个问题...
```

## 文件命名规则

| 规则 | 示例 |
|------|------|
| 格式 | `YYYY-MM-DD-主题.md` |
| 主题使用英文或拼音 | `react-hooks`、`api-sheji` |
| 同主题重复时追加序号 | `2026-05-30-react-hooks-2.md` |

## 注意事项

- 对话内容原样保留，不做任何精炼或改写
- 不会保存包含敏感信息（密码、密钥、token）的内容
- 代码片段自动使用对应的语法高亮
- 如果对话涉及多个不相关话题，会按话题分组

## 许可证

MIT