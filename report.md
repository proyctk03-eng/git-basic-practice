# Báo Cáo Thực Hành Git Cơ Bản

Dưới đây là phần trả lời cho các câu hỏi tư duy và bảng tóm tắt kết quả theo yêu cầu của đề bài. Bạn có thể sử dụng nội dung này để nộp bài.

---

## Bài 1: Khởi tạo Repository và thực hiện commit đầu tiên

**Câu hỏi tư duy:** Staging area (Index) có vai trò gì mà nếu không có nó, việc commit sẽ bất tiện như thế nào?

**Trả lời:**
- **Vai trò của Staging Area:** Staging Area đóng vai trò như một "phòng chờ" (vùng đệm) nơi chứa những thay đổi mà bạn muốn đưa vào commit tiếp theo. 
- **Nếu không có nó:** Việc commit sẽ trở nên cực kỳ bất tiện vì mọi thay đổi trong thư mục làm việc (Working Directory) sẽ bị "gom chung" vào một commit duy nhất. Bạn sẽ không thể tách rời các thay đổi có ý nghĩa khác nhau (ví dụ: sửa lỗi CSS và thêm tính năng HTML) thành các commit độc lập. Điều này phá vỡ tính nguyên tắc "mỗi commit là một thay đổi có nghĩa" của Git, khiến lịch sử commit lộn xộn và khó quản lý/rollback khi có lỗi xảy ra.

*(Ảnh chụp màn hình cần nộp: Mở Terminal ở thư mục `git-basic-practice`, chạy lệnh `git status` và `git log` để chụp)*

---

## Bài 3: Di chuyển giữa các phiên bản (checkout/reset)

**Bảng so sánh 3 loại git reset (soft / mixed / hard)**

| Loại Reset | Working Directory (Thư mục làm việc) | Staging Area (Vùng đệm) | Repository (Lịch sử Commit) |
| :--- | :--- | :--- | :--- |
| **`--soft`** | Giữ nguyên mọi thay đổi | Giữ nguyên (các file vẫn ở trạng thái Staged, sẵn sàng commit lại) | Xóa commit khỏi lịch sử nhánh, di chuyển HEAD lùi lại |
| **`--mixed`** (Mặc định) | Giữ nguyên mọi thay đổi | Bị xóa sạch (các file bị đẩy về trạng thái Untracked/Modified) | Xóa commit khỏi lịch sử nhánh, di chuyển HEAD lùi lại |
| **`--hard`** | **Bị xóa sạch** (Trở về y hệt phiên bản trước đó) | **Bị xóa sạch** | Xóa commit khỏi lịch sử nhánh, di chuyển HEAD lùi lại |

**Câu hỏi tư duy:** Nếu đã push code lên GitHub cho cả team dùng, việc dùng `git reset --hard` để lùi lại commit có an toàn không? Vì sao?

**Trả lời:**
- **Không an toàn!** Việc sử dụng `git reset --hard` trên một nhánh (branch) đã được push lên GitHub (nhất là nhánh dùng chung như `main`/`master`) là cực kỳ nguy hiểm.
- **Lý do:** Khi bạn reset và dùng lệnh `git push -f` (force push) để ép thay đổi lên server, hệ thống sẽ viết đè (ghi đè) và xóa bỏ vĩnh viễn các commit đó trên remote. Nếu các thành viên khác trong team đã pull những commit đó về máy của họ và phát triển tiếp, việc bạn tự ý xóa commit gốc sẽ làm hỏng lịch sử Git của toàn bộ team (gây ra tình trạng phân nhánh cục bộ/conflict toàn diện khi người khác cố gắng pull hoặc push). Thay vào đó, trong môi trường team, nên dùng `git revert` để tạo ra một commit mới có tác dụng "đảo ngược" lại commit lỗi, giúp bảo toàn lịch sử.

---

## Bài 5: Đồng bộ remote repository (clone/pull/push)

**Câu hỏi:** `git pull` thực chất là tổ hợp của 2 lệnh nào?

**Trả lời:**
`git pull` = `git fetch` + `git merge`
- **`git fetch`**: Tải toàn bộ metadata và lịch sử commit mới nhất từ remote repository về máy local, nhưng chưa can thiệp vào mã nguồn hiện tại của bạn.
- **`git merge`**: Lấy những dữ liệu vừa fetch về để gộp (merge) thẳng vào nhánh (branch) mà bạn đang làm việc trên Working Directory.

---

## Hướng dẫn chụp ảnh minh chứng cho Bài 1, 2, 3

Vì tôi đã chạy tự động tất cả lệnh trên máy của bạn, bạn có thể thực hiện theo các bước sau để chụp ảnh nộp bài:

1. Mở terminal và trỏ vào thư mục `C:\Users\dathao\Downloads\AI\git-basic-practice`.
2. Chạy `git status` -> chụp ảnh (thấy `notes.txt` chưa được add).
3. Chạy `git log --oneline` -> chụp ảnh (thấy 4 commit của Bài 2).
4. Chạy `git diff HEAD~1` hoặc `git show HEAD` -> chụp ảnh (thấy khác biệt của file CSS, notes.txt).
5. Trỏ terminal vào thư mục `C:\Users\dathao\Downloads\AI\git-final-practice`, chạy `git log --oneline` để chụp minh chứng Bài 6.
