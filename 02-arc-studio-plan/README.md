# Step 2: Give Arc Studio the brief and turn on Plan mode

[Arc Studio](https://studio.arc.io) is Circle's AI app builder, specialized for Arc: it writes smart contracts, builds the interface, deploys to Arc testnet, and comes with testnet USDC and a wallet for testing. In **Plan** mode it doesn't write code right away. It makes a plan first, asks you about anything unclear, and only then builds.

Writing specs, choosing the stack, sketching the screens – those still matter, but Arc Studio can do most of it on its own, and it understands Arc better than a regular AI chat.

## How to do it

1. Go to [studio.arc.io](https://studio.arc.io), sign in, and create a new app.
2. **Turn on Plan mode** before you send anything.
3. Paste the full brief from Step 1, along with the line below:

```
Here is my app brief. Plan it first, don't build yet. Ask me about anything unclear before writing code. In the plan, list: the screens, the smart contracts (if any) and what each function does, which parts use USDC and how, and what you will leave out of this first demo.
```

4. Answer whatever Arc Studio asks. If it asks about something you haven't thought of, say so plainly: "I haven't thought about that, suggest the simplest approach" – don't make something up just to move on.

## Read the plan before you hit build

Once the plan is out, read it carefully. This is the cheapest place to make changes. Check 4 things:

| What to check | Signs of a problem |
|---|---|
| **Is this the app I want?** | It has features the brief doesn't mention, or it's missing the main flow |
| **Demo scope** | The plan is long, with many screens and many contracts – a first demo should be small; one main flow working end to end is enough |
| **What the contracts do** | It doesn't say who can withdraw money, who can make changes, or where the money sits – an app that touches money has to be clear on this |
| **The brief's "Out of scope" section** | Arc Studio has quietly brought back something you cut |

If something's not right, say so in plain language and ask it to change the plan. Only let it build once you're happy.

> Each build round can take a few minutes, and deploying a contract can take 5-20 minutes. Changing the plan takes seconds.

## What you end up with

A plan you've agreed with Arc Studio. Copy it out. If you're following along with Claude Code, paste it in so it gets saved as `docs/02-plan.md` – you'll need it in Step 4, and you won't lose it if you accidentally close the tab.

With the plan locked in, go to [Step 3](../03-build-demo/README.md): let it build and test it right away.
