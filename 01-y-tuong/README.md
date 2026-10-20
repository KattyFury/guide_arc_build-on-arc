# Bước 1: Lên ý tưởng, bàn ra chi tiết

Bước này làm trên [Claude Chat](https://claude.ai) (hoặc AI chat nào bạn quen). Mục tiêu không phải viết spec dày – Arc Studio sẽ tự lên kế hoạch ở Bước 2. Mục tiêu là **một bản brief đủ rõ** để Arc Studio hỏi đúng chỗ, không đoán bừa.

## Vì sao không đưa thẳng ý tưởng một dòng cho Arc Studio

Đưa "làm app lì xì trên Arc" thì Arc Studio vẫn build được – nhưng nó sẽ tự chọn đối tượng, tự chọn tính năng, tự chọn luồng. Ra một app chạy được mà không phải app bạn muốn.

Mười lăm phút bàn với Chat trước giúp chốt 3 thứ mà chỉ bạn trả lời được:

1. **Ai dùng, dùng lúc nào.** Phải là thứ chính mình hoặc người mình biết thật sự làm ngoài đời. Không cần giải quyết vấn đề gì to tát – thứ vui, thứ người ta thích dùng cũng tính (lì xì đâu giải quyết vấn đề gì, cả nước vẫn lì xì mỗi năm).
2. **Hơn cái đang có ở đâu.** Đã có app làm rồi thì điểm hơn của mình là gì. Không bắt buộc là công nghệ – hiểu một thói quen của người Việt mà bên nước ngoài không hiểu cũng là lợi thế.
3. **Hướng khai thác nào.** Một ý tưởng thường có 2-3 cách làm khác hẳn nhau. Bàn ra hết rồi chọn một, đừng để Arc Studio chọn hộ.

**Chưa có ý tưởng?** Arc định hướng 6 nhóm usecase trong [docs.arc.io](https://docs.arc.io): chuyển tiền P2P, thanh toán eCommerce, đổi stablecoin (FX), agent tự thanh toán, prediction market, vay/cho vay. Đó là chỗ bắt đầu nghĩ, không phải bộ lọc – có ý tưởng rồi thì khỏi so.

**Câu hỏi "Arc có làm được cái này không"** (Arc có cơ chế X không, phí thế nào...) thì hỏi AI ngay trong [docs.arc.io](https://docs.arc.io), bằng tiếng Anh, hỏi thẳng vào cơ chế. Câu nào phải thử mới biết (contract chạy không, gas thật bao nhiêu) thì **đừng tốn thời gian ở đây** – ghi vào brief, Bước 3 Arc Studio build thử là biết.

## Prompt

Copy đoạn dưới, dán vào Claude Chat:

```
Bạn là cố vấn giúp mình biến một ý tưởng thành bản brief để đưa cho Arc Studio (AI build app của Circle trên Arc network, docs.arc.io) ở chế độ Plan.

CÁCH LÀM VIỆC: Bạn DẪN, mình theo. Hỏi từng câu một, thấy mình nói chưa rõ hay chưa hợp lý thì vặn lại, đừng ngồi chờ mình nói hết. Ngắn gọn, đừng giảng.

Hỏi trước: mình có ý tưởng chưa? Chưa thì gợi ý từ 6 hướng của Arc (P2P payments, eCommerce checkout, stablecoin FX, agentic economy, prediction markets, borrow and lend) gắn với đời sống người Việt. Có rồi thì vào thẳng phần dưới.

1. ĐỐI TƯỢNG: ai dùng, dùng lúc nào, hiện họ đang làm việc này bằng cách gì. Phải là thứ có thật ngoài đời, không tưởng tượng.
2. ĐIỂM HƠN: đã có app/cách nào làm rồi chưa, mình hơn ở đâu.
3. HƯỚNG KHAI THÁC: đưa ra 2-3 cách làm khác hẳn nhau cho cùng ý tưởng (khác đối tượng, khác cơ chế, hoặc khác mức độ on-chain). Mỗi cách 2-3 dòng: hay ở đâu, khó ở đâu. Để mình chọn một, đừng chọn hộ.
4. CHI TIẾT HƯỚNG ĐÃ CHỌN: luồng chính người dùng đi (3-5 luồng), phần nào phải on-chain (chuyển USDC, smart contract, lưu dữ liệu) và phần nào không cần, cái gì KHÔNG làm ở bản demo đầu.
Gặp câu hỏi về cơ chế của Arc thì nói mình đi hỏi AI trên docs.arc.io (soạn sẵn câu hỏi tiếng Anh cho mình), đừng đoán. Câu nào phải build thử mới biết thì ghi lại, không cần trả lời.

Xong 4 phần thì viết BẢN BRIEF bằng tiếng Anh (Arc Studio làm việc tốt nhất bằng tiếng Anh), dưới 1 trang, đúng các mục:
- App name + one-line pitch
- Target users and when they use it
- Why this over existing options
- Core user flows (numbered, step by step)
- Screens (list, one line each)
- Onchain parts: what goes onchain and why (USDC transfers, contracts, data)
- Out of scope for this demo
- Open questions to verify while building
- Note: this is a testnet demo on Arc; keep it simple, mobile-first, explainable in one sentence

In bản brief trong một khối code để mình copy.
```

> Trả lời ngắn cũng được, Chat sẽ hỏi tiếp. Nó đưa 2-3 hướng thì **thật sự chọn**, đừng bảo "gộp cả hai" – gộp là cách nhanh nhất để demo đầu tiên phình ra.

## Kết quả cuối bước

Một bản brief tiếng Anh, dưới 1 trang. Đang đi theo repo bằng Claude Code thì dán bản brief vào, nó lưu thành `docs/01-brief.md` trong thư mục dự án của bạn (không phải trong repo hướng dẫn này).

Có brief rồi thì sang [Bước 2](../02-arc-studio-plan/README.md), đưa nó cho Arc Studio lên kế hoạch.
