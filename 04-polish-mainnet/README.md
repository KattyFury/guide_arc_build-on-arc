# Step 4: Bring it to your machine, polish it, go to mainnet

Arc Studio only builds and deploys on **testnet** – it won't deploy to mainnet for you. To make this a real product, you have to bring the code to your machine and continue with Claude Code (or Codex): usually redesigning the interface, then getting the contracts and app onto mainnet.

## 4.1. Download the project

Two ways, pick one:

| Method | What to do |
|---|---|
| **Export to GitHub** (recommended) | In Arc Studio, click export/push to GitHub, then clone the repo to your machine. With GitHub from the start, you won't lose your code |
| **Pull with the CLI** | Install the CLI (section 4.2), then run `arc-studio apps` to get the app ID and `arc-studio pull --app <ID> --out <folder>`. Then create a GitHub repo yourself and push to it |

Open a terminal in the project folder and run `claude` (or `codex`). If you have `docs/` from Steps 1-3, keep it in this same folder.

## 4.2. Install the Arc Studio CLI

This lets Claude Code hand the on-chain work to Arc Studio (adding contracts, audits, test deploys to testnet) instead of figuring it out alone. It requires Node.js 20 or later:

```bash
npm install -g @circle-fin/arc-studio-cli
arc-studio login
arc-studio whoami
```

`arc-studio login` opens a browser, and you click to confirm yourself.

**Claude Code:** add the `arc-studio` skill + agent:

```bash
arc-studio skills install --tool claude-code
```

On Windows this command often reports "Claude Code not found" even when it's installed (the CLI calls `claude` and can't find `claude.cmd`). Work around it by manually running the 2 commands it was going to run:

```bash
claude plugin marketplace add "$(npm root -g)/@circle-fin/arc-studio-cli" --scope user
claude plugin install arc-studio@arc-studio-cli -y
```

Reopen Claude Code, then describe the result you want instead of the commands, e.g. *"have Arc Studio add an emergency withdraw function to the contract, test deploy it to testnet, and pull it into contracts/"*.

**Codex:** CLI version 1.2.1 (October 2026) can only install the skill for Claude Code. Codex can still use the underlying commands that the skill calls – tell Codex to run:

```bash
arc-studio run "<task>" --app <ID> --output json
arc-studio pull --app <ID> --changed
```

> The code Arc Studio writes lives in its sandbox, not on your machine. If you haven't run `pull` and committed it to GitHub, consider it nonexistent.

## 4.3. Redesign

Arc Studio's demos work, but they tend to look alike. This is when you make the interface your own. Draw it with anything: draw it yourself in Figma, have Claude Design draw it, or use an existing design system.

Three things that save the most effort:

1. **Lock in the look in a design tool first, then have Code build it once.** Iterating on a design is cheap; describing every tiny tweak in words for Code to fix is expensive.
2. **The design is the single source of truth.** If it's not in the design, it's not in the app – even if it's already in the demo code. Without this instruction, the AI tends to keep old buttons, placeholder text, and borders.
3. **Make the AI take its own screenshots and measure.** A clean build doesn't mean it looks right – I once had a button render as an empty box while every automated check stayed green.

Prompt for Claude Code once you have the design:

```
Rebuild the app's interface to match the design [Figma link / design package folder]. The design is the single source of truth: anything not drawn gets removed, even if it's in the old code; don't add effects, placeholder text, borders, or icons of your own. Keep colors, fonts, font sizes, and spacing in one shared definition, not written directly in each screen. Don't touch the logic or the on-chain parts. When you're done, run the app yourself, take a screenshot of each screen, compare them against the design, and tell me where they still differ.
```

## 4.4. Go to mainnet

This is where **real money** comes in. Go slowly and do things in order:

1. **Reread the contracts before deploying.** The code Arc Studio writes is unverified. Have Claude Code explain each function in plain language (or have Arc Studio audit it): who can withdraw money, who can change things, and whether there's any way to lock the money forever. If a contract holds other people's money, get someone who knows this stuff to review it.
2. **Use a separate deploy wallet with a small amount of USDC.** Gas on Arc is paid in USDC. Keep the private key only in a `.env` file that's already in `.gitignore` – **never commit it** (bots scan GitHub and find keys within minutes).
3. **Deploy the contracts to Arc mainnet with Claude Code** – chain ID `5042`, with network parameters in [`ARC-RESOURCES.md`](../ARC-RESOURCES.md). Tell it to get the RPC and USDC address from the official docs, not from memory.
4. **Switch the app to mainnet**: chain ID, RPC, new contract addresses, mainnet USDC address. Keep them all in one network config file rather than scattered through the code – that way you can keep the testnet version for testing later.
5. **Put the app on a host** (Cloudflare Pages, Vercel...). Enter secrets directly on the host. Ask Claude Code clearly: *"does pushing to GitHub update the site automatically, or do I have to run a deploy command by hand?"* – I've pushed everything before and the site stayed exactly the same.
6. **Test it yourself with real money, in small amounts**, before letting anyone else use it.

Prompt to give Claude Code:

```
Take this app to Arc mainnet. Before doing anything: read the official Arc docs (docs.arc.io) to get the chain ID, RPC, and mainnet USDC address – don't use memory. Explain each contract function to me in plain language (who can withdraw money, who can change what), then wait for my approval. Keep the private key only in .env, and check that .gitignore includes .env before committing. List the things only I can do (funding the deploy wallet with USDC, creating the host account, entering secrets) and stop and wait. After deploying: open the real link yourself, test the main flow, report the contract addresses + explorer links to me, and record in HANDOFF.md whether pushing auto-deploys.
```

## The end result

A link to a product running for real on Arc mainnet that outsiders can use. Give it to someone who knows nothing about the project and watch them figure it out – wherever they hesitate is what needs fixing.

A few traps that slow down real builds many times over:

1. **Calling SDK functions from memory.** If the SDK behaves strangely, have Claude Code read the real function signatures in `node_modules` (the `.d.ts` files) first. Don't guess from the symptoms and then trial-and-error on the running version.
2. **Fixing the interface without seeing it.** Make the AI take its own screenshots at multiple screen sizes (390px and 375px) and measure with a script instead of eyeballing it.
3. **Changing code and forgetting the tests.** Wherever you change logic, update the tests in that same round – tests that stay red for a long time become familiar and get ignored, and then they're useless.
4. **Blaming the code before measuring.** A bug can come from third-party infrastructure, the terminal, or it may have been there all along. Measure first, blame later.
5. **Hammering retries when the RPC rate-limits you.** Batch reads (Multicall) and space out retries. When you're unsure of a number, show `…`, not `0` – in a money app, a wrong `0` makes users think they've lost their money.

Once you have a link, post it on X, Arc House, and Discord: who you are, why you made this app, and an invitation to try it. Don't be afraid of criticism – people who criticize still care.
