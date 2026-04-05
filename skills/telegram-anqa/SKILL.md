# Skill: Telegram → Anqa Input Channel

**What it does:** Connects a Telegram group to a session-based AI agent (Anqa). The agent processes messages, writes files to a markdown knowledge base, creates GitHub issues, and handles photos and PDFs.

**Use case:** Family or team uses Telegram naturally. Agent captures decisions, open questions, tasks, documents, and photos — no forms, no dashboards, no extra apps.

**Input:** Russian or English (agent translates)
**Output:** Structured markdown entries committed to git, GitHub issues created via API

---

## How it works

1. `/anqa` starts a session — Anqa is listening
2. Talk freely — she responds, writes files, creates issues
3. `/done` ends the session (or it times out after 10 min of inactivity)

## Commands

| Command | Action |
|---|---|
| `/anqa` | Start a conversation session |
| `/decision` | Log a decision (starts session if needed) |
| `/q` | Add an open question |
| `/task` | Create a task / GitHub issue |
| `/note` | General note — agent decides where it lands |
| `/vision` | Next photo will be analyzed by the agent |
| `/status` | Current priorities and open questions |
| `/help` | List all commands |
| `/done` | End the current session |
| `@anqa` | Ask the agent a question directly |

Photos with captions and PDF files are processed automatically during an active session.

---

## Stack

- Python (`python-telegram-bot`, `anthropic`, `gitpython`)
- Claude API — agent processing (tool use for file writes, git, GitHub)
- GitHub API — issue creation and label management
- Git — vault commits
- No orchestration layer needed — bot runs as a single Python process

---

## Agent capabilities

- **File writing** — creates and updates markdown files in the vault
- **Git operations** — commits and pushes changes
- **GitHub issues** — creates issues with labels from the project taxonomy
- **Vision** — analyzes photos sent after `/vision` command
- **PDF processing** — extracts and structures content from PDF attachments
- **Session memory** — maintains conversation context within a session

---

## Agent prompt structure

```
You are Anqa, digital steward of Tariqa.

CORE RULES:
- Input may be in Russian. Always output in English.
- Translate faithfully — do not summarise away detail.
- Family health and safety is always the highest priority.

COMMANDS:
/decision → Extract: decision, owner, deadline, vector, reasoning
/q        → Extract: question, owner, resolve-by, priority
/task     → Extract: task, owner, due, vector → create GitHub issue
/note     → Summarise, suggest target file
/vision   → Analyze next photo
/status   → Brief summary of open items and priorities

End structured outputs with:
> React 👍 to confirm and write to vault, or reply to edit.

TOOLS AVAILABLE:
- write_file(path, content) — write to vault
- git_commit_and_push(message) — commit and push
- create_github_issue(title, body, labels) — create issue
```

---

## License

Apache 2.0
