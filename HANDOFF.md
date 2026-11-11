# HANDOFF – guide_arc_build-on-arc

> The author's working file, not content for readers of the series. On a new machine, read this file first.
> Rules for Claude Code are in `CLAUDE.md`. This file only records the **current state** – for older history see `git log`, don't copy it here.
> **Updated:** 2026-11-11.

## 0. What this repo is

A series on building apps on Arc, written for people who don't know crypto and have no programming background. The original content is the Vietnamese-language "Build on Arc bằng Claude Code" series on X by [@0xhieuxyz](https://x.com/0xhieuxyz) – this repo is its permanent home, because posts on X die after 48 hours.

**Translated to English on 2026-11-09.** The Vietnamese version is in the git history, before that commit. The folders `01-y-tuong/` and `04-hoan-thien-mainnet/` became `01-idea/` and `04-polish-mainnet/`.

**Guide only:** no sample project code, no "Examples" section, no "Where this prompt fell short" section (all removed Oct 20).

- GitHub: https://github.com/KattyFury/guide_arc_build-on-arc (public)
- Local: `D:\Files\Claude\guide_arc_build-on-arc`

## 1. Where things stand

4 steps. The old 6-step version was removed entirely (Oct 26), history is in git.

| Step | Folder | Where | Status |
|---|---|---|---|
| 1. Idea only → English Idea Brief (no tech) | `01-idea/` | Claude Chat | Written, not run for real |
| 2. Tech choice + plan | `02-arc-studio-plan/` | Arc Studio | Written, not run for real |
| 3. Build + testnet demo | `03-build-demo/` | Arc Studio | Written, not run for real |
| 4. Polish + mainnet | `04-polish-mainnet/` | Claude Code / Codex + Arc Studio CLI | Written, not run for real |

**▶ IN PROGRESS:** **The Step 1 prompt hasn't been run for real, in its current English form** – on the next run, use exactly the prompt in `01-idea`. At the end of the session, use a review prompt (make Chat list where it deviated from the prompt, one line each: rule | what happened | suggested fix), then fix the prompt directly. On 2026-11-11 the tech questions moved out of Step 1 and into Step 2 (tech choice + plan); the Step 2 prompt line hasn't been run for real in this form either.

**Sending the repo link to an AI chat (Oct 26):** defaults to Step 1 (come up with / refine an idea). Instructions are at the top of `README.md` + top of `CLAUDE.md` + `AGENTS.md`. Some AIs read a cached copy of the repo from before Oct 20 (6 steps, TapTip/EZwallet examples) – the repo can't delete those caches, so Step 1 still recommends pasting the prompt directly as the safest option.

**Unknown (don't make these up when writing more):** where the Plan toggle is on the studio.arc.io web UI (the docs don't describe the web UI); whether Arc Studio's preview links can be opened by outsiders.

**Verified Oct 20** (arc-docs MCP + npm + the Dell machine): mainnet chain `5042` / testnet `5042002`, RPC + explorer as in `ARC-RESOURCES.md`; 6 use-case directions in the docs; Arc Studio has Plan, GitHub Export, testnet-only deploys; the latest `@circle-fin/arc-studio-cli` is **1.2.1**, `skills install --tool` only supports `claude-code` (Codex uses `arc-studio run --output json`); Windows reports "Claude Code not found" → workaround in Step 4 section 4.2.

## 2. How to work

1. Write/edit the prompt for a step.
2. **Test it for real before publishing** – with someone's real project, or as a dry run.
3. If it falls short → fix the prompt. Done, no error history in the article.

## 3. Writing rules

- **Idea criteria:** fun things, things people just like using, count too (red envelopes don't solve any problem). What doesn't flex: it has to be something you or someone you know **actually does in real life**.
- **Voice:** plain, everyday English, first person "I" talking to the reader as "you". Short sentences, no clichés. Tables for comparisons, blockquotes for notes worth remembering, and every step ends with a line leading into the next.
- **Long dashes: only the en dash `–` (U+2013), no em dash (U+2014)** in any file readers see. Check with `grep -c`, which must return 0.

## 4. Step 4: read the skills before touching Circle/Arc

Before writing code that touches Circle Wallets or Arc, **load the right skill first**, don't dig through docs and trial-and-error:

- **Modular Wallets (Passkey, gasless)** → `circle:use-modular-wallets` (has an error table + the rule "complete Console Setup before using SDK").
- **Developer-Controlled Wallets (Entity Secret)** → `circle:use-developer-controlled-wallets`.
- **Other Circle products** (USDC, Gateway, swap, bridge...) → skill list at https://docs.arc.io/ai/skills, install via `/plugin marketplace add circlefin/skills`.
- **General Arc questions** → the `arc-docs` MCP (`docs.arc.io/mcp`), index at https://docs.arc.io/llms.txt.

## 5. Reference tools for the redesign (Step 4 section 4.3)

- **21st.dev** – https://21st.dev/ – React+Tailwind marketplace, ready-made prompts for Claude Code/Cursor/v0
- **Magic UI** – https://magicui.design/ – React+Tailwind components + animation
- **Astryx (Meta)** – https://astryx.atmeta.com/ – Meta's design system, React 19 + StyleX – a bit heavy for small apps
- **ui-ux-pro-max-skill** – https://github.com/nextlevelbuilder/ui-ux-pro-max-skill – skill that generates a design system per project
- **taste-skill** – https://github.com/Leonxlnx/taste-skill – skill against AI-generated "generic slop" UI

## 6. Git

Remote `origin` = GitHub, branch `main`. When a task is done, commit + push right away.
