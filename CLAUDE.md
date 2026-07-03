# threads-data — hướng dẫn cho routine

## Ủy quyền thường trực (chủ repo xác nhận 2026-07-03)
- Mỗi lần chạy routine viết bài nháp: **tự động `git commit` + `git push` lên branch được chỉ định, KHÔNG cần hỏi xin phép**. Dashboard tự render từ repo sau khi push.
- **Sau khi push branch routine, tự merge vào `main` và push `main` luôn** (chủ repo đã cho phép rõ ràng — dashboard render từ `main`, chủ repo không phải làm gì thêm). Cách làm an toàn:
  1. `git fetch origin main`
  2. `git checkout -B main origin/main`
  3. `git merge <branch-routine>` — nếu conflict thì DỪNG, quay về branch routine, báo lỗi, KHÔNG force
  4. `git push origin main`
  5. `git checkout <branch-routine>`
- Vẫn KHÔNG đăng bài lên Threads, KHÔNG gọi /api/deploy, KHÔNG render thủ công.

## An toàn git (bắt buộc, không thay đổi)
- TUYỆT ĐỐI KHÔNG dùng `git add -A` hay `git add .`
- CHỈ `git add <đúng đường dẫn file mới vừa tạo>`
- Trước khi commit chạy `git status --short`: chỉ được có dòng thêm file (`A`/`??`). Nếu có bất kỳ dòng `D` (xóa) → DỪNG, không commit/push, báo lỗi.

## Cấu trúc
- Mỗi thư mục con = 1 brand: `<brand>/config.json` + `<brand>/posts/YYYY-MM-DD.json`
- Ngày bài mới = kế sau ngày mới nhất trong `<brand>/posts/`, không trùng ngày, không trùng chủ đề với ~10 bài gần nhất.
