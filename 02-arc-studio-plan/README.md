# Bước 2: Đưa brief cho Arc Studio, bật chế độ Plan

[Arc Studio](https://studio.arc.io) là AI build app của Circle, chuyên về Arc: viết smart contract, dựng giao diện, deploy lên Arc testnet, có sẵn USDC testnet và ví để thử. Ở chế độ **Plan**, nó chưa viết code ngay mà lên kế hoạch trước, hỏi lại bạn những chỗ chưa rõ, rồi mới build.

Bước này thay cho cả cụm "viết PRD → phỏng vấn ngược → chốt stack → wireframe" của bản cũ. Không phải vì mấy việc đó hết quan trọng, mà vì Arc Studio giờ tự làm được phần lớn, và nó hiểu Arc hơn một AI chat thông thường.

## Làm thế nào

1. Vào [studio.arc.io](https://studio.arc.io), đăng nhập, tạo app mới.
2. **Bật chế độ Plan** trước khi gửi.
3. Dán nguyên bản brief của Bước 1, kèm câu dưới:

```
Here is my app brief. Plan it first, don't build yet. Ask me about anything unclear before writing code. In the plan, list: the screens, the smart contracts (if any) and what each function does, which parts use USDC and how, and what you will leave out of this first demo.
```

4. Arc Studio hỏi gì thì trả lời. Câu nào mình chưa nghĩ tới thì nói thẳng "chưa nghĩ tới, bạn đề xuất cách đơn giản nhất" – đừng bịa cho xong.

## Đọc kế hoạch trước khi bấm build

Kế hoạch ra rồi thì đọc kỹ, chỗ này sửa rẻ nhất. Soi 4 điểm:

| Soi gì | Dấu hiệu có vấn đề |
|---|---|
| **Đúng app mình muốn không** | Có tính năng brief không nhắc tới, hoặc thiếu luồng chính |
| **Phạm vi demo** | Kế hoạch dài, nhiều màn, nhiều contract – demo đầu nên nhỏ, chạy được 1 luồng chính trọn vẹn là đủ |
| **Contract làm gì** | Không nói rõ ai được rút tiền, ai được sửa, tiền nằm ở đâu – app đụng tiền thì phải rõ chỗ này |
| **Mục "Out of scope" của brief** | Arc Studio lặng lẽ đưa lại thứ mình đã gạch |

Chỗ nào không ưng thì nói lại bằng lời thường, bảo nó sửa kế hoạch. Ưng rồi mới cho build.

> Mỗi lượt build có thể mất vài phút, deploy contract có khi 5-20 phút. Sửa ở kế hoạch thì mất vài giây.

## Kết quả cuối bước

Một kế hoạch Arc Studio đã chốt với bạn. Copy kế hoạch ra, đang đi theo repo bằng Claude Code thì dán vào để nó lưu thành `docs/02-plan.md` – sau này Bước 4 sẽ cần, và để lỡ đóng tab cũng không mất.

Kế hoạch chốt rồi thì sang [Bước 3](../03-build-demo/README.md): cho build và thử luôn.
