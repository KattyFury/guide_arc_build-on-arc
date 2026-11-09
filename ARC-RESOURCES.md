# Arc & Circle resources

> A quick reference to check before researching from scratch through MCP – it saves tokens. Links come from the `arc-docs` + `circle` MCPs, verified on 2026-08-11, with the network details + Arc Studio re-verified on 2026-10-20, not guessed. If you suspect something has changed, check through MCP again before trusting this file.

## Official docs

- **Arc Docs**: https://docs.arc.io – chain concepts, RPC, contract deployment, wallet connection, EVM differences.
- **Arc App Kit** (Bridge/Swap/Send/Unified Balance SDK): https://docs.arc.io/app-kit
- **Arc Studio** (Circle's AI app builder, released September 2026): https://studio.arc.io – has a Plan mode (plans and asks questions before building), writes/previews/deploys apps + contracts to **Arc testnet** (no mainnet deploys), exports code to GitHub. Docs: https://docs.arc.io/ai/arc-studio. CLI: `npm install -g @circle-fin/arc-studio-cli` → `arc-studio login` → `arc-studio skills install --tool claude-code` (version 1.2.1 only supports `claude-code`; other tools call `arc-studio run ... --output json`). To download an app made on the web: `arc-studio apps` → `arc-studio pull --app <ID>`. CLI docs: https://docs.arc.io/ai/arc-studio-cli (verified 2026-10-20).
- **Circle Developer Docs**: https://developers.circle.com – Wallets (dev/user-controlled, modular), CCTP, Smart Contract Platform.
- **Circle Console** (API keys, kit keys, entity secret, wallet sets): https://console.circle.com

## Network parameters

Source: https://docs.arc.io/arc/references/rpc-endpoints + /arc/references/contract-addresses (verified 2026-10-20).

| Field | Mainnet | Testnet |
|---|---|---|
| Chain ID | `5042` | `5042002` |
| RPC (HTTPS) | `https://rpc.mainnet.arc.io` | `https://rpc.testnet.arc.io` |
| Backup RPC | `https://rpc.drpc.mainnet.arc.io` (and other providers in the docs) | `https://rpc.drpc.testnet.arc.io` (and other providers in the docs) |
| Block explorer | https://explorer.arc.io | https://explorer.testnet.arc.io |
| Faucet | – | https://faucet.circle.com |
| USDC (ERC-20, 6 decimals) | `0x3600000000000000000000000000000000000000` | `0x3600000000000000000000000000000000000000` |
| Gas token | Native USDC (18 decimals on-chain – the same balance as the 6-decimal ERC-20) | same as mainnet |
| CCTP domain | `26` | `26` |

For other contracts (EURC, Memo, Multicall3, Permit2, CCTP, Gateway...), see the full table on the contract-addresses page – don't copy them from memory.

## App Kit SDK – installation

```bash
npm install @circle-fin/app-kit          # full: Bridge + Swap + Send + Unified Balance
npm install @circle-fin/bridge-kit       # bridge only
npm install @circle-fin/swap-kit         # swap only
npm install @circle-fin/unified-balance-kit
```

Add exactly 1 adapter for your stack: `@circle-fin/adapter-viem-v2`, `@circle-fin/adapter-ethers-v6`, `@circle-fin/adapter-solana-kit`, or `@circle-fin/adapter-circle-wallets` (server-side, shared with Developer-Controlled Wallets).

## Brand assets

There's no public media kit to download yet – the Arc docs say outright "contact the Arc team for logo files". Don't make up an Arc logo or icon; if one is needed, ask the user to contact the Arc team directly.

## How to use this file

Read this file before calling the `arc-docs`/`circle` MCPs to research from scratch. Only go to MCP when you need more detail than what's above (sample code for a specific quickstart, the full API reference, Circle products not listed here).
