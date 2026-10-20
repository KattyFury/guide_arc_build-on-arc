# Bước 3: Build và demo luôn trên Arc Studio

Kế hoạch đã chốt thì cho Arc Studio build. Nó viết code, deploy contract lên Arc testnet và chạy app trong một bản **preview** – mở ra là bấm thử được, có sẵn faucet USDC testnet và nối ví để ký giao dịch thật trên testnet.

Bước này dừng lại khi **luồng chính chạy trọn vẹn trên preview**. Chưa cần đẹp, chưa cần đủ tính năng.

## Thử như người dùng thật

Mở preview, đi hết luồng chính từ đầu tới cuối như một người lần đầu dùng – đừng bỏ bước nào vì "biết rồi":

1. Lấy USDC testnet từ faucet có sẵn, nối ví.
2. Làm đúng việc chính của app (gửi tiền, tạo phòng, đặt cược...), xem tiền có đi thật không.
3. Mở link explorer của giao dịch ra xem, đừng tin mỗi dòng "thành công" trên màn hình.
4. Thử chỗ dễ sai: nhập số 0, số lẻ, bấm 2 lần, huỷ giữa chừng.

## Sửa thế nào cho rẻ

- **Mỗi lượt một việc.** "Nút gửi không ra gì khi số dư bằng 0" – một lượt. Đừng gom 5 lỗi vào một câu, nó sửa lỗi này làm hỏng lỗi kia mà mình không biết do đâu.
- **Tả cái mình thấy, không tả cách sửa.** "Bấm Gửi xong màn hình trắng" tốt hơn "sửa hàm handleSend". Nó đang cầm code, mình thì không.
- **Đừng sửa giao diện bằng lời ở bước này.** Ngứa mắt thì ghi lại, để dành Bước 4. Tả "nút dịch xuống tí, màu nhạt tí" là cách đắt nhất để làm giao diện.
- **Dán nguyên văn lỗi.** Có thông báo lỗi thì copy nguyên văn đưa nó, đừng kể lại.

## Ghi lại trước khi rời Arc Studio

Trước khi sang Bước 4, chép ra (hoặc dán cho Claude Code lưu vào `docs/03-demo.md`):

- Link preview và tên app trên Arc Studio
- Địa chỉ từng contract đã deploy + link explorer (copy từ kết quả Arc Studio trả về, mở explorer kiểm có thật không)
- Những gì đã thử chạy được, những gì còn lỗi, những gì để dành Bước 4

> Kết quả Arc Studio báo về (địa chỉ, "deploy thành công") là **chưa kiểm** – docs của chính Arc Studio ghi vậy. Mở explorer xem tận mắt.

## Kết quả cuối bước

Một bản demo chạy trên Arc testnet, luồng chính đi trọn được, có link preview để khoe. Đủ để biết ý tưởng có đáng làm tiếp hay không – nhiều ý tưởng tới đây là biết nên dừng, và dừng ở đây rẻ hơn nhiều so với dừng sau khi đã redesign.

## Prompt này từng hụt chỗ nào

| # | Hụt gì | Sửa thế nào |
|---|---|---|
| – | Bước mới (10/2026), **chưa chạy thật lần nào**. Chỗ hụt sẽ ghi vào đây sau lượt chạy đầu | – |

Demo ổn và muốn làm tiếp thì sang [Bước 4](../04-hoan-thien-mainnet/README.md): mang code về máy, redesign, lên mainnet.
