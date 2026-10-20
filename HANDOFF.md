# HANDOFF – guide_arc_build-on-arc

> File làm việc của tác giả, không phải nội dung cho người đọc series. Mở máy mới thì đọc file này trước.
> Luật cho Claude Code nằm ở `CLAUDE.md`. File này chỉ ghi **trạng thái hiện tại** – lịch sử cũ xem `git log`, không chép lại vào đây.
> **Cập nhật:** 2026-10-20.

## 0. Repo này là gì

Series hướng dẫn build app trên Arc, viết cho người Việt không rành crypto và không có nền lập trình. Nội dung gốc là loạt bài "Build on Arc bằng Claude Code" trên X của [@0xhieuxyz](https://x.com/0xhieuxyz) – repo này là bản có nhà, vì X thì bài chết sau 48 giờ.

**Thuần hướng dẫn:** không code dự án mẫu, không mục "Ví dụ", không mục "Prompt này từng hụt chỗ nào" (gỡ hết 10-20).

- GitHub: https://github.com/KattyFury/guide_arc_build-on-arc (public)
- Local: `D:\Files\Claude\guide_arc_build-on-arc`

## 1. Đang ở đâu

Từ 10-20: 4 bước (Arc Studio có chế độ Plan nên bỏ được phần PRD/phỏng vấn ngược/chốt stack/wireframe/setup của bản cũ). Bản 6 bước cũ ở `archive/`, không cập nhật nữa.

| Bước | Thư mục | Ở đâu | Trạng thái |
|---|---|---|---|
| 1. Lên ý tưởng → brief tiếng Anh | `01-y-tuong/` | Claude Chat | Viết xong, chưa chạy thật |
| 2. Plan | `02-arc-studio-plan/` | Arc Studio | Viết xong, chưa chạy thật |
| 3. Build + demo testnet | `03-build-demo/` | Arc Studio | Viết xong, chưa chạy thật |
| 4. Hoàn thiện + mainnet | `04-hoan-thien-mainnet/` | Claude Code / Codex + Arc Studio CLI | Viết xong, chưa chạy thật |

**▶ ĐANG DỞ:** 2 lượt chạy thật đầu (Bước 1 + "Bước 2" kiểu PRD 6 câu, app tingting) đều chạy prompt CŨ trong archive – lỗi của cả 2 lượt đã áp vào prompt Bước 1 mới (lượt 2 thêm: mỗi phía phải có người thật, xác định app bán gì rồi mới chọn đối thủ, cắt tính năng phải nói rủi ro mở ra, viết giúp nửa câu, brief định nghĩa thuật ngữ). Lượt đầu (user đưa **link repo** cho Claude Chat) bị Chat lạc vào `archive/01-ideation` → chạy prompt cũ. Đã sửa 10-20: biển chặn ở README chính + đầu mọi file archive, Bước 1 dặn "dán prompt, đừng đưa link", và áp vào prompt Bước 1 mới các lỗi còn đúng (1 câu hỏi/lượt, nhãn [ĐỀ XUẤT]/[CHƯA KIỂM], hỏi giai đoạn testnet/mainnet trước, search web trước khi nói "chưa ai làm", hỏi hai đầu dòng tiền, cho bỏ docs, tự viết brief khi user nói "chốt"). **Prompt Bước 1 mới vẫn chưa chạy thật lần nào** – lượt tới phải dán đúng prompt trong `01-y-tuong`. Cuối phiên dùng prompt soát lỗi (bắt Chat liệt kê chỗ lệch prompt, mỗi dòng: luật | chuyện xảy ra | đề xuất sửa) rồi sửa thẳng prompt.

**Chưa biết (đừng bịa khi viết tiếp):** vị trí nút bật Plan trên web studio.arc.io (docs không tả UI web); link preview của Arc Studio có cho người ngoài mở không.

**Đã verify 10-20** (MCP arc-docs + npm + máy Dell): mainnet chain `5042` / testnet `5042002`, RPC + explorer như `ARC-RESOURCES.md`; 6 hướng usecase trên docs; Arc Studio có Plan, Export GitHub, chỉ deploy testnet; `@circle-fin/arc-studio-cli` bản mới nhất **1.2.1**, `skills install --tool` chỉ hỗ trợ `claude-code` (Codex dùng `arc-studio run --output json`); Windows báo "Claude Code not found" → cách vá ở Bước 4 mục 4.2.

## 2. Cách làm việc

1. Viết/sửa prompt của một bước.
2. **Chạy thử thật trước khi đăng** – với dự án thật của ai đó, hoặc chạy khô.
3. Hụt chỗ nào → sửa prompt. Xong là thôi, không ghi lại lịch sử lỗi trong bài.

## 3. Quy định viết bài

- **Tiêu chí ý tưởng:** thứ vui, thứ người ta thích dùng cũng tính (lì xì đâu giải quyết vấn đề gì). Cái không nới: phải là thứ mình hoặc người mình biết **thật sự làm ngoài đời**.
- **Giọng văn:** tiếng Việt đời thường, xưng "mình" / "anh em". Câu ngắn, không sáo. Bảng khi so sánh, blockquote cho ghi chú đáng nhớ, mỗi bước kết bằng một câu dẫn sang bước sau.
- **Dấu gạch dài: chỉ en dash `–` (U+2013), không em dash (U+2014)** trong mọi file người đọc thấy. Kiểm bằng `grep -c` phải ra 0.

## 4. Bước 4: đọc skill trước khi đụng Circle/Arc

Trước khi viết code đụng Circle Wallets hoặc Arc, **load đúng skill trước**, đừng mò docs rồi thử-sai:

- **Modular Wallets (Passkey, gasless)** → `circle:use-modular-wallets` (có bảng lỗi + rule "complete Console Setup before using SDK").
- **Developer-Controlled Wallets (Entity Secret)** → `circle:use-developer-controlled-wallets`.
- **Thứ khác của Circle** (USDC, Gateway, swap, bridge...) → danh sách skill ở https://docs.arc.io/ai/skills, cài qua `/plugin marketplace add circlefin/skills`.
- **Câu hỏi chung về Arc** → MCP `arc-docs` (`docs.arc.io/mcp`), index https://docs.arc.io/llms.txt.

## 5. Tools tham khảo cho redesign (Bước 4 mục 4.3)

- **21st.dev** – https://21st.dev/ – marketplace React+Tailwind, prompt sẵn cho Claude Code/Cursor/v0
- **Magic UI** – https://magicui.design/ – component + animation React+Tailwind
- **Astryx (Meta)** – https://astryx.atmeta.com/ – design system của Meta, React 19 + StyleX – hơi nặng cho app nhỏ
- **ui-ux-pro-max-skill** – https://github.com/nextlevelbuilder/ui-ux-pro-max-skill – skill sinh design system theo project
- **taste-skill** – https://github.com/Leonxlnx/taste-skill – skill chống AI sinh UI "generic slop"

## 6. Git

Remote `origin` = GitHub, branch `main`. Xong việc là commit + push ngay.
