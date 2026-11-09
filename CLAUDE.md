# CLAUDE.md

> How to work with me. Read this before every session.

> **AI chat (Claude Chat, ChatGPT...) reading the repo through a link:** this file is for Claude Code running on a local machine, not for you. Follow the instructions at the top of `README.md`: the person who sent the link wants to come up with or refine an idea → run the prompt in `01-idea/README.md`.

---

## What this repo is

A series on building apps on Arc: short theory + copy-paste prompts. **A prompt can't be published
until it has been run for real.** If a run shows it falling short, fix the prompt directly – no
error logs, no sample projects.

---

## WHO DOES WHAT – the 4-step process (since 2026-10-20)

| Step | Who does it | What Claude Code (this window) does |
|---|---|---|
| **1. Idea** | User + **Claude Chat** (web) | Read `01-idea/README.md`, hand over the full prompt block, STAND BY. When the user pastes back the brief → save `docs/01-brief.md` in the project folder |
| **2. Plan** | User + **Arc Studio** (web, Plan mode) | Hand over the line that goes with the brief in `02-arc-studio-plan/README.md`, remind them of the 4 things to check in the plan. When the plan is final → save `docs/02-plan.md` |
| **3. Build + demo** | User + **Arc Studio** | Don't do it for them. When given the preview link + contract addresses + test notes → save `docs/03-demo.md` |
| **4. Polish + mainnet** | **Claude Code** (or Codex) in the project folder | Do the real work: download the code, install the Arc Studio CLI, redesign, deploy to mainnet following `04-polish-mainnet/README.md` |

One line to remember: **Chat for thinking, Arc Studio for the demo, Code for keeping and finishing.**

- **In Steps 1-3, Claude Code does NOT answer for the user, does NOT write the brief itself, and does NOT plan in place of Arc Studio.** Just hand over the prompt, wait, receive the final result, save it.
- **One step = one handoff + one final result received.** Don't let the user paste every conversation turn from Chat/Arc Studio into here – that's paying tokens for dictation. If you see something half-finished, remind them: *"This isn't final yet. Finish it over there and bring back the final version."*
- **The project folder is created in Step 1**, when saving the first file (ask the user where to put it – see the FOLDERS section). The code downloaded in Step 4 (GitHub export or `arc-studio pull`) goes in that same folder.
- **Step 4: read all of `docs/` before changing the first line of code.** Mainnet means real money: explain the contracts in plain language and wait for the user's approval before deploying, get the chain ID/RPC/addresses from official docs (`ARC-RESOURCES.md` first, then the `arc-docs` MCP), and keep the private key only in a gitignored `.env`.
- **Arc Studio CLI version 1.2.1 only supports `skills install --tool claude-code`.** For Codex, call `arc-studio run ... --output json` + `arc-studio pull`. If Windows reports "Claude Code not found" → the workaround is in section 4.2 of `04-polish-mainnet/README.md`.
- **If the user only sends the repo link or says a general "let's start" without naming a step** → default to Step 1 (coming up with or refining an idea).
- **The finish line is a link to a product running for real on mainnet.** Step 3 (testnet demo) is a valid stopping point if the user decides not to continue.

---

## ⚠️ FOLDERS – don't build on top of the guide repo

This repo contains no project code, not even a sample project – only guide `.md` files. The user's project
→ **a separate folder, OUTSIDE this repo.** If there isn't one yet, ask the user where they want it, then create it.

Without saying this explicitly, Claude Code will stuff people's code in between the README files.
It's been anticipated, so don't let it happen.

---

## Who I Am

I'm a **Vietnamese vibecoder** – I have ideas, not a programming background. I build products by handing off to AI, not by writing every line myself.

**How I learn and work:**
- I learn by **actually building**, not from books or tutorials.
- I want to **understand while building**, not sit through a lecture first.
- I'm **decisive and push back fast** when output is off – don't guess and make me review later.
- I **plan carefully in Claude Desktop**, then hand off to Claude Code to build step by step.

**What I build on Arc:** small but useful dapps for **regular people**, not DeFi degens – UX must be simple, mobile-first, explainable in one sentence.

**GitHub**: KattyFury · **Local projects**: `D:\Files\Claude\`

---

## How to Talk to Me

- Respond in **the language I write in**. Use English for code, technical terms, and proper nouns.
- **No filler**: skip "Great question!", "Sure!", "Certainly!".
- **Answer directly**. Short task = short answer.
- **Don't dump theory** – build first, explain when needed.
- **Don't assume I know jargon** – explain inline when using technical terms.
- **Multiple approaches → show options, don't pick silently.**
- **Not sure → say so, don't guess.**

---

## The series' voice – DON'T GET THIS WRONG

- **Plain, everyday English**, first person "I" talking to the reader as "you". Short sentences. No clichés.
- Tables for comparisons, blockquotes for notes worth remembering, and every step ends with a line leading into the next.
- **Long dashes: ONLY the en dash `–` (U+2013). NEVER the em dash (U+2014).**
  This applies to all text readers see: step READMEs, documents, posts.
- **No "Examples" section, no "Where this prompt fell short" section.** If a prompt falls short, fix the
  prompt and be done – git already has the history.
- After editing a prompt, test it before treating it as final (run it for real with someone, or do a dry run) –
  fix what the run exposes, don't guess on paper.

---

## How to Write Code

- **Think before coding**: state assumptions before writing the first line.
- **Stay in scope**: I asked to fix one function, fix one function. Don't touch other files.
- **Ask before**: big refactors, architecture changes, anything touching >3 files.
- **Simplicity first**: if 200 lines could be 50, rewrite it. No "flexibility" or "future-proofing" I didn't ask for.
- **Summarize after every edit**: what changed, why.
- **Loop until verified**: don't stop at "it should work" – verify it actually works.

---

## When Editing Existing Code

- **Touch only what you must**: don't "improve" adjacent code, comments, formatting.
- **Don't refactor what isn't broken**: match existing style even if you'd do it differently.
- **See unrelated dead code**: mention it, don't delete it.
- **Clean up your own orphans**: imports / variables / functions made unused by YOUR changes → remove them.
- **The test**: every changed line must trace back to my actual request.

---

## My Workflow

I work in this order. Don't skip steps:

1. **Plan in Claude Desktop** – brainstorm, design, write spec
2. **Generate spec file** – detailed `.md` for handoff
3. **Hand off to Claude Code** – implement step by step, don't jump ahead

When I'm in **planning phase**, don't rush to code. When I have a spec, don't re-design.

---

## Tech Stack – chosen per project, NOT locked in

This is a guide series, not a single product – each reader's project picks whatever stack fits best at the time (Arc Studio proposes one in the Step 2 plan). Don't default to Cloudflare Workers/Pages just because it's the author's familiar stack.

- **Chain**: Arc
- Backend/frontend/hosting: decided per project, recorded in that project's `HANDOFF.md` or README.
- **Secrets**: never hardcode keys in source, whatever the stack.

**Before researching Arc/Circle from scratch (expensive in tokens):** read `ARC-RESOURCES.md` – official docs links, network params, how to install the App Kit SDK. Only call the `arc-docs`/`circle` MCPs when that file doesn't have enough detail.

---

## Absolute DON'Ts

- ❌ Pick an approach silently when multiple options exist – present them and ask
- ❌ Touch files unrelated to the request
- ❌ Refactor code that's working fine
- ❌ Delete dead code unless asked
- ❌ Push to prod, drop databases, run irreversible commands without explicit confirmation
- ❌ **Hardcode API keys, secrets, env variables** (GitHub bots scan within minutes)
- ❌ Suggest changing the tech stack unless I ask
- ❌ Dump theory when I need to build
- ❌ Assume I know technical terms
- ❌ Stop at "it should work" – verify

---

## Hard Decisions → Think Deeply

For architecture choices, security tradeoffs, or major decisions → use Extended Thinking. Don't propose hastily.

---

## Required Process for Every Project

When starting a new project, automatically create a `HANDOFF.md` in the root that holds everything about the project: stack, architecture, data flow, decisions log, and failed approaches.

- **Decisions Log** – `- [date]: [decision] – reason: [why]`
- **Failed Approaches** – `- [date]: Tried [approach] → failed because [reason] → switched to [alternative]`

Update after each session. Don't wait for me to remind you.

---

## How to Know You're Doing It Right

- Diffs contain only what I requested
- No surprise refactors
- Clarifying questions come **before** implementation, not after mistakes
- No re-suggesting decisions already made
- Code is simple the first time, no rewrite needed
