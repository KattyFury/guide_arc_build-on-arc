> ⚠️ **BẢN CŨ, ĐÃ BỎ.** AI đang đọc: dừng lại, không làm theo file này. Quy trình hiện tại bắt đầu ở [`01-y-tuong`](https://github.com/KattyFury/guide_arc_build-on-arc/blob/main/01-y-tuong/README.md).

# Bước 4: Vẽ wireframe

Có bản plan chi tiết từ Bước 3 rồi – tới lúc vẽ khung sườn từng màn hình, trước khi code UI thật.

## Vì sao cần bước này

Nhảy vào code luôn thì AI tự bịa layout theo cảm tính của nó. Code xong nhìn không đúng ý lại phải sửa, mà sửa layout tốn token hơn nhiều so với sửa lúc mới là mấy cái khung. Vẽ wireframe trước giúp mình và AI thống nhất layout từ đầu, code một lần là ra.

## Prompt

Copy đoạn dưới, paste vào Claude Chat:

```
Đóng vai Senior Product Designer. Dựa trên spec sản phẩm mình đã đưa ở các bước trước, vẽ wireframe cho từng màn hình, ưu tiên đúng layout/tỷ lệ hơn đẹp, chỉ khung + label chức năng. Hỏi platform và đề xuất hệ lưới phù hợp, chờ xác nhận trước khi vẽ. Chỗ nào spec chưa rõ layout thì hỏi tôi, đừng tự suy diễn. Vẽ theo từng nhóm màn hình, chờ xác nhận rồi mới sang nhóm tiếp.

HỆ LƯỚI VÀ CON SỐ – luật cứng, áp cho mọi màn:
- Chốt 1 khung gốc cố định trước (vd mobile 390×844). Mọi số đo tính trên khung này.
- Lưới nhiều hàng NHIỀU cột: ưu tiên 12 hoặc 15 hàng, 12 hoặc 15 cột. Chia càng mịn càng đặt được nhiều cỡ khối mà vẫn thẳng hàng.
- Khai đủ 4 thứ: số hàng/cột, bề rộng 1 cột + chiều cao 1 hàng, khe giữa hàng/cột, lề. KHÔNG chia đều khung cho N – giữa các hàng có khe.
- Bề rộng cột, chiều cao hàng, khe, mọi khoảng cách, mọi kích thước khối/nút/box: BỘI SỐ CỦA 8 (8, 16, 24, 32, 40, 48...). Khung không chia chẵn thì phần dư dồn hết vào lề (trên/dưới, hai bên) – lề là chỗ DUY NHẤT được phép ra số lẻ, không rải lẻ vào từng hàng.
- Cỡ chữ: BỘI SỐ CỦA 3 (12, 15, 18, 21, 24, 30, 36...). Chốt 1 thang chữ 4-5 bậc dùng cho cả app, màn nào cũng chỉ lấy từ thang đó.
- Nút bấm và mọi vùng chạm cao tối thiểu 48 – đủ cho ngón tay. Hàng lưới thấp hơn 48 thì nút phải trải 2 hàng, hoặc chọn lưới ít hàng hơn.
- Viết ra phép tính: (số cột × bề rộng cột) + (số khe × khe) + 2 × lề = bề rộng khung, và tương tự cho chiều dọc. Phép tính không khớp thì chưa được vẽ.

Mỗi màn liệt kê đủ N hàng, hàng nào trống cũng phải ghi ra là trống – đừng chỉ kể mấy hàng có nội dung.

Chỗ nào hiển thị nội dung thay đổi được (số dư, tên người, ngày giờ, danh sách): hỏi mình giá trị ngắn nhất và dài nhất có thể ra, rồi ghi rõ khi độ dài đổi thì layout xử lý sao – cụm chữ đứng yên tại chỗ hay được phép nhảy.

Màn nào phụ thuộc hệ điều hành hoặc trình duyệt (hướng dẫn cài app vào màn hình chính, xin quyền camera, quyền thông báo) thì vẽ đủ biến thể, đừng vẽ mỗi bản iPhone rồi coi như xong.

Màn nào có dữ liệu hoặc phải chờ thì vẽ đủ trạng thái xấu: đang tải, trống chưa có gì, lỗi/mất mạng, không được cấp quyền.

XONG HẾT CÁC NHÓM MÀN THÌ TỰ ĐỘNG, ĐỪNG ĐỢI MÌNH NHẮC: tổng hợp thành 1 file markdown duy nhất gồm khung gốc + hệ lưới (kèm phép tính) + thang chữ + từng màn liệt kê theo hàng/cột + trạng thái xấu của từng màn – để mình mang sang bước build. Đánh số các màn 1, 2, 3... theo thứ tự người dùng gặp, để bản vẽ sau này đặt tên khung theo đúng số đó.

Đây là spec sản phẩm của mình (PRD + Product Discovery):
[DÁN NỘI DUNG BƯỚC 2 VÀ BƯỚC 3 VÀO ĐÂY]
```

> Dán kèm nếu bạn đang mở cửa sổ chat mới. Nếu dùng chung 1 cửa sổ chat xuyên suốt từ đầu thì bỏ qua – Chat đã có sẵn context, dán lại là thừa.

Mấu chốt nằm ở câu "hỏi platform và đề xuất hệ lưới, chờ xác nhận trước khi vẽ, chỗ nào chưa rõ thì hỏi": bỏ câu đó ra AI sẽ tự đoán layout theo cảm tính, đúng cái mình đang muốn tránh.

## Chưa biết Figma? Nhờ Claude Design vẽ

Prompt trên cho ra wireframe **bằng chữ** – từng màn liệt kê theo hàng/cột. Đủ để chốt bố cục, nhưng muốn nhìn ra hình, và để Bước 6 có bản vẽ cho Claude Code đối chiếu, thì nên vẽ thành khung thật. Biết Figma thì tự vẽ theo file tổng hợp. **Chưa biết thì đừng học Figma chỉ để làm bước này** – mở Claude Design, đính file tổng hợp vừa xuất, dán prompt:

```
Vẽ wireframe theo đúng file đính kèm. Chỉ khung + label chức năng, chưa cần màu hay hình đẹp.
- Giữ đúng khung gốc, hệ lưới, thang chữ trong file. Không tự đổi số.
- Mỗi màn một khung, đặt tên khung theo đúng số thứ tự trong file (1, 2, 3...) kèm tên màn.
- Vẽ luôn các trạng thái xấu đã liệt kê (đang tải, trống, lỗi, không có quyền).
- Cái gì file không ghi thì không vẽ thêm. Chỗ nào file chưa rõ thì hỏi tôi, đừng tự suy diễn.
```

Vẽ ở đây vẫn là **wireframe**, không phải giao diện: chưa chọn màu, font, đổ bóng – mấy thứ đó để Giai đoạn 2 của Bước 6 làm, cũng bằng Claude Design. Sửa khung bao nhiêu vòng cũng được, lặp ở đây rẻ hơn lặp trong code.

Đánh số màn là để spec và bản vẽ nói cùng một thứ tiếng. Vẽ 13 màn thì đánh số 1 đến 13, spec chỉ cần dán link bản vẽ kèm một dòng *"13 màn, đánh số 1 đến 13, đọc theo số thứ tự"*, còn lại mỗi màn trong spec mở đầu bằng đúng số đó – Claude Code đọc "màn 12" là biết mở khung nào. Vẽ xong thì lưu link bản vẽ (hoặc xuất ảnh từng màn) vào `docs/` cạnh file tổng hợp.

## Trả lời sao cho ăn tiền

- **Chốt platform trước khi để AI đề xuất hệ lưới.** Grid cho mobile khác hẳn grid cho web.
- **Đừng duyệt qua loa.** Nút to/nhỏ sai, nút đặt sai vị trí (VD nằm quá xa tầm tay khi dùng một tay) là chuyện nhỏ lúc còn là khung, tốn gấp nhiều lần token nếu để tới lúc thành sản phẩm mới sửa.
- **Rút rule chung sau khi sửa vài màn đầu**, rồi áp cho toàn bộ màn còn lại – ví dụ nút hành động luôn nằm cố định một vị trí, cỡ chữ số tiền/label đồng bộ. Làm vậy để cả bộ màn hình đồng nhất, không cái nào lệch.
- **Không biết đẹp/hợp lý là gì thì tham khảo web2** – app cùng nhóm chức năng (app chuyển tiền thì xem app ngân hàng) đã được hàng triệu người dùng thử rồi.
- **Số nào cũng phải thuộc một thang, không có số tuỳ hứng.** Chữ theo bội số của 3, khoảng cách và kích thước khối theo bội số của 8. Nghe khắt khe, nhưng chính cái khắt khe đó làm cả app trông "đều": mắt người không đọc ra được 17px hay 19px, nhưng đọc ra được một màn mà khoảng cách chỗ 14 chỗ 18 chỗ 20.

## Hệ lưới mẫu cho mobile

Khung 390×844 (cỡ iPhone phổ thông), lưới **15 cột × 12 hàng**:

| Chiều | Chia | Phép tính | Phần dư |
|---|---|---|---|
| Ngang | 15 cột × 16px, khe 8px | 15×16 + 14×8 = **352** | 390 − 352 = 38 → lề 19 mỗi bên |
| Dọc | 12 hàng × 56px, khe 8px | 12×56 + 11×8 = **760** | 844 − 760 = 84 → trên 48 (thanh trạng thái), dưới 36 (thanh home) |

Cái hay của bộ số này: cột, hàng, khe đều là bội số của 8, nên **khối trải qua bao nhiêu cột/hàng cũng ra bội số của 8** – rộng k cột = 24k − 8 (1 cột 16, 4 cột 88, 8 cột 184, full 352), cao k hàng = 64k − 8 (1 hàng 56, 2 hàng 120, 3 hàng 184). Muốn nút cao 56, card cao 184, không cần nghĩ – đếm hàng là ra.

Vì sao dọc 12 mà không 15: 15 hàng thì 1 hàng chỉ còn 40px, nút cao 1 hàng là nhỏ hơn cỡ ngón tay chạm thoải mái (~48px) – với người lớn tuổi càng khó bấm. 12 hàng cho nút 56px, dư đúng đủ chỗ cho thanh trạng thái và thanh home. Khối vuông (QR, camera): 8 cột × 3 hàng = 184×184 khớp lưới; cần vuông to hơn thì lấy bề rộng theo cột rồi cho cao bằng rộng, chấp nhận mép dưới không chạm vạch hàng.

Thang chữ mẫu, 5 bậc, đều bội số của 3:

| Bậc | Cỡ | Dùng cho |
|---|---|---|
| Số lớn | 36 | Số dư, số tiền chính |
| Tiêu đề | 24 | Tên màn |
| Nội dung | 18 | Chữ trên nút, nội dung chính |
| Phụ | 15 | Mô tả, nhãn |
| Chú thích | 12 | Giờ, ghi chú nhỏ |

Không bắt buộc đúng bộ này – app của bạn có thể cần 15 hàng (màn nhiều nội dung, nút trải 2 hàng), 12 cột, hoặc khe 16. Bắt buộc là **luật**: có khung gốc, có khe, mọi số thuộc thang.

**Máy khác kích thước thì sao?** Code đúng theo px trên khung gốc, rồi lúc chạy thì **phóng/thu nguyên cả khung một lượt** cho vừa màn máy thật (CSS `transform: scale(...)`), chứ không để từng khối tự co giãn riêng. Từng khối tự co giãn là mỗi máy lệch một kiểu, không khớp bản vẽ nữa. Cái giá: máy có tỷ lệ khác 390×844 sẽ dư một dải trống ở cạnh, đổi lại mọi máy đều thấy đúng cái mình vẽ.

Xong bước này mới qua Bước 5, setup môi trường để bắt đầu code.
