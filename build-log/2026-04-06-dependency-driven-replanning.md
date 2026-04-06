# Dependency-Driven Replanning

**Date:** 2026-04-06

---

## What happened

We started with a clean four-week plan: Week 1 document the property, Week 2 finances and legal, Week 3 family, Week 4 agent setup. One domain per week, sequential, tidy.

Then we actually started working. Over two sessions we processed 14 property documents, created 35 GitHub Issues from them, and mapped every dependency between tasks. The result: our plan was wrong.

## What we found

Two bottlenecks dominated everything:

**Bottleneck 1: a single administrative task** (recovering a deposit from a previous landlord) was blocking five other tasks — not because of the money alone, but because the person responsible for those tasks was the same person negotiating the deposit. Bandwidth, not money, was the real constraint.

**Bottleneck 2: a professional consultation** (meeting with a local legal advisor) turned out to be blocking ten issues across permits, land classification, structures, tourism, and entity setup. We'd originally scheduled this for Week 2. It should have been Day 1.

Meanwhile, the Week 1 goal ("document the property") was already half done from processing the documents we had on hand. No need to wait for a photo walk — the legal and cadastral docs told us more than photos would.

## The pattern

1. **Create issues from real documents, not assumptions.** We started with 18 issues from a flat question list. After processing actual PDFs — deeds, bills, architect reports, zoning maps — we added 17 more. The documents surfaced dependencies we hadn't imagined.

2. **Map blockers explicitly.** Every issue gets a "Blocked by" section. When you do this honestly, the critical path reveals itself. Our "Week 2" legal task was actually blocking half the board.

3. **Count how many issues each task unblocks.** A single consultation unblocking 10 issues beats a week of documentation that unblocks zero. Prioritize by leverage, not by what feels productive.

4. **Watch for person-bottlenecks.** When one person owns 8 of 11 critical tasks and is also dealing with an emotionally draining blocker, no amount of planning helps. Triage their queue ruthlessly: close the blocker first, then sequence everything else.

5. **Let the plan be wrong.** The original weekly structure wasn't bad — it was a starting point. The value was in having something concrete to revise once reality showed up. A plan that survives contact with 14 documents unchanged wasn't a plan — it was a wish.

## What changed

- Legal consultation moved from Week 2 to Week 1
- Property documentation moved from Week 1 to Week 2 (waiting for bandwidth to free up)
- One person's task queue triaged down to three items: close the blocker, track one in-progress item, run one quick errand. Everything else waits.
- A consolidated question document was created for the consultation — 11 question groups pulled from all blocked issues. One meeting, maximum leverage.

## Tools used

- GitHub Issues with a label taxonomy (domain, priority, owner, status)
- A Kanban board for visibility
- An AI agent (Anqa) to process documents, create issues, and map dependencies
- Markdown files in a git-synced vault as the knowledge base

## Why it works

Plans fail when they're organized by topic instead of by dependency. "Week 1: Land, Week 2: Legal" assumes these are independent streams. They're not. The land questions feed into legal questions, which feed into permit questions, which feed into building questions. The graph matters more than the calendar.

An AI agent helps here because it can hold the full graph in context — every issue, every blocker, every owner — and surface the non-obvious connections. A human looking at a 35-item list sees tasks. An agent looking at the same list sees that item #35 unblocks ten others and should be #1.

The combination of human judgment ("this feels wrong, reprioritize") and agent analysis ("here are the dependency chains") is more powerful than either alone.

---

*This is entry 3 in the [build log](README.md).*
