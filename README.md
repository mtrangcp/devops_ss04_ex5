# 1. Các bước thực hiện xử lý bài tập

## Trường hợp 1: Sửa đổi cục bộ với `git reset --mixed` (hoặc mặc định)

Khi phát hiện commit gần nhất có mã nguồn bị lỗi và bạn muốn lùi lại để chỉnh sửa mã nguồn cục bộ mà không làm mất các thay đổi hiện hành:

1. Di chuyển lịch sử cục bộ lùi lại 1 commit (giữ nguyên code trong Working Directory dưới dạng Modified):

   ```bash
   git reset HEAD~1
   ```

2. Kiểm tra trạng thái để xác nhận các tệp tin thay đổi đang nằm ở vùng Working Directory:

```bash
git status

```

## Trường hợp 2: Sửa đổi công cộng với `git revert`

Khi mã nguồn lỗi đã được đẩy lên nhánh chung (remote repository) và việc dùng `reset` có thể làm hỏng lịch sử của đồng nghiệp, ta sử dụng cơ chế tạo commit nghịch đảo:

1. Thực hiện đảo ngược thay đổi của một commit cũ bằng cách tạo commit mới đối lập:

```bash
git revert <commit-hash>

```

2. Xác nhận thông điệp commit đảo ngược (có tiêu đề bắt đầu bằng `Revert ...`) xuất hiện trên đầu nhánh.

# 2. Kiểm tra kết quả và Phân tích khác biệt

- **Lệnh kiểm tra lịch sử commit:**

```bash
git log --oneline -n 5

```

- **Phân biệt giữa Reset và Revert:**
- **Git Reset:** Thay đổi trực tiếp con trỏ HEAD và lịch sử cục bộ (xóa bỏ hoặc dịch chuyển lịch sử). Phù hợp khi làm việc cá nhân độc lập. **Tuyệt đối không dùng** khi code đã được đẩy lên nhánh chung (`main`/`develop`) vì sẽ gây xung đột lịch sử với các thành viên khác.
- **Git Revert:** Tạo ra một commit mới có tác dụng ngược lại với commit cũ, giữ nguyên vẹn lịch sử cũ. Cực kỳ an toàn và là tiêu chuẩn bắt buộc khi làm việc nhóm trên nhánh chung.
