# Hướng dẫn anh em build on Arc

Series hướng dẫn build app trên Arc network, từ ý tưởng tới sản phẩm chạy thật trên mainnet. Không cần đã rành Arc hay biết code.

Từ 10/2026 series chỉ còn **4 bước**, vì [Arc Studio](https://studio.arc.io) (AI build app của Circle) giờ có chế độ **Plan**: tự lên kế hoạch, hỏi lại chỗ chưa rõ, rồi build và deploy bản demo lên testnet. Phần nặng nhất của bản cũ (viết PRD, phỏng vấn ngược, chốt stack, wireframe, setup môi trường) giờ Arc Studio lo gần hết.

## 4 bước

| Bước | Làm gì | Ở đâu |
|---|---|---|
| [1. Lên ý tưởng](01-y-tuong/README.md) | Bàn ý tưởng ra 2-3 hướng khai thác, chọn một, viết thành bản brief | Claude Chat |
| [2. Plan với Arc Studio](02-arc-studio-plan/README.md) | Dán brief, bật chế độ Plan, trả lời câu hỏi, soi kế hoạch trước khi build | Arc Studio |
| [3. Build và demo](03-build-demo/README.md) | Cho build, thử luồng chính trên preview với USDC testnet, sửa tới khi chạy trọn | Arc Studio |
| [4. Hoàn thiện, lên mainnet](04-hoan-thien-mainnet/README.md) | Tải code về, cài Arc Studio CLI cho Claude Code / Codex, redesign, deploy lên mainnet | Claude Code / Codex |

Đích cuối là **một link sản phẩm chạy thật trên mainnet**, người ngoài vào dùng được. Nhưng Bước 3 cũng là một điểm dừng hợp lệ: demo xong thấy ý tưởng không đáng làm tiếp thì dừng – rẻ hơn nhiều so với dừng sau khi đã redesign.

## Bắt đầu

**Chỉ cần trình duyệt** cho Bước 1-3: một tài khoản [Claude](https://claude.ai) và một tài khoản [Arc Studio](https://studio.arc.io). Mở [Bước 1](01-y-tuong/README.md), copy prompt, dán vào Claude Chat.

**Muốn có người giữ hộ trạng thái** (nhớ mình đang ở bước nào, lưu brief/kế hoạch xuống đĩa) thì mở repo này bằng Claude Code:

```bash
git clone https://github.com/KattyFury/build-on-arc.git
cd build-on-arc
claude
```

Rồi nói: *"Đọc CLAUDE.md rồi dẫn tôi đi từ Bước 1."* Chưa cài Claude Code thì xem [hướng dẫn setup](https://x.com/0xhieuxyz/status/2082123528573448506). Tới Bước 4 thì đằng nào cũng cần Claude Code (hoặc Codex).

## Mỗi bước có gì

1. **Vì sao cần bước này** – ngắn thôi
2. **Prompt / cách làm** – copy dán được
3. **Kết quả cuối bước** – mang gì sang bước sau
4. **Prompt này từng hụt chỗ nào** – bản đầu sai ở đâu, sửa thế nào. Prompt được đem đi chạy thật, hụt chỗ nào ghi lại nguyên vẹn

## Bản 6 bước cũ

Quy trình 6 bước trước đây (cùng ví dụ thật của [TapTip](https://github.com/KattyFury/taptip) và [EZwallet](https://github.com/KattyFury/ezwallet)) nằm ở [`archive/`](archive/README.md). Vẫn đáng đọc khi làm app đụng nhiều tiền hoặc cần lên kế hoạch kỹ hơn những gì Arc Studio tự hỏi.

Link docs, thông số mạng mainnet/testnet, cách cài CLI: [`ARC-RESOURCES.md`](ARC-RESOURCES.md).

*(Quy định viết bài dành cho tác giả nằm ở `HANDOFF.md`.)*
