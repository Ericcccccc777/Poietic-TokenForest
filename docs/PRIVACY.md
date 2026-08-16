# Token Forest Privacy Notice

[English](PRIVACY.md) · [简体中文](PRIVACY.zh-CN.md)

**Version 1.0-beta · Last updated 2026-08-16 · In force since the first public release (v0.1.0, 2026-07-09)**
**Publisher: Poietic Studio**

Token Forest is a desktop companion that turns your Claude Code / OpenAI Codex usage into a growing pixel tree. This notice describes exactly what the app reads, stores, and — only if you opt in — uploads. The same text is published at [tokenforest.com.au/privacy](https://www.tokenforest.com.au/privacy); this file's git history is the public change log of the policy.

## Summary

- Core features run **entirely on your device**. No account, no API key, no network needed.
- The app contains **no telemetry, no ads and no crash reporting**. The optional update check is off by default, and even with it on the app never installs anything by itself — it tells you a new version exists and, if you ask, downloads the installer for you to run.
- It reads the **usage logs your AI coding tools already write locally** — never your source-code files.
- It does **not store or upload prompts or conversation content**.
- The **global leaderboard is optional and off by default**. Before it turns on, the app shows a consent dialog listing every field it would sync. Turning it off requests deletion of your entry.
- We do not sell personal data. There is nothing to sell — by default we never receive any.

## What the app reads locally

Token Forest reads the local usage logs created by supported tools:

```text
Claude Code:  ~/.claude/projects/**/*.jsonl
OpenAI Codex: ~/.codex/sessions/**/rollout-*.jsonl
```

From these logs it uses: token counts (input / output / cache read / cache write), timestamps, source (Claude or Codex), model identifiers, session identifiers, project-directory names, Git branch names, AI-generated session titles, and message-type structure (used only to tell genuine user turns apart from tool results).

To parse a log line, its full content — which can include prompt text — passes through memory. Token Forest does not need prompt meaning, does not copy prompt or conversation text into its own data files, and never uploads it. It never opens your source-code files.

## What the app stores locally

The current beta stores its data files next to the application. A future release will move them to standard per-user directories (Windows: `%LOCALAPPDATA%\TokenForest\`, macOS: `~/Library/Application Support/TokenForest/`) with automatic migration.

| File | Contents |
| --- | --- |
| `garden.json` | Per-tree tokens, growth stage, fruit, decorations, first-use time; plus the running per-model totals of the tokens you collected (model name + the four counts, no dates) |
| `config.json` | Window position, language, bubble mode, leaderboard state, display name, region |
| `growth_ledger.json` | Growth history by date × tree × token type |
| `usage_ledger.json` | Aggregated session metadata: log file paths, project names, branches, AI titles, times, models, daily token totals |
| `account.json` | Only if the leaderboard was enabled: anonymous user ID and Supabase session tokens |
| `sync_error.json` | Only if the leaderboard was enabled: the last leaderboard-sync error message and its timestamp (diagnostic only; never uploaded) |
| `update_state.json` | Only if the update check ran: when it last succeeded and when it last tried, plus the cached latest version number, release-page link, and the installer's SHA-256 and size |

These files stay on your machine and are never uploaded. `usage_ledger.json` contains local metadata (such as file paths) that other users of your computer could read if they can read your files; treat the app's data folder as private. From v0.2.0 the session tokens live in the operating system's credential store — Keychain on macOS, Credential Manager on Windows. A copy stays in `account.json` so that an older build, which does not know about the credential store, still finds your account instead of registering a new one and stranding your leaderboard row. Deleting these files (or uninstalling and deleting the folder) removes all local data.

## Network behaviour

By default Token Forest makes **no network requests at all**. Growth, bubbles, the shop, capsule mode and the dashboard all work offline. Cost estimates use a bundled price table.

The features that can go online are the leaderboard, the price-table update and the update check. Each is off by default, and none of them does anything until you act:

- **Leaderboard** — off by default; see the next section.
- **Price-table update** (v0.1.5+) — clicking **"↻ Update prices"** in the dashboard, or turning on **"Auto-update prices"** in Settings (off by default; when on, at most one check per day), downloads a single static file, `https://tokenforest.com.au/pricing.json`, so newly released models can be priced without waiting for an app update. This is a **download only**: the request carries no usage data, no identifiers and no account. The file is validated and cached locally; on any failure the app silently keeps using the bundled/cached table.

- **Update check** (v0.2.1+) — off by default. You can turn it on in the first-run welcome dialog or in **Settings → About**, and there is a manual **“Check for updates…”** you can click once without turning anything on. When on, the app asks GitHub for the latest release: `GET https://api.github.com/repos/Ericcccccc777/Poietic-TokenForest/releases/latest`, **at most once a day after a successful check**; while it cannot connect it retries at most every 6 hours (so at most four attempts a day). The request has no body, no query string, no cookies and no authorization; the only headers the app sets are three fixed constants (`User-Agent: TokenForest-update`, `Accept: application/vnd.github+json`, `X-GitHub-Api-Version: 2022-11-28`) that are identical on every install. It carries **no version number, no platform, no identifier and no usage data** — the version comparison happens on your machine. Nothing is downloaded until you click **Download update**; the file is then checked against the SHA-256 published in that same GitHub release, keeps its macOS quarantine / Windows mark-of-the-web flag, and is only revealed in Finder / File Explorer. **The app never installs it, never replaces itself and never asks for elevated privileges.** Automatic checks fail silently and are treated as “no new version”; a manual check shows a message written into the app, never text returned by the server.

  Turning this on adds **GitHub** as a network counterparty. Like any online service, GitHub and the networks in between may process your IP address, request time and standard server logs under their own policies — we will not claim otherwise, and those logs are not ours to see. And even a request that carries no data still says something by existing: a machine with the update check on leaves a trace at GitHub of roughly which days it was switched on. That is the cost of the feature, which is why it is off until you turn it on.

Menu items that open a web page (for example the leaderboard website) launch your default browser; the desktop app itself sends nothing in the background.

## Optional leaderboard

The leaderboard is off by default. Selecting **On** shows a consent dialog listing exactly what will sync; nothing is sent unless you confirm it.

When enabled, the app creates an anonymous account with Supabase (our database provider) and syncs, roughly every 30 minutes and at moments like startup, tree switch, and quitting:

| Field | Shown publicly? |
| --- | --- |
| Random anonymous ID (generated by Supabase; owns your row, and is the address of your badge image and your project image) | Yes (it appears in those two links) |
| Display name (blank = a generated "Anonymous#id" name) | Yes |
| Total collected tree tokens | Yes |
| Each tree's token total and growth stage | Yes (tree details) |
| Region — only if you picked one | Yes (flag) |
| Current tree species | Yes |
| App version | No |
| Previous anonymous ID — only after a session reset re-registers you; links your new row to the one it replaced so the stale one can be retired (v0.1.6+) | No |
| Anti-cheat summary — four numbers, see below (v0.1.5+) | No |
| Model breakdown of the tokens you collected — model name, its vendor, the input / output / cache-read / cache-write counts and their sum, with no dates attached (v0.2.0+) | Yes (model boards) |
| **Project showcase** — a project name, a one-line description, a link and one image, all written by you (v0.2.2+). Off by default, inside the leaderboard settings; see the “Project showcase” section below | Yes |
| Server-generated created/updated timestamps | May be shown |

In that column, "Yes" means it appears on a public page and "No" means it does not. The four anti-cheat numbers are additionally locked at the database level: the public read-only key that the app and the website use is refused those columns outright.

Small print: if you leave the name blank, the generated anonymous name is rendered in your app language, so the leaderboard indirectly reflects which UI language you use.

### What the model breakdown is used for (v0.2.0+)

Two public boards are built from it, besides the token board:

- **Vendor usage** — every player's tokens for a given vendor, and for a given model, added together. These are whole-community totals; one player's usage cannot be read back out of them.
- **Forest value** — an estimate of what your collected tokens would have cost, shown next to your name.

The value figure is worked out on our server by multiplying the token counts you already sync by each model's published price. **No money figure is ever sent from your machine**, and no new field is uploaded for it. It is an estimate and not a bill: subscriptions, discounts and free allowances are ignored, a vendor price change moves everybody at once, and the model each token is filed under comes from your own machine and is not independently verified. Both boards state how much of all counted tokens they actually cover, because the model data only starts from the release that introduced it.

### The anti-cheat summary (v0.1.5+)

A leaderboard score is a number your own machine computes, so on its own it proves nothing — and it cuts both ways. Someone can inflate it by editing a local file, while an honest heavy user who lets bubbles pile up all day and collects them at once produces a jump that looks identical to that. To tell the two apart, each sync that raises your score carries four aggregate numbers describing how the increase was earned:

- how many **5-minute windows** the new tokens are spread across,
- how many tokens are in the **busiest single window**,
- their **sum**, and
- the **time span** from the earliest window to the latest.

The windows are keyed on the timestamps in the Claude Code / Codex logs themselves — when the tokens were actually spent — so a hoarded workday correctly reads as many ordinary windows rather than one impossible spike.

**We deliberately do not upload the per-window timeline.** A 5-minute-resolution record of your token use would amount to a log of when you work and when you sleep. The four aggregates cannot reconstruct that: they say *how big* the busiest window was, never *which* window it was. The precise per-window figures are computed on your machine, used to derive the four numbers, and never leave it.

These four numbers are **not shown on the public leaderboard** — the database revokes read access to those columns for the public read-only role. They are readable only by an administrator reviewing a specific account, and they are advisory: they inform a human decision, they do not automatically punish anyone. If the app cannot vouch for its own figures (for example, it was upgraded mid-stream, or it was closed between collecting a bubble and syncing), it sends nothing rather than send something wrong.

### The model breakdown (v0.2.0+)

The leaderboard has boards beyond "biggest tree" — most-used model, one vendor against another. They are fed by a per-model breakdown of your tokens: the model name (say `claude-opus-4-8`), the vendor it belongs to, and the four token counts plus their sum.

**It covers only the bubbles you popped yourself.** Every bubble carries the breakdown of which models burned it, and that breakdown is banked at the exact moment you collect the bubble — the same instant, the same energy, that raises your tree score. A bubble that expires unpopped counts for neither. Token Forest does not go digging through logs from before you installed it in order to build this.

The vendor is derived from the **model name**, not from which CLI wrote the log: people routinely route DeepSeek, GLM or Kimi through Claude Code via `ANTHROPIC_BASE_URL`, and attributing by source would file those under Claude.

**It carries no dates.** Running totals only — no per-day, per-hour or per-session split — so like the four anti-cheat numbers it cannot reconstruct when you work and when you rest. The per-date breakdown stays on your machine, for the dashboard.

Tracking begins with v0.2.0. Tokens collected before it have no model attribution and are not backfilled, so the model total is normally lower than your score.

A sync carries at most 30 models (a real user typically has 5–15); anything beyond that is dropped by token count. Model names pass two checks: the app folds anything outside a strict character set into a single `unknown` entry — usage is not lost, but no arbitrary string reaches a public page — and the server independently re-checks the character set and a banned-word list, dropping rows that fail.

**Never uploaded, in any mode:** raw logs, prompts or conversation content, source code, session titles, file paths, project names, Git branches, per-session usage, cost estimates, anything about tokens you never collected, or any per-window / time-of-day breakdown of your token use — including any per-date breakdown of the model figures above.

Like any online service, Supabase's infrastructure processes standard connection data (such as IP addresses and request timestamps) to operate and secure the service, under Supabase's own policies.

### On · Paused · Off

- **On** — syncs periodically.
- **Paused** — stops updates; your last entry stays on the board.
- **Off** — stops syncing and sends a request to delete your row.

Beta limitation, stated plainly: if the deletion request fails (for example, you are offline), the current beta does not yet retry or confirm it. Toggling Off again while online re-sends it. Reliable delete-with-confirmation is planned before the stable release. You can also ask us to delete your entry (see Contact) — mention the anonymous name/ID shown in the app, and never send us your tokens from `account.json`.

## Website

The official website ([tokenforest.com.au](https://www.tokenforest.com.au)) uses **no analytics, no advertising trackers, and no marketing cookies**. Its hosting provider processes standard server logs (IP address, user agent, requested page, time) to serve and secure the site. The leaderboard page reads the public leaderboard rows described above; viewing it requires no login. The site also serves a badge image to any player who asks for one: its address contains your anonymous ID, and it shows the same public figures as your leaderboard row. Wherever you paste it, that page's visitors — or that host's image proxy — fetch it from us, so those requests appear in the ordinary server logs described above. If we ever add analytics or similar services, this notice will be updated first.

The home page shows a demo video hosted on YouTube. Nothing is fetched from YouTube until you press play: at rest the page shows only a still image served from this site. Once you press play, the video loads from YouTube's no-cookie player domain, and from that point YouTube may set its own cookies and receive your IP address under Google's privacy policy. You can avoid it entirely by not playing the video.

## Service providers

We use a small number of providers, only for the functions described: Supabase (anonymous auth + leaderboard database), the website host, and GitHub (this repository, issues, release downloads). Provider regions and policy links will be finalised in this section before the first stable release.

## Project showcase (v0.2.2+, off by default)

Inside the leaderboard settings there is a switch called **Project showcase**. Turn it on and
you can add a project name (up to 24 characters), a one-line description (up to 80), a link,
and one image. Those four things are synced along with your leaderboard entry and shown
publicly next to it. A few things worth stating plainly:

- **It is off by default, and it does nothing while the leaderboard itself is off.** While the
  switch is off, none of these four fields is sent at all.
- **You write it, so it appears exactly as written.** Do not put anything there you would not
  want public.
- **We can hold it back.** If your account is under review, your showcase stays private until a
  person clears it; the rest of your entry is unaffected, and nothing you wrote is deleted while
  it waits.
- **The image is re-encoded on your machine before it is uploaded** — resized to at most
  512 pixels on its longest side and 64 KB, and stripped of location and camera metadata in the
  process. If you pick a photo from your phone, its GPS coordinates do not go with it.
- **Turning the switch off takes it down.** The next sync clears those fields on the leaderboard
  and deletes the uploaded image; turning the leaderboard off entirely deletes them along with
  your whole entry. It is not merely hidden on your side. Beta limitation, stated plainly: that
  clean-up happens when the switch-off reaches us, so if you are offline — or the app's anonymous
  session has expired and can no longer authenticate — the entry and the picture stay as they
  were until a later attempt succeeds. Ask us and we will remove them for you.
- **Links must start with https://** and are checked before they are accepted. The text goes
  through the same word filter as display names, on your machine and again on the server.

## Verifying these claims

We take "trust us" seriously enough to know it isn't good enough. The app works with your network fully disabled — try it. Releases publish SHA-256 checksums and a signing status, and release notes call out any privacy or network change; four early builds are the exception — v0.1.0, v0.1.1 and v0.1.2 went out without a published checksum, and v0.1.9 without either. The source code is currently private, but we are exploring opening the core usage-reader component so the "reads logs, uploads nothing" claims can be independently audited.

## Your controls

- Use the app fully offline — never enable the leaderboard.
- Pause or turn off leaderboard sync at any time from the tree's menu.
- Change or blank your display name and region.
- Delete local data by deleting the app's data files / uninstalling.
- Turning Off requests deletion of your leaderboard entry. If that request can't complete — you are offline, or the anonymous session has expired and can no longer authenticate — the entry may remain on the board until a later attempt succeeds (the app records the failure locally). Contact us to confirm or force its removal.

## Changes

If a future version adds any new data processing — telemetry, crash reporting, auto-update checks, new leaderboard fields — this notice and the in-app consent will be updated **before** that version ships, and the release notes will call it out under "Privacy or network changes".

This has happened three times so far: the **price-table update** (shipped in v0.1.5, which added our website's hosting provider as a counterparty), the **update check** (v0.2.1, which added GitHub), and the **project showcase** (v0.2.2, which added the first fields you write yourself and the first file you upload). All three are off by default.

## Contact

```text
Publisher: Poietic Studio
Privacy:   contact@tokenforest.com.au (a dedicated privacy@tokenforest.com.au inbox is being set up)
Security:  see SECURITY.md
Website:   https://www.tokenforest.com.au
```

Privacy questions get answered first.
