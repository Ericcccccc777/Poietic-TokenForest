# Token Forest — FAQ ❓

[English](FAQ.md) · [简体中文](FAQ.zh-CN.md)

## The basics

### What is Token Forest, in one sentence?
A pixel desktop pet: a tree that lives above your taskbar and grows from the tokens you spend in Claude Code / Codex.

### Is it free?
Yes — Token Forest is free during the public beta, and the core experience will stay free.

### Which platforms are supported?
Windows 10/11 and macOS. Linux is on our radar but not officially supported yet.

### Which AI tools does it track?
Claude Code and Codex today. More assistants are under consideration — [tell us which one you use](../../../issues/new/choose).

## Privacy

### Does it read my code?
**No.** It reads the usage logs those tools already keep locally and uses only their metadata — token counts, model names, timestamps, session titles. It never opens your code files, and never stores or uploads prompts or conversations. Full details in the [Privacy Notice](PRIVACY.md).

### Does it need the internet?
No. Everything works fully offline. The single optional network feature is the leaderboard, which is off until you enable it — and leaving it deletes your entry.

### Is the source code available?
The app is developed in a private repository and isn't open source at this time. We're exploring opening core components (like the usage reader) so the privacy claims can be independently verified.

## The tree

### How fast does the tree grow?
It grows with your usage across 8 stages. Heavy agentic sessions move it visibly; a quiet day barely stirs the leaves. Exact thresholds are part of the game — where's the fun otherwise?

### Why is my token number so big?
Token Forest counts **all four token classes** — input, output, cache read, cache write — the same way usage dashboards do. Agentic tools re-read your conversation context on every tool call, so cache reads dominate and totals climb into the billions. That's normal. The dashboard's cost view weights each class by its actual price, so the *money* number stays honest.

### Do tokens count while the app is closed?
Currently the tree only grows while the app is running. "Offline catch-up growth" is on the [roadmap](ROADMAP.md).

### Can I have more than one tree?
You unlock and switch between **four** species (Apple, Cherry Blossom, Cactus, and the 🎄 Christmas Tree — each keeps its own progress, fruit, and decorations). Each one unlocks the next as you harvest its fruit, and the Christmas Tree sits at the end of the chain. A fifth species is already sprouting in the greenhouse.

### What are fruit for?
Mature trees produce fruit over time. Harvest by clicking, then spend fruit in the shop on decorations for your tree.

### The tree is covering my window!
Switch to **capsule mode** — a tiny status pill in the corner — or toggle always-on-top off, or just drag the tree somewhere else. Your forest should never fight your work.

## Leaderboard

### What does the leaderboard upload?
Exactly what its consent dialog lists — nothing more. The full field table lives in the [Privacy Notice](PRIVACY.md), including the four anti-cheat aggregates added in v0.1.5 and why the per-window timeline is never uploaded.

### How do I get off the leaderboard?
Turn it off in the app. It asks the server to delete your entry — removed from the board, not just hidden.

## Anything else?

Open an [issue](../../../issues/new/choose) or email [contact@tokenforest.com.au](mailto:contact@tokenforest.com.au) — we read everything.
