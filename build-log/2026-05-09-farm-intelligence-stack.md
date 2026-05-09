# Farm Intelligence Stack

**Date:** 2026-05-09

---

## What we built

A fully local AI assistant — named Anqa — that knows the physical farm, the family, the finances, and the open work. She runs on our home server (a desktop PC in Valencia), costs nothing per query, and operates across three channels: a chat interface, a sync pipeline, and outbound voice calls.

---

## The stack

**Hardware:** A desktop PC (AMD Ryzen 9 5950X, 64GB RAM, RTX 3090 24GB) running Ubuntu Server 24.04. Accessible remotely over Tailscale. Static IP on the local network, always on.

**Inference:** `llama.cpp` serving Qwen3.6-27B (Q5_K_M quantization) on the GPU. ~37 tokens/second. Enough for serious reasoning, fast enough for conversation. No API costs, no data leaving the building.

**Interface:** Open WebUI — a self-hosted chat UI with RAG (retrieval-augmented generation). Anqa is a named model profile in Open WebUI, backed by the local LLM and wired to a knowledge collection called "Tariqa Farm".

**Knowledge:** A private git repo (the vault) containing markdown files: the land, the house, farm operations, people, finances, infrastructure vision, and Anqa's own identity brief. Plus GitHub Issues from the same repo, fetched and included in every sync.

**Sync pipeline:** A shell script running every 6 hours on the server. It pulls the latest vault, fetches all GitHub Issues, resets the knowledge collection in Open WebUI, and re-uploads everything. Nine files per run. Anqa always has current context.

**Web search:** SearXNG — a self-hosted meta-search engine — wired into Open WebUI. Used on demand for anything outside the vault: prices, news, external information.

**Voice calls:** A Telegram bot (`/call` command) that triggers outbound phone calls via ElevenLabs (Spanish voice) and Twilio. Built for recurring calls: water delivery, irrigation cooperative, supplier contacts. The call script is injected as the agent's context. A webhook receives the transcript and saves it to the vault. Currently halted pending Twilio identity verification.

**Monitoring:** Uptime Kuma watching all containers and services. Stream Deck integration planned — one glance to see if anything is down.

**Infrastructure repo:** `tariqa-infra` (GitHub, private) — one repo for the whole farm. Machine-specific config lives under `machines/<name>/`, fleet docs under `fleet/`, GitHub Issues as the task tracker with `machine:` labels. No TASKS.md files — everything is an issue.

---

## What makes this different

Most homelab setups are technically impressive but contextually empty. The server knows nothing about the people using it or why it exists.

Most "second brain" / PKM setups are rich in personal context but disconnected from infrastructure. The knowledge lives in Obsidian, the server runs Jellyfin, and these two worlds never meet.

What we built is one system. The AI assistant knows:
- That the orange groves produce roughly €8k/year net and the cooperative picks up in autumn
- That Diana is the designer and co-founder, and her Telegram handle is @dvoroneca (not her GitHub handle)
- That the 4-month-old daughter's health is the highest-weighted vector in any decision
- Which GitHub Issues are open, who owns them, and what's blocking what
- That the DIR-1960 router is running OpenWrt and VLANs are the next network task

And she can act on that knowledge — not just answer questions, but make phone calls, log decisions, create issues, process receipts, update the vault.

The vault is the source of truth. The infrastructure repo is the operational layer. The AI sits at the intersection.

---

## The architecture pattern

```
tariqa-vault (private git)
    ├── knowledge/          ← land, house, people, finances, farm ops
    ├── anqa/               ← identity brief, skills, call scripts
    └── decisions/          ← all decisions made and why

tariqa-infra (private git)
    ├── machines/sneg/      ← server scripts, services, sync pipeline
    ├── fleet/              ← hardware profiles for every machine
    └── GitHub Issues       ← task tracker, labeled by machine + topic

Anqa (running on Sneg)
    ├── Chat                ← Open WebUI + Qwen3.6-27B + vault knowledge
    ├── Sync                ← every 6h: vault + issues → knowledge collection
    └── Voice               ← Telegram /call → ElevenLabs → Twilio → phone
```

The key design decision: **everything flows through files.** No proprietary databases, no platform lock-in. The vault is markdown and git. The infra is shell scripts and YAML. The AI reads files, writes files, commits files. If we switch models tomorrow, the knowledge stays. If Open WebUI goes away, the vault stays. If Tailscale closes, we SSH directly.

---

## What's next

- VLANs on the router (IoT isolation — Key Light and smart home devices on a separate segment)
- Home Assistant (Docker on the server, once VLANs are ready)
- Backup automation (restic + Arduino relay: drive powers on at 5am, backup runs, drive goes offline)
- Navidrome (music server — the existing music library finally streamable)
- Uptime Kuma → Stream Deck (service health visible at a glance)
- Twilio KYC unblocked → first live outbound call

---

## Why local

The decision to run everything locally wasn't just cost (though the math works: inference at ~37 tok/s on hardware we own vs. API costs at scale). It was sovereignty.

The vault contains real family information — finances, health considerations, legal questions about the land. We're not comfortable routing that through third-party APIs, even trusted ones. Local inference means the context stays in the building.

The tradeoff is real: setup complexity, hardware responsibility, no elastic scaling. For a family farm, that's acceptable. The knowledge is ours. The inference is ours. The bills are predictable.

---

*This is an entry in the [Tariqa build log](README.md). We document what we build.*
