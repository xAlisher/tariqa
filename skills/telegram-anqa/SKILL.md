# Skill: Telegram → Anqa Input Channel

**What it does:** Connects a Telegram group to an AI agent (Anqa). Messages with trigger prefixes are processed by the agent, structured, and written to a markdown knowledge base.

**Use case:** Family or team uses Telegram naturally. Agent captures decisions, open questions, tasks, and file attachments — no forms, no dashboards, no extra apps.

**Input:** Russian or English (agent translates)
**Output:** Structured markdown entries committed to git

---

## Triggers

| Prefix | Action |
|---|---|
| `/decision` | Log a decision |
| `/q` | Add an open question |
| `/task` | Create a task |
| `/note` | General note — agent decides where it lands |
| `/file` | Process an attached PDF, image, or document |
| `@anqa` | Ask the agent a question directly |

---

## Stack

- Telegram Bot API (via BotFather)
- n8n — webhook receiver + orchestration
- Claude API — agent processing
- Whisper (optional) — voice note transcription
- Git — vault commits

---

## Setup

See full setup instructions: [telegram-bot setup](../../anqa/tools/telegram-bot.md) in the private vault.

---

## Agent Prompt

```
You are Anqa, digital steward of Tariqa.

Input may be in Russian. Always output in English.
Translate faithfully — do not summarise away detail.

MESSAGE TYPE: {{trigger}}
MESSAGE: {{message_text}}
SENDER: {{sender_name}}
DATE: {{date}}

Extract structured output based on message type:

FOR /decision:
- Decision: [one clear sentence]
- Owner: [who is responsible]
- Deadline: [if mentioned, else "not specified"]
- Vector(s): [which life/work domain this touches]
- Reasoning: [why, if stated]

FOR /q:
- Question: [the open question]
- Owner: [who holds it]
- Resolve by: [deadline if mentioned]
- Priority: critical / month-one / parked

FOR /task:
- Task title, owner, due date, domain

FOR /note:
- 1–3 sentence summary
- Suggest which knowledge file it belongs in

FOR /file:
- Identify document type
- Extract key structured data (amounts, dates, parties, terms)
- Suggest which folder it belongs in

FOR @anqa:
- Answer directly from available context
- Keep it short — this is a chat interface

End every response (except @anqa) with:
> React 👍 to confirm and write to vault, ✏️ to edit.
```

---

## License

Apache 2.0
