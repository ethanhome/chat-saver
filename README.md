# Chat Saver

Save AI chat conversations as structured markdown documents.

## Why

Conversations with AI often contain valuable analysis, decisions, and code solutions — but they disappear when the session ends. Chat Saver preserves the full conversation: a summary at the top for quick scanning, followed by the verbatim dialogue for detailed review.

## Features

- **Full preservation**: keeps the user's words and AI's responses verbatim — no condensing, no omitting
- **Auto summary**: generates a topic summary and key points for quick scanning
- **Smart trigger**: only executes when the user explicitly asks to save — no interference with normal conversation
- **Structured storage**: saves to a project `chats/` directory with date and topic in the filename
- **Multi-language**: outputs documents in the same language as the conversation

## Installation

> **Works with 55+ AI coding agents** — Claude Code, Codex, Cursor, OpenCode, Windsurf, and more.

### Option 1: via skills CLI (recommended)

Install [vercel-labs/skills](https://github.com/vercel-labs/skills) once, then:

```bash
# Project-level (available in this project only)
npx skills add ethanhome/chat-saver

# Global (available across all projects)
npx skills add ethanhome/chat-saver -g
```

This automatically installs to the correct directory for each agent (`.claude/skills/`, `.agents/skills/`, `.windsurf/skills/`, etc.).

### Option 2: manual clone

```bash
git clone https://github.com/ethanhome/chat-saver.git ~/.claude/skills/chat-saver
```

> For other agents, clone to their respective skills directory (e.g., `~/.codex/skills/chat-saver`, `.agents/skills/chat-saver`).

## Usage

After installation, trigger with natural language in any supported agent:

- "save this conversation"
- "export chat"
- "write a record"
- "archive this discussion"

**Will NOT trigger** when you just want a verbal recap (e.g., "summarize this", "what did we discuss") — those are answered inline.

## Output example

Files are saved to `<project-root>/chats/YYYY-MM-DD-topic.md`:

```markdown
# React Hooks Optimization

> 2026-05-30

## Summary

Discussed performance optimization strategies for React Hooks in large projects, including useMemo and useCallback usage patterns, and how to avoid unnecessary re-renders.

## Key Points

- useMemo should only be used for expensive computations
- useCallback only makes sense with memoized components
- Custom hooks can encapsulate complex state logic

---

## Conversation

### User

Help me check this code for performance issues...

### AI

This code has a few issues...
```

## Filename rules

| Rule | Example |
|------|---------|
| Format | `YYYY-MM-DD-topic.md` |
| Topic uses English or pinyin | `react-hooks`, `api-design` |
| Duplicate topics get a sequence number | `2026-05-30-react-hooks-2.md` |

## Notes

- Conversation content is preserved verbatim — no condensing or rewriting
- Sensitive information (passwords, keys, tokens) is not saved
- Code snippets use appropriate syntax highlighting
- Multi-topic conversations are grouped by topic with H2 headings

## License

MIT