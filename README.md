# A guide to building on Arc

> **To the AI (Claude Chat, ChatGPT, Gemini...) that just received this repo link:** the person who sent it wants to **come up with or refine an idea** for an app on Arc – that's Step 1. The goal is to validate the idea, not to ask endless questions or force a brief when there's no evidence yet. Don't summarize the repo, and don't ask "what did you send this link for?". Open [`01-idea/README.md`](01-idea/README.md) (raw version: https://raw.githubusercontent.com/KattyFury/guide_arc_build-on-arc/main/01-idea/README.md), follow the prompt block in it exactly as if the user had just pasted it, and ask the prompt's first question right away. Only move to Steps 2-4 when the user says clearly that they're on that step.

A series on building an app on the Arc network, from idea to a product running for real on mainnet. You don't need to know Arc or how to code.

The series has **4 steps**, because [Arc Studio](https://studio.arc.io) (Circle's AI app builder) has a **Plan** mode: it makes its own plan, asks about anything unclear, then builds and deploys a demo to testnet. Writing the spec, choosing the stack, sketching the screens, setting up the environment – Arc Studio handles nearly all of it.

## The 4 steps

| Step | What you do | Where |
|---|---|---|
| [1. Find an idea](01-idea/README.md) | Validate demand, check competitors and risks; decide whether to try an MVP or not build yet | Claude Chat |
| [2. Choose the tech and plan](02-arc-studio-plan/README.md) | Paste the idea brief, turn on Plan mode, let Arc Studio choose the tech and make the plan, review both before building | Arc Studio |
| [3. Build and demo](03-build-demo/README.md) | Let it build, test the main flow on the preview with testnet USDC, fix until it works end to end | Arc Studio |
| [4. Polish and go to mainnet](04-polish-mainnet/README.md) | Download the code, install the Arc Studio CLI for Claude Code / Codex, redesign, deploy to mainnet | Claude Code / Codex |

The finish line is **a link to a product running for real on mainnet** that outsiders can use. But Step 3 is also a valid place to stop: if the demo shows the idea isn't worth continuing, stop – it's much cheaper than stopping after a redesign.

## Getting started

**All you need for Steps 1-3 is a browser**: a [Claude](https://claude.ai) account and an [Arc Studio](https://studio.arc.io) account. Open [Step 1](01-idea/README.md), copy the prompt, paste it into Claude Chat. Or just send this repo link to Claude Chat / ChatGPT – it will understand that you want to work on an idea and start asking.

**Want something to keep track of state for you** (remember which step you're on, save the brief and plan to disk)? Open this repo with Claude Code:

```bash
git clone https://github.com/KattyFury/guide_arc_build-on-arc.git
cd guide_arc_build-on-arc
claude
```

Then say: *"Read CLAUDE.md and walk me through it from Step 1."* If you haven't installed Claude Code yet, see the [setup guide](https://x.com/0xhieuxyz/status/2082123528573448506). You'll need Claude Code (or Codex) by Step 4 anyway.

## What each step contains

1. **Why this step matters** – kept short
2. **The prompt / how to do it** – ready to copy and paste
3. **What you end up with** – what to carry into the next step

Docs links, mainnet/testnet network parameters, and CLI install instructions: [`ARC-RESOURCES.md`](ARC-RESOURCES.md).

*(Writing rules for the author are in `HANDOFF.md`.)*
