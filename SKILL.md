---
name: chat-saver
description: Save AI chat conversations as structured markdown documents. Triggers when the user explicitly asks to save, export, archive, or write the conversation to a file (e.g., "save this conversation", "export chat", "write a record"). Does NOT trigger when the user just wants a verbal summary ("summarize this", "what did we discuss") — those are answered inline.
---

# Chat Saver

Save the current conversation as a structured markdown document to the project's `chats/` directory.

## Why

Conversations with AI often contain valuable analysis, decisions, and code solutions — but they disappear when the session ends. This skill preserves the full conversation: a summary at the top for quick scanning, followed by the verbatim dialogue for detailed review.

## When to save

Execute when the user **explicitly asks to save the conversation to a file**. Keywords include: save, archive, export, write to document, record.

**Do NOT trigger when**: the user only wants a verbal summary or review, e.g., "summarize this", "what did we discuss". Answer inline in those cases. Only create a file when the user expresses intent to persist to a file.

## Process

### 1. Collect conversation content

Review the full context of the current session and extract the conversation turn by turn. Collection rules:
- **Preserve verbatim**: keep the user's words and the AI's responses as close to the original as possible — do not condense, omit, or rewrite
- Tool call details (e.g., reading a file, running a command) do not need to be preserved, but **valuable results** from tool calls (code snippets, config content, key findings) should be kept as part of the AI's response
- Brief user confirmations (e.g., "OK", "right", "好的", "对") should also be preserved — they mark the rhythm of the conversation

### 2. Generate topic summary

Summarize based on the conversation:
- **Topic**: the core subject of this conversation (1-5 words, used as filename)
- **Summary**: 2-5 sentences covering the main content and conclusions
- **Key Points**: 3-7 bullet points listing the most important findings, decisions, or conclusions

### 3. Organize conversation content

Record the conversation turn by turn, verbatim, using this format:

```markdown
### User

{user's original words, preserved verbatim}

### AI

{AI's original response, preserved verbatim}
```

The core principle of the conversation section is **faithful reproduction** — write exactly what the user and AI said, no condensing, no omitting. This is the most essential value of the document: enabling a full retrospective of the discussion process later, not just the conclusions.

### 4. Generate filename

Format: `YYYY-MM-DD-topic.md`

- Use today's date
- Topic uses English words or pinyin, separated by hyphens, e.g., `react-hooks`, `api-design`
- If a file with the same topic already exists, append a number, e.g., `2026-05-30-react-hooks-2.md`

### 5. Save the file

Save to the `chats/` directory under the project root (create it if it doesn't exist).

Full path: `<project-root>/chats/YYYY-MM-DD-topic.md`

## Document template

Use the following template strictly:

```markdown
# {Topic}

> {Save date}

## Summary

{2-5 sentences summarizing the main content and conclusions}

## Key Points

- {Point 1}
- {Point 2}
- {Point 3}

---

## Conversation

### User

{User's original words, preserved verbatim}

### AI

{AI's original response, preserved verbatim}

### User

{Next turn from user}

### AI

{Next turn from AI}

(Continue alternating turns, verbatim...)
```

## Notes

- **Preserving the conversation verbatim is the most important principle**. Write exactly what the user and AI said — do not condense, omit, or rewrite
- The summary and key points sections serve as an auxiliary index, helping quickly determine whether to expand the conversation section later — these parts should be concise and distilled
- Use appropriate syntax highlighting for code snippets (```python, ```javascript, etc.)
- If the conversation covers multiple unrelated topics, group by topic using H2 headings
- Do not save content containing sensitive information (passwords, keys, tokens)
- Use the same language as the conversation (Chinese conversation → Chinese document, English → English)
- After saving, tell the user the full file path