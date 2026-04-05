# GitHub Infrastructure Bootstrap

**Date:** 2026-04-05
**Decision:** D8 — Tasks managed via GitHub Issues, labels mapped to five vectors, Kanban board via GitHub Projects.

---

## What was set up

### Repo hygiene
- Added `.gitignore` to both `tariqa` (public) and `tariqa-vault` (private) repos
- Excludes: `.obsidian/`, `.DS_Store`, `.env`
- Committed and pushed bot code (`anqa_bot.py`, setup docs) that was previously untracked in the private repo

### Label taxonomy on `tariqa-vault`
Replaced GitHub's default labels with a structured system:

- **Vector labels** (5): `family`, `farm-infrastructure`, `community`, `documenting`, `security-privacy`
- **Priority labels** (4): `critical`, `month-one`, `month-two`, `parked`
- **Owner labels** (5): `owner:diana`, `owner:alisher`, `owner:anqa`, `owner:gestor`, `owner:family`
- **Status labels** (3): `blocked`, `in-progress`, `needs-research`

### 18 GitHub Issues from open-questions.md
Every open question (OQ-001 through OQ-018) converted to a GitHub issue with full context from the source file. Each issue tagged with appropriate vector, priority, owner, and status labels.

### Kanban project board
Created "Tariqa — Kanban" project (board format) under `xAlisher` and added all 18 issues. Column customization (Backlog/Open/Blocked/In Progress/Done) to be refined via the web UI.

## Why

The vault's `open-questions.md` was a flat file with no assignment tracking, no priority filtering, and no visibility for Diana or other stakeholders. GitHub Issues + Projects gives us:

- Filterable views by vector, owner, or priority
- A shared Kanban board accessible without Obsidian
- A foundation for Anqa (the bot) to create and update issues programmatically
- Clear ownership and status tracking across the family
