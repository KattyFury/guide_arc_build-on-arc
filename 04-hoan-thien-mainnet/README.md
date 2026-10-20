# Bước 4: Mang về máy, hoàn thiện, lên mainnet

Arc Studio chỉ build và deploy trên **testnet** – nó không deploy mainnet thay bạn. Muốn thành sản phẩm thật thì phải mang code về máy, làm tiếp bằng Claude Code (hoặc Codex): thường là redesign giao diện, rồi đưa contract và app lên mainnet.

## 4.1. Tải dự án về máy

Hai cách, chọn một:

| Cách | Làm gì |
|---|---|
| **Export lên GitHub** (khuyên dùng) | Trong Arc Studio bấm export/push lên GitHub, rồi clone repo về máy. Có GitHub từ đầu thì khỏi lo mất code |
| **Kéo bằng CLI** | Cài CLI (mục 4.2), rồi `arc-studio apps` lấy ID app, `arc-studio pull --app <ID> --out <thư-mục>`. Sau đó tự tạo repo GitHub và push lên |

Mở terminal trong thư mục dự án, chạy `claude` (hoặc `codex`). Có `docs/` từ Bước 1-3 thì để chung trong thư mục này.

## 4.2. Cài Arc Studio CLI

Để Claude Code giao tiếp phần on-chain cho Arc Studio (viết thêm contract, audit, deploy thử lên testnet) thay vì tự mò. Cần Node.js 20 trở lên:

```bash
npm install -g @circle-fin/arc-studio-cli
arc-studio login
arc-studio whoami
```

`arc-studio login` mở trình duyệt, bạn tự bấm xác nhận.

**Claude Code:** gắn thêm skill + agent `arc-studio`:

```bash
arc-studio skills install --tool claude-code
```

Trên Windows lệnh này hay báo "Claude Code not found" dù đã cài (CLI gọi `claude` mà không tìm ra `claude.cmd`). Vá bằng cách chạy tay 2 lệnh nó định chạy:

```bash
claude plugin marketplace add "$(npm root -g)/@circle-fin/arc-studio-cli" --scope user
claude plugin install arc-studio@arc-studio-cli -y
```

Mở lại Claude Code, rồi nói kết quả muốn có chứ không nói lệnh, vd *"giao Arc Studio thêm hàm rút tiền khẩn cấp vào contract, deploy thử lên testnet, pull về contracts/"*.

**Codex:** CLI bản 1.2.1 (10/2026) chỉ gắn skill được cho Claude Code. Codex vẫn dùng được bằng lệnh nền mà skill gọi bên dưới – dặn Codex chạy:

```bash
arc-studio run "<việc cần làm>" --app <ID> --output json
arc-studio pull --app <ID> --changed
```

> Code Arc Studio viết nằm ở sandbox của nó, không phải máy bạn. Chưa `pull` về và commit lên GitHub thì coi như chưa có.

## 4.3. Redesign

Demo của Arc Studio chạy được nhưng thường nhìn na ná nhau. Đây là lúc làm giao diện cho ra sản phẩm của mình. Vẽ bằng gì cũng được: tự vẽ trên Figma, nhờ Claude Design vẽ, hay lấy một design system có sẵn.

Ba điều giúp đỡ tốn công nhất:

1. **Chốt hình ở công cụ thiết kế trước, rồi mới bắt Code dựng một lần.** Sửa trên bản vẽ là lặp rẻ; tả bằng lời cho Code sửa từng li là lặp đắt.
2. **Bản thiết kế là nguồn sự thật duy nhất.** Cái gì bản vẽ không có thì app không có – kể cả chi tiết đang nằm sẵn trong code demo. Không dặn câu này thì AI hay tự giữ lại nút, chữ gợi ý, viền cũ.
3. **Bắt AI tự chụp màn hình và đo.** Build sạch không có nghĩa là nhìn đúng – có lần nút hiện thành ô rỗng mà mọi kiểm tra tự động vẫn xanh.

Prompt cho Claude Code khi đã có bản thiết kế:

```
Dựng lại giao diện app theo bản thiết kế [link Figma / thư mục gói thiết kế]. Bản thiết kế là nguồn sự thật duy nhất: cái gì không vẽ thì bỏ, kể cả đang có trong code cũ; không tự thêm hiệu ứng, chữ gợi ý, viền, icon. Màu, font, cỡ chữ, khoảng cách gom về một chỗ định nghĩa chung, không viết thẳng trong từng màn. Không đụng vào logic và phần on-chain. Làm xong tự chạy app, chụp màn hình từng màn, đối chiếu với bản thiết kế rồi báo tôi chỗ còn lệch.
```

## 4.4. Lên mainnet

Đây là chỗ đụng **tiền thật**. Đi chậm, làm đúng thứ tự:

1. **Đọc lại contract trước khi deploy.** Code Arc Studio viết là chưa kiểm. Bảo Claude Code (hoặc giao Arc Studio audit) giải thích từng hàm bằng lời thường: ai rút được tiền, ai sửa được, có cách nào khoá tiền vĩnh viễn không. Contract giữ tiền người khác thì nên nhờ người rành xem lại.
2. **Ví deploy riêng, có ít USDC.** Gas trên Arc trả bằng USDC. Private key chỉ để trong file `.env` đã nằm trong `.gitignore` – **không bao giờ commit** (bot quét GitHub tìm key trong vài phút).
3. **Deploy contract lên Arc mainnet bằng Claude Code** – chain ID `5042`, thông số mạng ở [`ARC-RESOURCES.md`](../ARC-RESOURCES.md). Bảo nó lấy RPC, địa chỉ USDC từ docs chính thức, không lấy từ trí nhớ.
4. **Đổi app sang mainnet**: chain ID, RPC, địa chỉ contract mới, địa chỉ USDC mainnet. Gom hết vào một file cấu hình mạng, đừng rải khắp code – sau này giữ được cả bản testnet để thử.
5. **Đưa app lên host** (Cloudflare Pages, Vercel...). Secret nhập thẳng lên host. Hỏi rõ Claude Code: *"push lên GitHub có tự cập nhật web không, hay phải chạy lệnh deploy tay?"* – có lần push xong xuôi mà web vẫn y như cũ.
6. **Tự thử bằng tiền thật, số nhỏ**, rồi mới đưa người khác dùng.

Prompt giao cho Claude Code:

```
Đưa app này lên Arc mainnet. Trước khi làm gì: đọc docs chính thức của Arc (docs.arc.io) lấy chain ID, RPC, địa chỉ USDC mainnet – không dùng trí nhớ. Giải thích cho tôi từng hàm của contract bằng lời thường (ai rút được tiền, ai sửa được gì) rồi đợi tôi đồng ý. Private key chỉ để trong .env, kiểm .gitignore có .env trước khi commit. Liệt kê những việc chỉ tôi làm được (nạp USDC vào ví deploy, tạo tài khoản host, nhập secret) và dừng lại đợi. Deploy xong: tự mở link thật, đi thử luồng chính, báo tôi địa chỉ contract + link explorer, và ghi vào HANDOFF.md: push có tự deploy không.
```

## Kết quả cuối

Một link sản phẩm chạy thật trên Arc mainnet, người ngoài vào dùng được. Đưa cho người không biết gì về dự án dùng thử, ngồi nhìn họ mò – chỗ họ khựng lại là chỗ cần sửa.

## Prompt này từng hụt chỗ nào

| # | Hụt gì | Sửa thế nào |
|---|---|---|
| – | Bước mới (10/2026), **chưa chạy thật lần nào**. Chỗ hụt sẽ ghi vào đây sau lượt chạy đầu | – |

Kinh nghiệm build thật chi tiết hơn (đọc chữ ký hàm SDK trước khi gọi, sửa code nhớ sửa test, đo trước rồi mới đổ lỗi, RPC giới hạn request) nằm ở [`archive/06-build`](../archive/06-build/README.md), mục "5 thứ làm bạn chậm gấp nhiều lần".

Có link rồi thì đăng lên X, Arc House, Discord: bạn là ai, vì sao làm app này, mời mọi người dùng thử. Đừng ngại lời chê – người chê là người còn quan tâm.
