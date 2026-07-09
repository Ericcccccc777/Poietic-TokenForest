# Security Policy 🔐

[English](SECURITY.md) · [简体中文](SECURITY.zh-CN.md)

**Last updated 2026-07-08 · Publisher: Poietic Studio**

Token Forest is a proprietary, local-first desktop app with no network access by default. We take reports about its security and privacy behaviour seriously — especially anything that contradicts our published [Privacy Notice](docs/PRIVACY.md).

## Supported versions

Only the latest public release receives security fixes unless a release note states otherwise. Older releases and development snapshots are unsupported — please upgrade.

## Reporting a vulnerability

Please report suspected vulnerabilities **privately** — do **not** open a public issue for an unpatched problem:

1. **Preferred:** this repository's *Security* tab → *Report a vulnerability* (GitHub private vulnerability reporting).
2. Email: [contact@tokenforest.com.au](mailto:contact@tokenforest.com.au) — subject line starting with `[SECURITY]`. (A dedicated `security@tokenforest.com.au` inbox is activating before the first public release.)

Ordinary bugs and feature requests are welcome in the public issue tracker.

Do **not** include in any report: your Claude/Codex logs, prompts or conversation content, source code, access/refresh tokens, or other users' leaderboard data. If we need artifacts, we will arrange a minimal, private way to share them.

### What to include

- Token Forest version and exact download filename (plus its SHA-256 if possible);
- operating system and architecture;
- clear impact description and reproducible steps or proof of concept;
- whether the leaderboard was Off, Paused or On;
- whether the issue has been disclosed anywhere else;
- how you would like to be credited (or anonymity).

## In scope

We especially welcome reports of:

- any upload of local logs, prompts, conversation content or source-code files;
- **any network request while the leaderboard is off** (the app promises zero);
- a mismatch between the consent dialog / Privacy Notice and what is actually sent;
- leaderboard authentication or row-level-security bypass (reading or modifying another user's row);
- exposure of access/refresh tokens;
- local storage readable across OS user boundaries;
- arbitrary code execution, unsafe archive/update handling, DLL or library hijacking;
- tampering with official downloads, checksums or signatures;
- failure of the advertised leaderboard-deletion flow.

Please use only your own accounts and test data, and stop once the issue is demonstrated.

## Out of scope (usually)

- UI, animation or layout bugs; feature requests;
- token-count differences explained by our documented metric definitions;
- SmartScreen warning that a new file is "not commonly downloaded" when signature/hash are otherwise valid;
- issues requiring full prior control of the user's OS account;
- automated scanner output without demonstrated impact;
- social engineering of team members.

We may still act on out-of-scope reports that expose real user risk.

## Our response

Targets, not guarantees: acknowledge within **3 business days**; initial assessment within **7 business days**; status updates at least every **14 days** for confirmed issues. For critical issues we may pull affected downloads immediately. Fixes are rebuilt from a clean commit, re-signed where applicable, republished with new checksums, and announced in the release notes; withdrawn binaries stay marked rather than silently rewritten.

If you act in good faith — avoid privacy harm, use only your own data, allow reasonable time to fix — we will work with you, and with your permission credit you in the release notes.

## Privacy requests

Requests to delete a leaderboard entry or questions about data handling are not vulnerabilities — see the [Privacy Notice](docs/PRIVACY.md) contact section. Never send anyone your `account.json` tokens.

## Release authenticity

Official downloads come only from [the official website](https://www.tokenforest.com.au) and this repository's Releases, each with a SHA-256 checksum and a stated signing status. A step-by-step verification guide ships with the first release. Do not run a download that fails verification — delete it, re-download from an official channel, and report it if the mismatch persists.

Thank you for helping keep the forest safe. 🌳
