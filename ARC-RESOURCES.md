# Tài nguyên Arc & Circle

> Tra cứu nhanh trước khi research lại từ đầu bằng MCP — đỡ tốn token. Link lấy từ MCP `arc-docs` + `circle`, verify ngày 2026-08-11, mạng + Arc Studio verify lại 2026-10-20, không phải đoán. Nếu nghi ngờ đã đổi, tra lại qua MCP trước khi tin file này.

## Docs chính thức

- **Arc Docs**: https://docs.arc.io — khái niệm chain, RPC, deploy contract, connect wallet, evm differences.
- **Arc App Kit** (SDK Bridge/Swap/Send/Unified Balance): https://docs.arc.io/app-kit
- **Arc Studio** (AI build app của Circle, ra 09/2026): https://studio.arc.io – có chế độ Plan (lên kế hoạch, hỏi lại trước khi build), viết/preview/deploy app + contract lên **Arc testnet** (không deploy mainnet), export code lên GitHub. Docs: https://docs.arc.io/ai/arc-studio. CLI: `npm install -g @circle-fin/arc-studio-cli` → `arc-studio login` → `arc-studio skills install --tool claude-code` (bản 1.2.1 chỉ hỗ trợ `claude-code`; tool khác gọi `arc-studio run ... --output json`). Tải app làm trên web về: `arc-studio apps` → `arc-studio pull --app <ID>`. Docs CLI: https://docs.arc.io/ai/arc-studio-cli (verify 2026-10-20).
- **Circle Developer Docs**: https://developers.circle.com — Wallets (dev/user-controlled, modular), CCTP, Smart Contract Platform.
- **Circle Console** (API key, kit key, entity secret, wallet sets): https://console.circle.com

## Thông số mạng

Nguồn: https://docs.arc.io/arc/references/rpc-endpoints + /arc/references/contract-addresses (verify 2026-10-20).

| Field | Mainnet | Testnet |
|---|---|---|
| Chain ID | `5042` | `5042002` |
| RPC (HTTPS) | `https://rpc.mainnet.arc.io` | `https://rpc.testnet.arc.io` |
| RPC dự phòng | `https://rpc.drpc.mainnet.arc.io` (và các bên khác trong docs) | `https://rpc.drpc.testnet.arc.io` (và các bên khác trong docs) |
| Block explorer | https://explorer.arc.io | https://explorer.testnet.arc.io |
| Faucet | – | https://faucet.circle.com |
| USDC (ERC-20, 6 decimals) | `0x3600000000000000000000000000000000000000` | `0x3600000000000000000000000000000000000000` |
| Gas token | USDC native (18 decimals on-chain – cùng một số dư với ERC-20 6 decimals) | như mainnet |
| CCTP domain | `26` | `26` |

Các contract khác (EURC, Memo, Multicall3, Permit2, CCTP, Gateway...) xem bảng đầy đủ trong trang contract-addresses – đừng chép tay từ trí nhớ.

## App Kit SDK — cài đặt

```bash
npm install @circle-fin/app-kit          # full: Bridge + Swap + Send + Unified Balance
npm install @circle-fin/bridge-kit       # chỉ bridge
npm install @circle-fin/swap-kit         # chỉ swap
npm install @circle-fin/unified-balance-kit
```

Kèm đúng 1 adapter theo stack đang dùng: `@circle-fin/adapter-viem-v2`, `@circle-fin/adapter-ethers-v6`, `@circle-fin/adapter-solana-kit`, hoặc `@circle-fin/adapter-circle-wallets` (server-side, dùng chung Developer-Controlled Wallets).

## Brand assets

Chưa có bộ media kit public để tải — docs Arc ghi thẳng "contact the Arc team for logo files". Đừng tự chế logo/icon Arc; nếu cần thì hỏi user liên hệ team Arc trực tiếp.

## Cách dùng file này

Đọc file này trước khi gọi MCP `arc-docs`/`circle` research lại từ đầu. Chỉ tra MCP khi cần chi tiết sâu hơn bảng trên (code mẫu cho 1 quickstart cụ thể, API reference đầy đủ, sản phẩm Circle chưa liệt kê ở đây).
