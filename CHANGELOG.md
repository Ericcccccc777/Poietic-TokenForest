# Changelog 🌱

[English](CHANGELOG.md) · [简体中文](CHANGELOG.zh-CN.md)

Public release notes for Token Forest. Dates are when features reached the beta.

## August 2026 — what it all costs

- 💵 **Your tree now has a price tag** — every token you collect is priced at its model's published rate, so the tree carries a running dollar estimate. An estimate, not a bill: subscriptions, discounts and free allowances are not reflected.
- 🏷️ **The leaderboard knows which models** — popping a bubble also records which vendor and which model produced those tokens. Two new boards on the website follow from it: **vendor usage** (what the community actually runs on) and **forest value** (whose tree is worth the most). Only bubbles you popped yourself count, and nothing from before you installed the app is ever read.
- 🔄 **Prices keep themselves current** — the price table refreshes daily, so a new model or a vendor price cut lands without waiting for an app update.
- 🔐 **Credentials moved into the system keychain** — macOS Keychain and Windows Credential Manager, instead of plain text in the data folder.
- ✅ **All 97 model prices verified against the vendors' own pages** — 15 wrong prices corrected (the whole Mistral line, the late-July GPT-5.6 cuts and more) and 10 retired models removed.
- 🆕 **A brand-new model version no longer shows $0** — until its price is published it borrows the previous version's rate, instead of counting as unpriced.
- 🔧 **"Auto-update prices" is now actually respected** — it used to download daily whenever the leaderboard was on, which matched neither the setting nor the privacy notice.

## July 2026 — the forest grows

- 🌍 **Every model you run, priced right** — the Dashboard now recognizes DeepSeek, Kimi, GLM (Zhipu), Qwen, MiniMax and Xiaomi MiMo — when you route them through Claude Code or Codex — as their own providers and prices them at their own rates, instead of lumping them under Claude/Codex (where their cost was silently dropped).
- 🪪 **README badges** — every leaderboard player gets an embeddable badge that leads with your token count, shows your worldwide rank, and draws your current tree species. Grab yours from the app's **Badge Setup**.
- 🔧 **Leaderboard reliability** — fixed the root cause of a sync issue that could quietly drop an opted-in player off the board.
- 🎄 **Christmas Tree — the fourth species** — a snow-dusted pine, unlocked at the end of the progression chain. Hang ornaments, string the lights, and trim it all the way to "Christmas Splendor." Every species now carries its own fruit and its own set of stage names.
- 🌏 **Now in four languages** — the app UI speaks English, 中文, 日本語 and 한국어 (the website already did).
- 📊 **Dashboard** — growth, usage and per-conversation receipts, a 26-week heatmap, per-project splits and offline pricing across every provider — now shipping.
- 💊 **Capsule mode** — Dynamic-Island-style mini pill: see which engine is running and whether it's done, without the full tree on screen.
- 🌸 **Two new species** — Cherry Blossom and Cactus join the Apple Tree, each with its own themed decorations (torii gate, stone lantern, wind chimes, bamboo fence, and more).
- 🍎 **Fruit & shop** — mature trees bear fruit; harvest it and spend it on decorations you can equip per tree.
- 🏆 **Global leaderboard (opt-in)** — anonymous worldwide ranking on the website; opting out deletes your entry.
- 🍏 **macOS support** — the forest now grows on Macs too.
- 📏 **Unified token metric (v3)** — the tree, bubbles, curves and leaderboard all count the same four token classes, so every number in the product agrees.

## June 2026 — first seedling (initial beta)

- 🌱 **The core loop** — a patch of soil above your taskbar; a pixel tree that grows through 8 stages from the tokens you spend.
- ⚡ **Live local tracking** — incremental, real-time reading of Claude Code and Codex usage logs. Local-only, offline, no telemetry.
- 💬 **Token bubbles** — per-conversation bubbles, color-coded by source, bouncing as numbers climb.
- 🎛️ **Desktop-pet manners** — drag, snap to corner, lock, always-on-top, autostart, hide/show, click-to-wiggle, polished right-click menu.
- 🌏 **English & 中文** app UI.

---

🌲 *Next up: one-click installers and the next species — see the [roadmap](docs/ROADMAP.md).*
