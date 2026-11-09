# Step 3: Build and demo right in Arc Studio

With the plan locked in, let Arc Studio build. It writes the code, deploys the contracts to Arc testnet, and runs the app in a **preview** – open it and you can click through it, with a testnet USDC faucet built in and a wallet connection for signing real transactions on testnet.

This step ends when **the main flow works end to end on the preview**. It doesn't need to look good or have every feature yet.

## Test it like a real user

Open the preview and go through the main flow from start to finish like someone using it for the first time – don't skip a step because "I already know that one":

1. Get testnet USDC from the built-in faucet and connect a wallet.
2. Do the app's main job (send money, create a room, place a bet...) and check whether the money really moves.
3. Open the transaction's explorer link and look at it. Don't just trust a "success" message on the screen.
4. Try the places that break easily: enter 0, enter decimals, click twice, cancel halfway through.

## How to fix things cheaply

- **One thing per round.** "The send button does nothing when the balance is 0" – that's one round. Don't pack 5 bugs into one message: fixing one can break another, and you won't know what caused it.
- **Describe what you see, not how to fix it.** "After I click Send the screen goes white" beats "fix the handleSend function". It's holding the code, and you're not.
- **Don't fix the interface with words at this step.** If something bugs you, write it down and save it for Step 4. Describing "move the button down a bit, make the color a bit lighter" is the most expensive way to do UI.
- **Paste errors word for word.** If there's an error message, copy it exactly and give it that. Don't retell it.

## Write things down before you leave Arc Studio

Before you go to Step 4, copy these out (or paste them to Claude Code to save in `docs/03-demo.md`):

- The preview link and the app's name on Arc Studio
- The address of each deployed contract + explorer link (copy them from Arc Studio's output, then open the explorer to confirm they're real)
- What you tested that worked, what's still broken, and what's saved for Step 4

> The results Arc Studio reports back (addresses, "deployed successfully") are **unverified** – Arc Studio's own docs say so. Open the explorer and see for yourself.

## What you end up with

A demo running on Arc testnet, with the main flow working end to end and a preview link to show off. That's enough to tell whether the idea is worth continuing – many ideas reveal here that it's time to stop, and stopping here is much cheaper than stopping after a redesign.

If the demo is solid and you want to keep going, head to [Step 4](../04-polish-mainnet/README.md): bring the code to your machine, redesign, and go to mainnet.
