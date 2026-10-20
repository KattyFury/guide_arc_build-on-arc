# Bước 6: Build

Khâu chuẩn bị xong rồi. Đang có 2 file spec – một về tính năng (Bước 3), một về giao diện (Bước 4). Bước này ném cả hai vào folder dự án và bắt đầu build thật.

## Vì sao chia 3 giai đoạn

Lỗi hay gặp nhất: build xong một màn hình là dành thời gian chăm chút giao diện cho đẹp luôn, rồi mới qua màn tiếp theo. Đến khi phát hiện logic sai hoặc cần đổi flow, phải sửa từ đầu – phần giao diện đã tốn công trước đó gần như bỏ đi, lãng phí token.

Cách tránh: tách hẳn 3 giai đoạn, xong hẳn cái này mới sang cái kia.

| Giai đoạn | Làm gì | Công cụ |
|---|---|---|
| **1 – Logic & flow** | UI để mộc, không cần đẹp. Build từng tính năng theo đúng thứ tự spec, xong cái nào test cái đó | Claude Code |
| **2 – Giao diện** | Chốt hình hài app trên công cụ design trước, rồi mới bắt Code dựng lại | **Claude Design** → Claude Code |
| **3 – Live & sửa theo người dùng** | Đưa sản phẩm cho người thật xài, sửa dần tới khi không ai chê được nữa | Claude Code |

Lý do tách Giai đoạn 2 ra thành một vòng riêng: **sửa giao diện bằng cách tả bằng lời cho Claude Code là cách đắt nhất.** Mỗi lần "nút này dịch xuống tí", "màu này nhạt quá" là một vòng sửa code – chạy lại – chụp màn hình – nhìn – chưa ưng – sửa tiếp. Chốt hình hài ở công cụ design trước, khi nào nhìn đã mắt rồi mới đưa sang Code dựng một lần.

---

## Giai đoạn 1 – Logic và flow

Các file spec từ Bước 1-4 đã nằm sẵn trong `docs/` của folder dự án (đi tay thì copy chúng vào đó). Mở terminal **ngay trong folder dự án**, chạy `claude` để mở Claude Code, dán prompt dưới.

```
Đọc toàn bộ folder dự án [tên dự án của bạn] trước khi build. Spec có link bản vẽ (Figma, Claude Design) thì mở bản vẽ ra đọc luôn; màn nào spec đánh số thì đối chiếu với đúng khung mang số đó.

TRƯỚC KHI VIẾT DÒNG CODE ĐẦU TIÊN – kiểm những chỗ spec chưa chắc:
Tìm trong spec mục "Cần kiểm tra khi build" (hoặc bất cứ chỗ nào ghi "ước tính", "chưa rõ", "cần đo lại", "cần chốt"). Kiểm từng dòng bằng cách thật: đo trên testnet, tra docs chính thức, gọi thử API – không trả lời bằng trí nhớ. Báo tôi kết quả từng dòng kèm bằng chứng (con số đo được, link docs, output lệnh). Dòng nào cần đo thật trên Arc testnet (phí gas, giới hạn dung lượng, contract có chạy không) mà máy đã cài Arc Studio CLI thì giao cho Arc Studio deploy một contract thử rồi đo – lấy số đo, địa chỉ contract và link explorer từ kết quả nó trả về, không tự bịa. Dòng nào ra khác với spec thì dừng lại để tôi sửa spec trước, đừng tự chọn cách khác rồi code luôn. Mục "Để sau" trong spec là thứ KHÔNG build ở bản này.

GIAI ĐOẠN 1 – Logic và flow
Build từng tính năng một theo đúng thứ tự trong file spec tính năng. Với mỗi tính năng, code logic và flow trước, gồm xử lý dữ liệu, điều hướng giữa màn hình, validate, xử lý lỗi đúng theo spec. UI lúc này để mộc, chưa cần đẹp, chỉ cần đủ để test được flow. Sau khi xong 1 tính năng, dừng lại báo tôi test, đợi tôi xác nhận OK rồi mới qua tính năng tiếp theo. Không tự thêm tính năng ngoài spec.

Chưa làm giao diện. Chỉ khi tất cả tính năng trong spec đã được tôi xác nhận chạy đúng logic thì dừng lại báo tôi, tôi sẽ tự chuyển qua giai đoạn 2.

Trước khi bắt đầu, xác nhận lại với tôi bạn hiểu thứ tự build các tính năng là gì dựa theo spec.
```

Claude Code sẽ kiểm mục "cần kiểm tra" trước, rồi đọc spec, liệt kê lại thứ tự tính năng sắp build, đợi xác nhận rồi mới bắt đầu.

**Vì sao phải kiểm trước khi code:** spec nào cũng có những câu viết lúc chưa chắc. Vd một app nhật ký ảnh (mỗi ảnh một NFT trên Arc) ghi thẳng phí gas mint + memo là *"ước tính từ gas limit, chưa phải số công bố chính thức"*, chưa biết Memo chứa được bao nhiêu chữ, chưa biết The Graph có hỗ trợ Arc không – và gom hết vào một mục riêng. Không bắt kiểm trước thì AI code luôn trên giả định đó. Có chỗ sai là sửa được, có chỗ sai là mất luôn: caption gửi qua Memo nằm **công khai, vĩnh viễn** trên chain, quên mã hoá thì caption của người dùng đầu tiên đã lộ, không có nút xoá. Spec chưa có mục này thì quay lại Vòng 2 Bước 3 lấy (file stack giờ có sẵn mục đó). Xong tính năng đầu tiên, nó dừng lại chờ mở app test flow – mọi thứ đúng thì gõ "OK" để nó tiếp tục.

### Giao phần on-chain cho Arc Studio

[Arc Studio](https://docs.arc.io/ai/arc-studio) là AI coding agent của Circle, chuyên về Arc: viết contract Solidity, compile, deploy lên Arc testnet, chạy giao dịch thật trong sandbox của nó. Claude Code giỏi việc chung, Arc Studio giỏi đúng mảng on-chain – app có contract, hoặc spec còn dòng phải đo thật trên testnet (danh sách "cần thử khi build" mang từ Bước 1), thì để Claude Code giao phần đó cho Arc Studio, khỏi bắt Claude Code tự mò.

**Dùng qua CLI ngay trong Claude Code, đừng mở web studio.arc.io ra chat tay.** Gắn CLI xong, Claude Code có thêm agent `arc-studio` – nó tự soạn việc, gửi kèm spec làm ngữ cảnh, đợi Arc Studio chạy xong rồi kéo code + số đo về thẳng thư mục dự án. Mình chỉ nói kết quả muốn có, không phải copy qua lại giữa hai cửa sổ.

Cài một lần (Bước 5 đã có, chưa cài thì chạy trong terminal – cần Node.js 20 trở lên):

```bash
npm install -g @circle-fin/arc-studio-cli
arc-studio login
arc-studio skills install --tool claude-code
```

`arc-studio login` mở trình duyệt để bạn tự bấm xác nhận. Lệnh cuối gắn Arc Studio vào Claude Code. Trên Windows, lệnh cuối hay báo "Claude Code not found" dù Claude Code đã cài (bản CLI 1.1.3 gọi `claude` mà không tìm ra `claude.cmd`). Vá bằng cách chạy tay đúng 2 lệnh nó định chạy: `claude plugin marketplace add "<thư mục npm global>/node_modules/@circle-fin/arc-studio-cli" --scope user` rồi `claude plugin install arc-studio@arc-studio-cli -y` (thư mục npm global xem bằng `npm root -g`). Mở lại Claude Code rồi nói kết quả muốn có, đừng nói lệnh:

```
Giao cho Arc Studio: viết và deploy contract [mô tả theo spec, vd "ERC-721, mỗi ảnh một token, lưu hash + con trỏ + thời điểm chụp"] lên Arc testnet. Gửi kèm file spec làm ngữ cảnh. Xong thì pull phần contracts về thư mục contracts/ của dự án này, ghi địa chỉ contract + link explorer vào HANDOFF, rồi báo tôi.
```

Chỉ cần đo một dòng trong mục "Cần kiểm tra khi build" (chưa build thật) thì nói vậy:

```
Giao cho Arc Studio đo dòng [chép dòng cần kiểm, vd "phí gas mint 1 NFT kèm Memo 200 ký tự"] trên Arc testnet: deploy contract thử tối giản, chạy đúng giao dịch đó, trả về số đo + tx hash + link explorer. Chỉ đo, chưa build app. Ghi kết quả vào mục Cần kiểm tra của spec rồi báo tôi.
```

Ba điều phải nhớ:

- **Code nằm ở sandbox của Arc Studio, không phải máy bạn.** Chưa `pull` về thư mục dự án và commit lên GitHub thì coi như chưa có. Nguồn sự thật vẫn là thư mục dự án.
- **Chỉ testnet.** Arc Studio không deploy mainnet thay bạn. Lên mainnet là việc riêng, làm sau.
- **Kết quả nó trả về chưa phải sự thật đã kiểm.** Docs của chính Arc Studio ghi vậy. Địa chỉ contract thì copy từ kết quả, mở explorer xem có thật không; contract đụng tiền thì vẫn phải đọc lại, test trước khi cho người dùng thật xài.

Deploy contract có thể mất 5-20 phút – cứ để nó chạy, ngắt giữa chừng là lượt đó bị huỷ.

**Tiêu chí "xong" ở Giai đoạn 1: nút bấm đúng vị trí mong muốn + flow chạy đúng, thế là đủ.** Ngứa mắt cỡ nào cũng kệ, đừng bắt AI chỉnh màu/spacing/font lúc này.

---

## Giai đoạn 2 – Giao diện

Ba nhịp, đi đúng thứ tự: **đóng gói → thiết kế tới khi ưng → xuất spec cho Code dựng lại.**

### 2.1. Bảo Claude Code đóng gói spec giao diện

Đừng tự ngồi mô tả app đang trông thế nào – Claude Code đang mở dự án, để nó tự đọc code rồi viết ra. Dán prompt này:

```
Đọc toàn bộ giao diện hiện tại trong dự án rồi viết ra một file spec mô tả CHÍNH XÁC những gì đang có, để tôi mang sang một AI thiết kế khác.

Yêu cầu file spec:
- Sản phẩm là gì, người dùng là ai, chạy trên khổ màn hình nào
- Toàn bộ design token đang dùng: màu, font, cỡ chữ, bo góc, đổ bóng, khoảng cách
- Hệ lưới / cách chia bố cục từng màn (khung gốc, số hàng/cột, khe, lề)
- Liệt kê riêng mọi con số KHÔNG theo luật của Bước 4 (cỡ chữ không chia hết cho 3, khoảng cách/kích thước không chia hết cho 8) – để bên thiết kế sửa cho đúng thang
- Liệt kê TỪNG màn: có gì trên đó, đặt ở đâu, chữ hiển thị chính xác là gì, bấm vào thì ra sao
- Các trạng thái: đang tải, trống, lỗi, disabled
- Ràng buộc kỹ thuật nào bắt buộc phải giữ nguyên khi đổi giao diện

Chỉ mô tả hiện trạng. Không góp ý, không đề xuất sửa, không so sánh với tài liệu cũ.
Lưu vào docs/ trong dự án và copy thêm một bản ra Desktop cho tôi dễ lấy.
```

Cái cần là **mô tả hiện trạng**, không phải bản thiết kế mơ ước – Claude Design cần biết nó đang sửa cái gì.

### 2.2. Sang Claude Design, chỉnh tới khi ưng mắt

Mở [Claude Chat](https://claude.ai), đính file spec vừa xuất, rồi bảo nó dựng lại các màn thành bản thiết kế nhìn được.

**Đây là chỗ được phép khó tính, và nên khó tính.** Cứ nói chuyện qua lại tới khi app đúng ý:

- Nút này nên nằm ở đâu, to nhỏ ra sao
- Font gì, cỡ nào, chỗ nào đậm chỗ nào nhạt
- Bảng màu, màu chính là màu gì, màu nhấn dùng vào đâu
- Khoảng cách, bo góc, đổ bóng

Nói luôn với nó luật số từ Bước 4 ngay câu đầu: *"Giữ đúng hệ lưới trong spec. Cỡ chữ chỉ dùng bội số của 3, khoảng cách và kích thước khối chỉ dùng bội số của 8."* Không nói thì nó vẽ đẹp bằng số tuỳ hứng, sang tới Code lại phải chuẩn hoá một lần nữa.

Sửa bao nhiêu vòng cũng được – ở đây nó chỉ vẽ lại, **không đụng vào code dự án**, nên sai thì sửa tiếp, không tốn gì ngoài mấy phút. Đây chính là lý do tách giai đoạn này ra: chỗ này lặp rẻ, còn lặp ở Claude Code thì đắt.

Chưa ưng thì **chưa đưa sang Code**. Nhìn còn thấy gợn ở đâu là nói tiếp ở đây.

### 2.3. Ưng rồi thì bảo Claude Design xuất spec

Khi nhìn đã thuận mắt, bảo nó đóng gói lại:

```
Thiết kế tới đây là chốt. Xuất cho tôi một gói bàn giao để đưa cho Claude Code dựng lại trong dự án thật, gồm:
- File mô tả: design token (màu, font, thang chữ bội số của 3, bo góc, đổ bóng), hệ lưới (khung gốc, số hàng/cột, khe, lề – khoảng cách bội số của 8), và từng màn có gì đặt ở đâu, ghi bằng số đo
- Bản dựng tĩnh của TẤT CẢ các màn ở đúng khổ màn hình thật, để làm bản tham chiếu
- Toàn bộ asset: logo, icon, hình
```

Gói này mang về folder dự án, rồi quay lại Claude Code:

```
Đọc gói bàn giao thiết kế trong [tên folder] rồi dựng lại toàn bộ giao diện cho đúng.

Yêu cầu:
- Gom mọi màu/font/cỡ chữ/bo góc/đổ bóng về MỘT chỗ định nghĩa duy nhất, component chỉ được dùng lại từ đó. Không viết màu hay cỡ chữ trực tiếp trong từng màn.
- Hệ lưới cũng định nghĩa một chỗ dùng chung cho các màn cùng dạng, đừng chép lại ở từng file.
- Dựng đúng px trên khung gốc của bản thiết kế (vd 390×844), rồi phóng/thu NGUYÊN khung cho vừa màn máy thật. Không để từng khối tự co giãn riêng.
- Cỡ chữ chỉ lấy từ thang chữ (bội số của 3), khoảng cách và kích thước khối chỉ là bội số của 8. Gặp số lẻ trong gói bàn giao thì hỏi tôi, đừng tự làm tròn.
- Cái gì bản thiết kế không vẽ thì KHÔNG có trong app – kể cả chi tiết đang có sẵn trong code cũ. Không tự thêm hiệu ứng, chữ gợi ý, viền, icon "cho đủ".
- Icon lấy từ đúng bộ trong gói bàn giao, không tự thay bằng icon library khác.

Làm xong thì tự chạy app, tự chụp màn hình và tự đo lại vị trí các khối, đối chiếu với bản dựng tham chiếu rồi báo tôi số đo. Đừng đoán bằng mắt.
```

**Chỗ dễ mất công nhất:** không có câu "tự chạy, tự chụp, tự đo" cuối cùng thì rất dễ nhận về một bản build *biên dịch sạch nhưng nhìn sai*. Từng có lần code pass hết kiểm tra mà nút bấm hiện ra là ô rỗng không có chữ – chỉ chụp ảnh lên mới thấy.

Chưa ưng chỗ nào thì **quay lại 2.2 sửa ở Claude Design**, đừng ngồi tả bằng lời cho Claude Code sửa vặt từng li.

---

## Giai đoạn 3 – Live rồi sửa theo người dùng

Đây mới là giai đoạn quyết định sản phẩm có ai xài không.

1. **Đưa sản phẩm lên live**, có link cho người ngoài vào được. Dán prompt này vào Claude Code:

```
Đưa app lên live để người ngoài vào dùng được, theo đúng chỗ host đã chốt trong file stack (docs/03-stack.md).

- Trước khi deploy: chạy build production thật một lần (không chỉ dev server) – build production kiểm tra chặt hơn, lỗi hay lòi ra ở đây.
- Liệt kê cho tôi những việc chỉ tôi làm được (tạo tài khoản host, đăng nhập, nhập API key/secret lên host, khai báo domain trên console của nhà cung cấp) – dừng lại đợi tôi làm xong từng việc.
- Secret nhập thẳng lên host, không commit vào code.
- Deploy xong: tự mở link thật kiểm tra trang lên được, đi thử luồng chính một lượt, báo tôi link.
- Nói rõ cho tôi: lần sau sửa code thì push lên GitHub có tự cập nhật web không, hay phải chạy lệnh deploy bằng tay? Ghi câu trả lời vào HANDOFF/MEMORY của dự án.
```

   Câu cuối cứu được một buổi: từng có lần sửa, commit, push xong xuôi mà web vẫn y như cũ – vì deploy là việc chạy tay, push không tự làm.
2. **Tự mình xài thật** như một người dùng bình thường, không phải như người viết ra nó – đi hết flow từ đầu, đừng bỏ qua bước nào vì "biết rồi".
3. **Đưa cho người khác test.** Quan trọng là người *không* biết gì về dự án. Đừng hướng dẫn trước, cứ đưa link rồi ngồi nhìn họ mò – chỗ họ khựng lại chính là chỗ sai, dù bạn thấy nó hiển nhiên.
4. **Ghi lại mọi lời chê**, kể cả lời khó nghe. "Không hiểu bấm gì tiếp" cũng là bug, ngang với app crash.
5. **Sửa dần**: lỗi hiển thị, lỗi logic, chỗ gây hiểu nhầm. Sửa xong đưa test lại.

Lặp tới khi **không ai còn chê được gì nữa** thì mới coi là xong. Không phải xong lúc code chạy được.

> Đừng ngại những góp ý khó nghe. Người dùng chê là người dùng còn quan tâm; đáng sợ hơn là họ vào, không hiểu gì, rồi đi luôn mà không nói gì cả.

---

## Trả lời sao cho ăn tiền

- **Kiên nhẫn đi từng tính năng một.** Đừng để nó gộp nhiều tính năng vào một lượt build vì "cho nhanh".
- **Xong hẳn giai đoạn này mới sang giai đoạn kia.** Logic ổn định trước thì chỉnh giao diện sau không làm gãy flow.
- **Đừng chỉnh giao diện bằng mồm ở Giai đoạn 1.** Ngứa mắt thì ghi lại, để dành xử một lượt ở Giai đoạn 2.
- **Ở Giai đoạn 2, dựng đúng px trên khung gốc rồi phóng/thu nguyên khung** – đúng hệ lưới đã chốt ở Bước 4 (chữ bội số của 3, khoảng cách/khối bội số của 8). Đừng để từng khối tự co giãn theo màn hình: làm vậy là lệch khỏi bản vẽ, mỗi máy lệch một kiểu.
- **Bắt AI tự kiểm tra bằng số đo, đừng để nó (và bạn) đoán bằng mắt.** Xem mục 2 phần dưới.
- **Build app không phải thả cho AI tự làm hết.** Có lúc phải tự tay tạo tài khoản, lấy API key, tạo database, deploy smart contract – cứ làm rồi sửa, ai cũng chật vật ở bước này.

## 5 thứ làm bạn chậm gấp nhiều lần

Rút từ build thật. Không phải vì dự án khó, mà vì 5 cái bẫy dưới đây lặp đi lặp lại. Tránh được là nhanh hơn hẳn:

1. **Không đọc chữ ký hàm thật của SDK trước khi gọi.** Một màn quan trọng (câu hỏi bảo mật) hiện RỖNG TRẮNG, chặn cả luồng tạo ví – dò nguyên nhân bằng cách đoán rồi thử-sai trên production tốn nhiều lượt vẫn sai. Root cause thật: gọi hàm SDK theo kiểu object trong khi hàm đó nhận **tham số vị trí** – đọc thẳng file `.d.ts` trong `node_modules` (30 giây) ra ngay, nhưng chỉ đọc SAU khi đã đoán mò nhiều vòng. Đụng SDK lạ, cư xử lạ: đọc chữ ký hàm thật trước, đừng đoán từ triệu chứng.
2. **Sửa giao diện mà không nhìn thấy được kết quả.** Bắt AI dựng cách tự kiểm tra trước khi sửa: chụp màn hình headless ở nhiều kích thước máy (390px và 375px – đo cả hai, vì lỗi tràn chữ chỉ lộ ra ở máy hẹp hơn), đo toạ độ từng khối bằng script chứ không đoán bằng mắt.
3. **Sửa code mà quên sửa test trong cùng lúc.** Một lần sửa thuật toán gợi ý số tiền nhưng quên đồng bộ file test tương ứng – bộ test báo đỏ suốt **9 ngày** dù app chạy đúng, vì nhìn quen thấy đỏ riết rồi bỏ qua, test mất hẳn tác dụng cảnh báo. Sửa logic ở đâu, sửa test ngay trong cùng một lượt, đừng tách ra "làm sau".
4. **Đổ lỗi cho code của mình trước khi đo.** Ba lần trong một phiên tưởng lỗi do code, hoá ra không phải: chữ tiếng Việt mất dấu khi gửi qua Telegram (do cách gọi lệnh dòng lệnh trên Windows mã hoá sai, không phải server); một tính năng đổi tiền báo lỗi "không tìm được đường" (do hạ tầng bên thứ ba hết thanh khoản test, không phải code); một lỗi tràn giao diện tưởng mới xuất hiện (kiểm bằng cách lùi lại phiên bản code cũ thì hoá ra đã tràn từ trước). Đo trước, đổ lỗi sau.
5. **Gặp giới hạn kỹ thuật thật thì né bằng cách đọc kỹ hơn, không phải đổi ẩu.** RPC công cộng giới hạn số lượng request rất chặt – phản xạ đầu là retry liên tục khi gặp lỗi, mà retry dày lại tự đâm vào chính giới hạn đó, thành vòng lặp tự giết mình. Sửa đúng: gộp nhiều lệnh đọc thành một request (Multicall), giãn cách giữa các lần thử lại, và khi chưa chắc số liệu thì hiện dấu `…` chứ không vẽ số `0` giả – vẽ `0` sai với một app tiền bạc là làm người dùng tưởng mất tiền thật.

## Kết quả cuối

Một website để người khác vào trải nghiệm thật, đã qua tay người ngoài test và đã sửa theo những gì họ chê.

## Chia sẻ sản phẩm

Đừng ngại đăng lên X, Arc House, Discord – và đừng ngại những góp ý khó nghe, feedback người dùng giúp hoàn thiện sản phẩm tốt hơn. Cấu trúc bài đăng đơn giản:

1. Giới thiệu bản thân
2. Vì sao làm dapp này, xây dựng thế nào, mất bao lâu
3. Giới thiệu sản phẩm, mời trải nghiệm

---

Series tới đây là hết. Có thể sẽ có thêm tập bonus: *1 Prompt Đưa Bạn Từ Ý Tưởng Đến Sản Phẩm Hoàn Chỉnh.*
