# Bước 1: Lên ý tưởng

Bước đầu tiên khi build trên Arc. Đọc phần dưới, lấy prompt paste vào AI bạn đang dùng (Claude, ChatGPT...), AI sẽ hỏi bạn từng câu để ra được một ý tưởng đủ điều kiện, kể cả khi đang chưa có gì trong đầu.

## 4 câu hỏi của một ý tưởng hợp lý

### Câu 0: Định hướng Arc

Arc là chain mới với nhiều tính năng đặc biệt. Nên khai thác những tính năng đặc biệt ấy để build app có sự khác biệt, chứ build dự án đơn thuần thì copy mã nguồn của mấy dự án đình đám lẹ hơn.

Usecase chính Arc định hướng trong [docs.arc.io](https://docs.arc.io):
- **Peer-to-peer payments** – chuyển tiền trực tiếp giữa người với người bằng stablecoin, nhanh, phí thấp, chốt giao dịch chắc chắn
- **eCommerce checkout** – cửa hàng online nhận thanh toán stablecoin, chốt nhanh, có sẵn phần tuân thủ
- **Stablecoin FX** – đổi giữa các stablecoin theo thời gian thực, giá minh bạch, phí đoán trước được
- **Agentic economy** – AI agent tự phối hợp, tự giao kèo và tự thanh toán cho nhau
- **Prediction markets** – thị trường dự đoán phi tập trung, kết quả chốt bằng oracle, giao dịch token vị thế
- **Borrow and lend** – giao thức vay/cho vay có tài sản thế chấp, vay thẳng bằng USDC

**Câu 0 chỉ là điểm bắt đầu cho người chưa có ý tưởng, không phải bộ lọc.** Chưa biết build gì thì 6 hướng này là chỗ để bắt đầu nghĩ. Có ý tưởng rồi thì **bỏ qua Câu 0, đi thẳng Câu 1** – đừng đem ý tưởng ra so với 6 gạch đầu dòng này, khớp hay không khớp đều không nói lên ý tưởng tốt hay dở. Ý tưởng có tận dụng được đặc thù kỹ thuật của Arc (USDC làm gas, finality nhanh, Memo, gas sponsorship...) hay không thì để Câu 3 soi, không phải ở đây.

> Danh sách này đổi theo docs. Lúc series mới viết, docs.arc.io chỉ có 4 hướng đầu – 2 hướng sau (Prediction markets, Borrow and lend) được Arc thêm vào sau. Trước khi dùng, mở docs ra xem lại một lượt cho chắc.

Một điều áp cho cả người đã có ý tưởng: ý tưởng có nhắc tới cái gì cụ thể của Arc hoặc hệ sinh thái quanh nó (tên token, cơ chế, tính năng chưa chắc đã sống) thì tra ngay lúc này – đừng để dồn tới Câu 3 mới phát hiện tiền đề sai, lúc đó đã lỡ tưởng tượng cả ý tưởng trên nền sai.

### Câu 1: Thật, và đúng đối tượng

Xác định mình đang làm cho ai, trong chính xã hội Việt Nam. Arc định hướng builder địa phương làm cho người địa phương, những thứ gần gũi như bỏ heo, chơi hụi, từ thiện, lì xì... đều biến thành app được.

**Không nhất thiết phải giải quyết một vấn đề.** Thứ vui, thứ mình thích, thứ người ta thật sự muốn dùng cũng tính. Lì xì đâu giải quyết vấn đề gì – nhưng cả nước vẫn lì xì mỗi năm. App vui mà có người dùng thì đáng build hơn app "giải quyết nỗi đau" mà chẳng ai mở lần thứ hai.

Cái không được nới: nó phải là thứ **chính mình hoặc người mình biết thật sự làm ngoài đời**. Không ngồi tưởng tượng ra một thói quen rồi build app cho cái thói quen đó.

### Câu 2: Dẫn đầu hay cạnh tranh

Ý tưởng có lead mảng này không, tức chưa ai làm? Nếu đã có dự án làm rồi, ưu điểm cạnh tranh của mình là gì. Build một DEX trong 3 tháng, sao không fork Uniswap? Thứ người khác đã làm rất tốt thì tay ngang rất khó cạnh tranh, phải chỉ ra được điểm hơn hẳn.

Ưu điểm cạnh tranh **không bắt buộc phải là công nghệ**. Hiểu một thói quen của người Việt mà công ty nước ngoài không hiểu cũng là một lợi thế, đôi khi còn khó copy hơn.

### Câu 3: Khả thi

Nhiều ý tưởng AI đưa ra nghe hay nhưng không làm được, hoặc quá khó với team nhỏ. Cách chắc ăn: soạn một câu hỏi feasibility rồi vào [docs.arc.io](https://docs.arc.io), mở khung chat AI trong đó mà hỏi.

**Đây không phải một bước làm một lần rồi xong.** Ý tưởng ở Bước 1 mới là bản thô – Bước 2, 3 sẽ khui ra thêm chi tiết kỹ thuật cụ thể (dùng SDK nào, cơ chế ví nào...), app có thể dùng nhiều cơ chế Arc khác nhau chứ không chỉ một. Hễ lúc nào chốt phải dùng một cơ chế cụ thể của Arc, tra docs.arc.io ngay lúc đó, đừng đợi dồn lại. Câu 3 ở đây là cửa **tối thiểu** trước khi qua Bước 2 – xác nhận hướng đi lớn có khả thi không, không phải xác nhận hết mọi chi tiết sẽ gặp về sau.

Cũng cần tách rõ nguồn tra cứu: câu hỏi thuộc **cơ chế của Arc** (SDK, kiến trúc on-chain, tốc độ, phí, tính năng còn sống hay chưa) thì hỏi docs.arc.io. Câu hỏi **không thuộc Arc** (tokenomics/roadmap của dự án hay token khác, tính năng của bên thứ ba) thì tự search web riêng – ép AI của docs.arc.io trả lời ngoài phạm vi của nó, nó sẽ đoán bừa chứ không biết thật.

**Câu nào phải thử thật mới biết thì đừng thử ở đây.** Kiểu: contract này viết được không, gas thật bao nhiêu, cơ chế A ghép với B có chạy không. Docs chỉ trả lời được "có không, hoạt động thế nào" – phần còn lại ghi thành một danh sách **"cần thử khi build"** rồi mang theo. Bước 3 gom nó vào mục "Cần kiểm tra khi build" của spec, tới Bước 6 Claude Code giao cho Arc Studio (AI coding agent của Circle, deploy thử được lên Arc testnet) đo thật qua CLI.

| Loại câu hỏi | Làm ở đâu |
|---|---|
| Arc có cái này không, nó hoạt động thế nào | AI của docs.arc.io – ngay bây giờ |
| Phải thử mới biết: gas thật, contract chạy không, A ghép B có được không | Ghi vào danh sách "cần thử khi build" → Bước 6, Arc Studio |
| Không thuộc Arc | Tự search web |

> Vì sao không thử luôn bằng Arc Studio ở bước này: một lượt deploy thử mất 5-20 phút, trong khi ý tưởng ở Bước 1 còn đổi liên tục – thử xong có khi Bước 2 đã bỏ luôn tính năng đó. Ở Bước 6, Claude Code gọi Arc Studio qua CLI ngay trong thư mục dự án, có sẵn spec làm ngữ cảnh, kết quả kéo thẳng về repo – nhanh và đáng tiền hơn nhiều so với mở web studio.arc.io ra chat tay.

Ba điều quyết định câu trả lời có xài được hay không:

1. **Hỏi bằng tiếng Anh.** AI của docs trả lời chính xác và đầy đủ hơn hẳn khi hỏi bằng đúng ngôn ngữ của tài liệu.
2. **Đừng hỏi hời hợt.** "Arc có hỗ trợ X không?" thì nhận lại câu trả lời chung chung đúng bằng câu hỏi. Hỏi thẳng vào cơ chế: tên SDK, tên kiến trúc (account abstraction, Paymaster, gas sponsorship), con số cụ thể.
3. **Nó liệt kê 2-3 lựa chọn thì đừng nhận cả hai.** Câu trả lời hay có kiểu "bạn dùng A hoặc B đều được". Đem từng cái đối chiếu ngược lại yêu cầu gốc của mình để loại – hai thứ cùng khả thi trên giấy vẫn có thể xung khắc với thứ mình cần.

Và nhớ hỏi luôn **cái gì KHÔNG có sẵn**. Biết trước phải tự build phần nào đáng giá ngang với biết phần nào có sẵn.

## Prompt để AI guide bạn từ đầu

Copy đoạn dưới, paste vào AI bạn đang dùng:

```
Bạn là cố vấn giúp mình lên ý tưởng build app trên Arc network (docs.arc.io).

CÁCH LÀM VIỆC – quan trọng nhất, đọc kỹ:
Bạn DẪN, mình theo. Ở mỗi câu, bạn chủ động đặt câu hỏi thách thức, chỉ ra chỗ mình nói chưa hợp lý, ép mình làm rõ hơn. ĐỪNG ngồi đợi mình nói hết rồi mới góp ý – mình đến đây để được dẫn, không phải để tự dẫn bạn đi theo mình. Chưa hài lòng với câu trả lời của mình thì hỏi tiếp, đừng cho qua.

Đi từng câu một, xong câu này mới sang câu sau.

Hỏi trước: Bạn có ý tưởng chưa, hay còn chưa biết build gì? Có rồi thì BỎ QUA câu 0, vào thẳng câu 1 mà vặn ý tưởng đó. Chưa có thì bắt đầu từ câu 0.
Dù có hay chưa: nếu ý tưởng nhắc tới cái gì cụ thể của Arc hoặc hệ sinh thái quanh nó (tên token, cơ chế, tính năng chưa chắc đã sống) – tra nhanh ngay bây giờ, đừng để dồn tới câu 3 mới phát hiện tiền đề sai.

CÂU 0: Định hướng Arc (CHỈ khi mình chưa có ý tưởng)
Gợi ý 6 định hướng Arc: Peer-to-peer payments, eCommerce checkout, Stablecoin FX, Agentic economy, Prediction markets, Borrow and lend – đây là điểm bắt đầu để gợi hướng cho người chưa có ý tưởng, KHÔNG phải bộ lọc. Mình đã có ý tưởng thì không đem nó ra so với 6 hướng này, không hỏi "ý tưởng thuộc hướng nào", không loại hay ép pivot vì không khớp. Chuyện ý tưởng có dùng được đặc thù kỹ thuật của Arc hay không thì để câu 3 soi.

CÂU 1: Thật, và đúng đối tượng
Xác định mình làm cho ai, trong chính xã hội Việt Nam. Arc định hướng builder địa phương làm cho người địa phương. KHÔNG bắt buộc phải giải quyết một vấn đề – thứ vui, thứ người ta thật sự muốn dùng cũng tính. Nhưng nó phải là thứ mình hoặc người mình biết THẬT SỰ làm ngoài đời, không tưởng tượng ra. Hỏi thêm: yêu cầu quan trọng nhất của sản phẩm này là gì (nhanh? rẻ? riêng tư? vui?) – câu này sẽ dùng lại ở câu 3 để loại phương án.

CÂU 2: Dẫn đầu hay cạnh tranh
Ý tưởng có lead mảng này không? Nếu đã có dự án làm rồi, ưu điểm cạnh tranh là gì? Nhắc mình: ưu điểm KHÔNG bắt buộc phải là công nghệ, hiểu văn hoá/thói quen bản địa cũng là lợi thế.

CÂU 3: Khả thi (cửa tối thiểu trước khi qua Bước 2, không phải lần kiểm duy nhất)
Chỉ ra ý tưởng dùng tới đặc thù kỹ thuật nào của Arc (USDC làm gas, finality nhanh, Memo, gas sponsorship...). Đây là chỗ soi chuyện "có đáng build trên Arc không", không phải câu 0.
Trước khi soạn câu hỏi, tách rõ 2 loại thắc mắc: cái gì thuộc CƠ CHẾ CỦA ARC (SDK, kiến trúc on-chain, tốc độ, phí, tính năng còn sống hay chưa) thì hỏi docs.arc.io. Câu nào docs không trả lời chắc được, phải thử thật trên testnet mới biết (gas thật, contract có chạy không, cơ chế A ghép B có được không) thì KHÔNG thử ở bước này – ghi vào danh sách "CẦN THỬ KHI BUILD", để Bước 6 giao Arc Studio đo. Cái gì KHÔNG thuộc Arc (tokenomics/roadmap của dự án hay token khác, tính năng bên thứ ba) thì bảo mình tự search web riêng – đừng ép docs.arc.io trả lời ngoài phạm vi của nó.

Chốt được ý tưởng rồi, soạn 1 câu hỏi feasibility cho phần thuộc Arc, đưa ra thành khối riêng để dễ copy. Bắt buộc:
- Viết câu hỏi BẰNG TIẾNG ANH (AI của docs trả lời chính xác hơn).
- Hỏi thẳng vào cơ chế kỹ thuật cụ thể: tên SDK, tên kiến trúc (account abstraction, Paymaster, gas sponsorship...), con số (tốc độ, phí). KHÔNG hỏi chung chung kiểu "does Arc support X".
- Hỏi luôn cái gì KHÔNG có sẵn, phần nào phải tự build.
Kèm hướng dẫn: "Copy đoạn trên, vào docs.arc.io, mở khung chat AI của Docs, paste vào rồi gửi. Xong đem câu trả lời quay lại đây."
Đọc câu trả lời để đánh giá khả thi. Nếu nó đưa ra nhiều lựa chọn kiến trúc song song thì TUYỆT ĐỐI KHÔNG kết luận "cả hai đều được" – đem từng cái đối chiếu lại yêu cầu quan trọng nhất ở câu 1 để loại bớt, rồi nói rõ vì sao loại.

Nhắc mình: đây là cửa TỐI THIỂU trước khi qua Bước 2, không phải lần kiểm feasibility duy nhất của cả dự án. Bước 2, 3 sẽ khui thêm chi tiết kỹ thuật cụ thể – hễ tới lúc phải chốt dùng đúng một cơ chế nào đó của Arc, quay lại hỏi docs.arc.io ngay lúc đó, đừng đợi gộp lại review một lần.

XONG CÂU 3 THÌ TỰ ĐỘNG LÀM 2 VIỆC NÀY, ĐỪNG ĐỢI MÌNH NHẮC:
1. Tổng hợp toàn bộ thành một case study gọn (4 câu + kết luận pass/không pass + danh sách "CẦN THỬ KHI BUILD", mỗi dòng ghi rõ cần đo cái gì), định dạng markdown để mình copy đi lưu.
2. Rút ra những lỗi quy trình vừa gặp trong lúc chạy 4 câu này – chỗ nào mình bị hỏi hụt, chỗ nào suýt kết luận sai – viết thành một khối riêng.

Chỗ nào chưa hợp lý thì rèn lại cho hợp lý, xong xuôi hết mới qua Bước 2.
```
