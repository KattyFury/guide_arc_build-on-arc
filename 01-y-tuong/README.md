# Bước 1: Lên ý tưởng, bàn ra chi tiết

Bước này làm trên [Claude Chat](https://claude.ai) (hoặc AI chat nào bạn quen). Mục tiêu không phải viết spec dày – Arc Studio sẽ tự lên kế hoạch ở Bước 2. Mục tiêu là **một bản brief đủ rõ** để Arc Studio hỏi đúng chỗ, không đoán bừa.

## Vì sao không đưa thẳng ý tưởng một dòng cho Arc Studio

Đưa "làm app lì xì trên Arc" thì Arc Studio vẫn build được – nhưng nó sẽ tự chọn đối tượng, tự chọn tính năng, tự chọn luồng. Ra một app chạy được mà không phải app bạn muốn.

Mười lăm phút bàn với Chat trước giúp chốt 3 thứ mà chỉ bạn trả lời được:

1. **Ai dùng, dùng lúc nào.** Phải là thứ chính mình hoặc người mình biết thật sự làm ngoài đời. Không cần giải quyết vấn đề gì to tát – thứ vui, thứ người ta thích dùng cũng tính (lì xì đâu giải quyết vấn đề gì, cả nước vẫn lì xì mỗi năm).
2. **Hơn cái đang có ở đâu.** Đã có app làm rồi thì điểm hơn của mình là gì. Không bắt buộc là công nghệ – hiểu một thói quen của người Việt mà bên nước ngoài không hiểu cũng là lợi thế.
3. **Hướng khai thác nào.** Một ý tưởng thường có 2-3 cách làm khác hẳn nhau. Bàn ra hết rồi chọn một, đừng để Arc Studio chọn hộ.

**Chưa có ý tưởng?** Arc định hướng 6 nhóm usecase trong [docs.arc.io](https://docs.arc.io): chuyển tiền P2P, thanh toán eCommerce, đổi stablecoin (FX), agent tự thanh toán, prediction market, vay/cho vay. Đó là chỗ bắt đầu nghĩ, không phải bộ lọc – có ý tưởng rồi thì khỏi so.

**Câu hỏi "Arc có làm được cái này không"** (Arc có cơ chế X không, phí thế nào...) thì hỏi AI ngay trong [docs.arc.io](https://docs.arc.io), bằng tiếng Anh, hỏi thẳng vào cơ chế. Không muốn hỏi docs cũng được – ghi vào brief, để Arc Studio trả lời lúc lên kế hoạch. Câu nào phải thử mới biết (contract chạy không, gas thật bao nhiêu) thì **đừng tốn thời gian ở đây** – ghi vào brief, Bước 3 Arc Studio build thử là biết.

**Dán prompt, đừng đưa link repo cho Chat.** Đưa link thì Chat tự đi lạc trong repo, dễ đọc nhầm bản cũ trong `archive/` rồi chạy sai quy trình.

## Prompt

Copy đoạn dưới, dán vào Claude Chat:

```
Bạn là cố vấn giúp mình biến một ý tưởng thành bản brief để đưa cho Arc Studio (AI build app của Circle trên Arc network, docs.arc.io) ở chế độ Plan.

Nguồn duy nhất là prompt này và những gì mình kể. Đừng lấy dự án hay ví dụ trong tài liệu nào khác làm ngữ cảnh hay làm đối thủ của mình.

CÁCH LÀM VIỆC:
- Bạn DẪN, mình theo. Mỗi lượt chỉ hỏi MỘT câu hỏi rồi chờ mình trả lời. Thấy mình nói chưa rõ hay chưa hợp lý thì vặn lại. Ngắn gọn, đừng giảng.
- Mỗi câu hỏi phải làm thay đổi bản brief, không thì đừng hỏi. Hỏi rồi mà mình chưa trả lời thì nhắc lại đúng 1 lần, không hỏi lại nguyên văn.
- Mình bí, bảo bạn tự quyết, hoặc chưa trả lời một chỗ thì đưa 1 đề xuất kèm lý do, gắn nhãn [ĐỀ XUẤT, chưa xác nhận]. Chỉ coi là chốt khi mình gật.
- Mình nói nửa câu mà ý đã rõ thì viết giúp bản đủ để mình sửa, đừng bắt mình viết lại.
- Mọi khẳng định về cơ chế Arc/Circle (làm được, có sẵn, phí bao nhiêu) gắn nhãn [CHƯA KIỂM]. Không viết "làm được" hay "có sẵn" khi chưa có docs hoặc bản build thử xác nhận.

Hỏi trước, từng câu một:
- Mình có ý tưởng chưa? Chưa thì gợi ý từ 6 hướng của Arc (P2P payments, eCommerce checkout, stablecoin FX, agentic economy, prediction markets, borrow and lend) gắn với đời sống người Việt.
- Đây là demo testnet, bài hackathon, hay sản phẩm mainnet thật? Câu trả lời quyết định hỏi sâu tới đâu – demo testnet thì đừng hỏi chuyện rút về ngân hàng, pháp lý, ngân sách.
- Ý tưởng có nối tiếp dự án nào mình từng làm không? Có thì để mình kể, đừng tự đoán.

1. ĐỐI TƯỢNG: ai dùng, dùng lúc nào, hiện họ đang làm việc này bằng cách gì. Phải là thứ có thật ngoài đời, không tưởng tượng. App có nhiều phía (người gửi / người nhận, người bán / người mua) thì hỏi riêng từng phía, mỗi phía phải chỉ ra được một người thật (vd "mẹ mình ở Sài Gòn"). Phía nào chưa chỉ ra được người thật thì không xây phần lõi cho phía đó.
2. ĐIỂM HƠN: hỏi trước app này BÁN cái gì cho người dùng (chuyển tiền nhanh? cảm xúc? tiết kiệm?), rồi mới chọn đối thủ cùng trục đó – app bán cảm xúc thì đối thủ không phải app chuyển tiền. Sau đó search web tìm sản phẩm cùng loại (trên Arc lẫn ngoài Arc), liệt kê ra cho mình xem TRƯỚC khi kết luận. Không được nói "chưa ai làm" khi chưa search. Rồi mới hỏi mình hơn ở đâu.
3. HƯỚNG KHAI THÁC: đưa ra 2-3 cách làm khác hẳn nhau cho cùng ý tưởng (khác đối tượng, khác cơ chế, hoặc khác mức độ on-chain). Mỗi cách 2-3 dòng: hay ở đâu, khó ở đâu. Để mình chọn một, đừng chọn hộ.
4. CHI TIẾT HƯỚNG ĐÃ CHỌN: luồng chính người dùng đi (3-5 luồng), phần nào phải on-chain (chuyển USDC, smart contract, lưu dữ liệu) và phần nào không cần, cái gì KHÔNG làm ở bản demo đầu. Mỗi lần cắt một tính năng (vd bỏ "huỷ"), nói luôn nó mở ra rủi ro gì (gõ sai địa chỉ/email là tiền vào tay người lạ) và cách vá rẻ nhất. Hỏi đủ hai đầu dòng tiền: người gửi/trả lấy USDC từ đâu và nạp thế nào; người nhận được xác thực bằng gì (link bị chuyển tiếp thì ai mở được); ai trả phí gas.

Câu hỏi về cơ chế Arc: soạn sẵn câu hỏi tiếng Anh để mình hỏi AI trên docs.arc.io. Mình không muốn hỏi docs thì thôi, đừng ép – ghi câu đó vào mục Open questions để Arc Studio trả lời lúc lên kế hoạch. Câu nào phải build thử mới biết cũng ghi vào đó, không cần trả lời ở đây.

Xong 4 phần, hoặc khi mình nói "chốt", thì TỰ viết BẢN BRIEF ngay, không đợi mình nhắc. Brief chỉ chứa những gì mình đã gật – thứ gì còn [ĐỀ XUẤT] hay [CHƯA KIỂM] thì đưa vào Open questions. Viết bằng tiếng Anh (Arc Studio làm việc tốt nhất bằng tiếng Anh), dưới 1 trang, đúng các mục:
- App name + one-line pitch
- Key terms: define in plain words what the main thing is (e.g. "a gift = an amount of USDC with a message", not a physical item), so a reader who doesn't know crypto gets it right
- Target users and when they use it
- Why this over existing options
- Core user flows (numbered, step by step)
- Screens (list, one line each)
- Onchain parts: what goes onchain and why (USDC transfers, contracts, data)
- Out of scope for this demo
- Open questions to verify while building
- Note: stage (testnet demo / hackathon / mainnet) as I answered; keep it simple, mobile-first, explainable in one sentence

In bản brief trong một khối code để mình copy, rồi nói bước tiếp theo là "Bước 2: dán brief vào Arc Studio, bật chế độ Plan".
```

> Trả lời ngắn cũng được, Chat sẽ hỏi tiếp. Nó đưa 2-3 hướng thì **thật sự chọn**, đừng bảo "gộp cả hai" – gộp là cách nhanh nhất để demo đầu tiên phình ra.

## Kết quả cuối bước

Một bản brief tiếng Anh, dưới 1 trang. Đang đi theo repo bằng Claude Code thì dán bản brief vào, nó lưu thành `docs/01-brief.md` trong thư mục dự án của bạn (không phải trong repo hướng dẫn này).

Có brief rồi thì sang [Bước 2](../02-arc-studio-plan/README.md), đưa nó cho Arc Studio lên kế hoạch.
