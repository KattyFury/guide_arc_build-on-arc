# CLAUDE.md

> How to work with me. Read this before every session.

---

## Repo này là gì

Series hướng dẫn build app trên Arc: lý thuyết, prompt copy-dán được, và kinh nghiệm thật rút
ra sau khi chạy. **Prompt chưa đem đi chạy thật thì chưa được đăng** – không nhất thiết phải
build trong repo này, chạy thử với dự án thật của ai đó (của tác giả hay người khác) là đủ, ghi
lại chỗ hụt vào mục "Prompt này từng hụt chỗ nào" của bước đó.

Repo này **thuần hướng dẫn** – không giữ code dự án mẫu, cũng không có mục ví dụ dự án mẫu
(ví dụ TapTip/EZwallet đã gỡ hết 2026-10-20 vì cũ).

---

## VAI CỦA MỖI BÊN – quy trình 4 bước (từ 2026-10-20)

| Bước | Ai làm | Claude Code (cửa sổ này) làm gì |
|---|---|---|
| **1. Ý tưởng** | User + **Claude Chat** (web) | Đọc `01-y-tuong/README.md`, đưa nguyên khối prompt, ĐỨNG CHỜ. Nhận bản brief user dán về → lưu `docs/01-brief.md` trong thư mục dự án |
| **2. Plan** | User + **Arc Studio** (web, chế độ Plan) | Đưa câu kèm brief trong `02-arc-studio-plan/README.md`, nhắc 4 điểm soi kế hoạch. Nhận kế hoạch chốt → lưu `docs/02-plan.md` |
| **3. Build + demo** | User + **Arc Studio** | Không làm hộ. Nhận link preview + địa chỉ contract + ghi chú thử → lưu `docs/03-demo.md` |
| **4. Hoàn thiện + mainnet** | **Claude Code** (hoặc Codex) trong thư mục dự án | Làm thật: tải code về, cài Arc Studio CLI, redesign, deploy mainnet theo `04-hoan-thien-mainnet/README.md` |

Một câu cho dễ nhớ: **Chat để nghĩ, Arc Studio để dựng demo, Code để giữ và để hoàn thiện.**

- **Bước 1-3 Claude Code KHÔNG trả lời hộ, KHÔNG tự viết brief, KHÔNG tự lên kế hoạch thay Arc Studio.** Chỉ đưa prompt, chờ, nhận kết quả chốt, lưu.
- **Một bước = một lần giao + một lần nhận kết quả chốt.** Không để user dán từng lượt hội thoại của Chat/Arc Studio vào đây – đó là trả tiền token cho việc chép chính tả. Thấy đoạn dở dang thì nhắc: *"Cái này chưa chốt, nói tiếp bên kia cho xong rồi mang bản cuối về."*
- **Thư mục dự án tạo ở Bước 1**, lúc lưu file đầu tiên (hỏi user đặt ở đâu – xem mục THƯ MỤC). Bước 4 code tải về (export GitHub hoặc `arc-studio pull`) để chung thư mục đó.
- **Bước 4: đọc hết `docs/` trước khi sửa dòng code đầu tiên.** Lên mainnet là đụng tiền thật: giải thích contract bằng lời thường và chờ user đồng ý trước khi deploy, lấy chain ID/RPC/địa chỉ từ docs chính thức (`ARC-RESOURCES.md` trước, rồi MCP `arc-docs`), private key chỉ trong `.env` đã gitignore.
- **Arc Studio CLI bản 1.2.1 chỉ `skills install --tool claude-code`.** Codex thì gọi `arc-studio run ... --output json` + `arc-studio pull`. Windows báo "Claude Code not found" → cách vá ở `04-hoan-thien-mainnet/README.md` mục 4.2.
- **Đích cuối là link sản phẩm chạy thật trên mainnet.** Bước 3 (demo testnet) là điểm dừng hợp lệ nếu user quyết không làm tiếp.
- Bản 6 bước cũ nằm ở `archive/` – **không còn dẫn theo nó**, chỉ trích khi user hỏi hoặc cần dẫn chứng/bài học.

---

## ⚠️ THƯ MỤC – đừng build đè vào repo hướng dẫn

Repo này không chứa code dự án nào, kể cả dự án mẫu – chỉ có `.md` hướng dẫn. Dự án của user
→ **thư mục riêng, NGOÀI repo này.** Chưa có thì hỏi user muốn đặt ở đâu rồi tạo.

Không nói rõ chỗ này thì Claude Code sẽ nhét code của người ta vào giữa mấy file README.
Đã lường trước, đừng để xảy ra.

---

## Who I Am

I'm a **Vietnamese vibecoder** – I have ideas, not a programming background. I build products by handing off to AI, not by writing every line myself.

**How I learn and work:**
- I learn by **actually building**, not from books or tutorials.
- I want to **understand while building**, not sit through a lecture first.
- I'm **decisive and push back fast** when output is off – don't guess and make me review later.
- I **plan carefully in Claude Desktop**, then hand off to Claude Code to build step by step.

**What I'm building – two directions:**

**Direction 1: Data → Predictions**  
My background is crypto research (VHG, 2023-2024). Now I do content + community ([0xhieu.xyz](https://0xhieu.xyz)). I have datasets on TGE, FDV, market conditions. I build tools that turn **data and statistics into predictions** – e.g., predict TGE FDV from fundraising + VC allocation, project scoring, market signal dashboards.

**Direction 2: Simple dapps for everyday users**  
I'm a code noob, so I don't try to build DEXs or complex AMMs. I aim for **small but useful dapps** – payment app (QuickPay), savings app (PigSave / Bỏ Heo), trading agent (Arcis). Target users are **regular people**, not DeFi degens – UX must be simple, mobile-first, explainable in one sentence.

**Stack**: Solidity + Cloudflare Workers + Cloudflare Pages  
**Chains**: Arc, Seismic, Monad (EVM-compatible)  
**AI integration**: Anthropic API (Claude)  
**GitHub**: KattyFury · **Local projects**: `D:\Files\Claude\`

---

## How to Talk to Me

- Respond in **Vietnamese**. Use English for code, technical terms, and proper nouns.
- **No filler**: skip "Great question!", "Sure!", "Certainly!".
- **Answer directly**. Short task = short answer.
- **Don't dump theory** – build first, explain when needed.
- **Don't assume I know jargon** – explain inline when using technical terms.
- **Multiple approaches → show options, don't pick silently.**
- **Not sure → say so, don't guess.**

---

## Giọng văn của series – KHÔNG ĐƯỢC SAI

- **Tiếng Việt đời thường**, xưng "mình" / "anh em" như bài gốc trên X. Câu ngắn. Không sáo.
- Bảng khi so sánh, blockquote cho ghi chú đáng nhớ, mỗi bước kết bằng một câu dẫn sang bước sau.
- **Dấu gạch dài: CHỈ dùng en dash `–` (U+2013). TUYỆT ĐỐI KHÔNG em dash `—` (U+2014).**
  Áp dụng cho mọi chữ người đọc nhìn thấy: README các bước, tài liệu, bài đăng.
- **Không có mục "Ví dụ" dự án mẫu** (gỡ 2026-10-20). Kinh nghiệm thật thì ghi vào mục
  "Prompt này từng hụt chỗ nào", không bịa tình huống.
- Sửa prompt thì **ghi lại nó từng hụt gì** ở mục "Prompt này từng hụt chỗ nào" của bước đó –
  đừng lặng lẽ sửa. Đây là phần BẮT BUỘC của mỗi bước, kể cả khi không có mục Ví dụ.
- Prompt sửa xong nên chạy thử trước khi coi là chốt (chạy thật với ai đó, hoặc tự chạy khô) –
  chỗ hụt lòi ra lúc chạy mới là thứ đáng ghi, đừng đoán chỗ hụt trên giấy.

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

## Tech Stack – chọn theo từng dự án, KHÔNG khoá cứng

Đây là series hướng dẫn, không phải một sản phẩm duy nhất — dự án của người đọc chọn stack theo cái phù hợp nhất lúc đó (ở bản 4 bước, Arc Studio đề xuất trong kế hoạch Bước 2). Đừng mặc định Cloudflare Workers/Pages chỉ vì đó là stack quen thuộc của tác giả.

- **Chains**: Arc / Seismic / Monad (EVM-compatible)
- **AI**: Anthropic API
- Backend/frontend/hosting: quyết định theo từng dự án, ghi rõ trong `HANDOFF.md` hoặc README của dự án đó.
- **Secrets**: không hardcode key trong source, bất kể dùng stack nào.

**Trước khi research Arc/Circle lại từ đầu (tốn token):** đọc `ARC-RESOURCES.md` — link docs chính thức, network params Arc Testnet, cách cài App Kit SDK. Chỉ gọi MCP `arc-docs`/`circle` khi file đó chưa đủ chi tiết.

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
