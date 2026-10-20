# Bước 5: Setup môi trường

Đã có 2 file spec – một về tính năng (Bước 3), một về giao diện (Bước 4). Bước này dựng môi trường để code: cài công cụ, nối GitHub, chuẩn bị để Claude Code làm việc trong đúng thư mục dự án.

## Vì sao cần bước này

Đây là chỗ nhiều người mới hay khựng lại nhất – nghe tới terminal, Node.js, Git, MCP server là thấy ngợp, không biết cài cái gì trước cái gì sau. Không cần tự mò: AI hướng dẫn từng bước một, mình chỉ chạy lệnh và dán kết quả lại.

**Đang đi theo repo này bằng Claude Code?** Vậy Node.js và Claude Code đã có sẵn trên máy rồi (không có thì bạn đã không mở được repo). Cứ bảo Claude Code *"sang Bước 5"* – nó tự chạy lệnh kiểm tra, chỉ cài phần còn thiếu, và chỉ dừng lại ở chỗ cần bạn tự tay làm (đăng nhập GitHub, tạo tài khoản). Thư mục dự án cũng đã có từ Bước 1 (chứa `docs/`), bước này chỉ nối nó với Git/GitHub.

Đi tay bằng Claude Chat thì giả định lúc bắt đầu là máy sạch, chỉ mới có Claude Desktop + gói Pro, chưa Node.js, chưa Git, chưa GitHub. **Máy bạn đã từng build project khác rồi?** Nói thẳng với AI ngay từ câu đầu – nó sẽ verify từng phần đã có thay vì bắt cài lại từ đầu.

## Prompt

Copy đoạn dưới, paste vào Claude Code (hoặc Claude Chat nếu đi tay):

```
Đóng vai mentor kỹ thuật, hướng dẫn tôi cài đặt môi trường để code cùng Claude Code trên [Windows / macOS – chọn 1]. Tôi đã có Claude Desktop và gói Pro. [Nếu máy đã build project khác rồi: "Máy tôi đã từng build project khác, có thể đã cài sẵn một số thứ trong danh sách dưới." / Nếu máy sạch trơn: "Máy tôi sạch, chưa có gì khác."]

Trước khi bắt đầu, hỏi tôi máy đã có sẵn phần nào trong danh sách dưới chưa (chạy lệnh version-check tương ứng), rồi chỉ hướng dẫn cài phần còn thiếu – đừng bắt tôi làm lại việc đã xong.

Đi từng bước một. Nếu bạn tự chạy được lệnh trên máy tôi (Claude Code) thì tự chạy, giải thích ngắn gọn lệnh đó làm gì và báo kết quả. Nếu không (Claude Chat) thì mỗi bước chỉ đưa 1 lệnh terminal, giải thích ngắn gọn, rồi đợi tôi paste kết quả vào trước khi sang bước tiếp theo. Nếu có lỗi, giúp tôi debug trước khi tiếp tục. Nếu là macOS và tôi chưa có Homebrew, hướng dẫn cài trước.

Các bước cần hoàn thành:

1. Kiểm tra/cài Node.js (bản LTS) và npm
2. Cài Claude Code qua npm
3. Đăng nhập Claude Code bằng tài khoản Pro của tôi
4. Cài Git, kiểm tra hoạt động
5. Hướng dẫn tôi tạo tài khoản GitHub (nếu chưa có) và tạo 1 repo mới
6. Folder project: nếu đã có (chứa docs/ từ các bước lên kế hoạch) thì dùng luôn, chưa có thì tạo. Init git, connect tới repo GitHub vừa tạo
7. Thêm Arc MCP server vào Claude Code (server: https://docs.arc.io/mcp)
8. Verify: hỏi Claude Code 1 câu liên quan Arc Docs để confirm MCP hoạt động
8b. Nếu app có smart contract, hoặc mục "Cần kiểm tra khi build" trong docs/03-stack.md có dòng phải đo thật trên Arc testnet: cài Arc Studio CLI để Claude Code giao phần contract cho Arc Studio – `npm install -g @circle-fin/arc-studio-cli`, rồi `arc-studio login` (mở trình duyệt, tôi tự bấm xác nhận), rồi `arc-studio skills install --tool claude-code`. Verify bằng `arc-studio whoami`. Cần Node.js 20 trở lên. Windows báo "Claude Code not found" ở lệnh skills install thì làm theo cách vá ghi ở Bước 6, mục Arc Studio.
9. Nếu project CHƯA có CLAUDE.md: tạo bằng lệnh dưới. **Nếu đã có rồi thì bỏ qua bước này** – đừng ghi đè, hỏi tôi trước nếu không chắc:

curl -o CLAUDE.md https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/CLAUDE.md

Đây là template giúp Claude Code làm việc cẩn thận hơn, bớt tự suy diễn, bớt làm phức tạp hơn cần thiết, bớt sửa lan ra ngoài phạm vi. Sau đó thêm phần riêng cho project của tôi vào cuối file (tech stack, coding style, lưu ý bảo mật...)

10. Nếu project CHƯA có file nào ghi trạng thái dự án (MEMORY.md, HANDOFF.md, hay tương đương): tạo MEMORY.md, ghi trạng thái hiện tại (đang làm gì, đã xong gì, bước tiếp theo là gì). **Nếu đã có rồi thì dùng file đó luôn, đừng tạo thêm file trùng vai trò.**

11. Đọc file chốt stack (docs/03-stack.md hoặc kết quả Vòng 2 Bước 3): cài đúng các gói trong mục "thứ cần cài", liệt kê cho tôi các tài khoản cần đăng ký và chỗ phải khai báo trước khi chạy (mục "thứ cần đăng ký" + "chỗ phải khai báo"). API key/secret chỉ để trong file môi trường (vd .env.local) đã nằm trong .gitignore – không bao giờ commit.

Sau khi xong tất cả, tóm tắt lại cho tôi những gì đã cài, và những lệnh tôi cần nhớ để mở lại môi trường này vào lần sau.
```

Trả lời khi Chat hỏi: chọn Windows hay macOS, log in cái gì thì log in cái đó, lỗi gì thì dán nguyên văn lỗi để Chat debug tiếp – đừng tự sửa rồi báo lại là "vẫn lỗi".

## Kết quả cuối bước

- Một folder dự án đã connect GitHub
- Claude Code chạy được trong folder đó, có Arc MCP để tra Arc Docs trực tiếp
- `CLAUDE.md` + `MEMORY.md` ở gốc dự án – lần sau mở lại không cần kể lại từ đầu
- Một dòng lệnh để mở lại môi trường mỗi lần sau, dạng:

```
cd "đường-dẫn-tới-project"
claude
```

