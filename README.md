Quy tắc khi commit lên repo: 
1. **Không code trực tiếp trên nhánh `main` (hoặc `master`).** Nhánh `main` chỉ chứa mã nguồn đã hoàn chỉnh và chạy ổn định.
2. Khi bắt đầu làm phần của mình, hãy tạo một nhánh mới từ `developer`:
  - Quy tắc đặt tên branch: tên+3 số cuối mssv
  - Dùng U/I trên github: Chọn `branch` rồi chọn `new branch` với source là  branch `developer`
  - hoặc dùng code tạo một nhánh khác
   ```bash
   git checkout developer
   git pull origin developer // Tai file ve may
   git checkout -b nhat017
   ```
  - Mở file ipynb trong `main` rồi chọn `Open in Colab`.
  - Sau khi làm xong thì chọn `Save to GitHub `
3. Quy tắc viết commit:

- [loại_commit]: Mô tả ngắn gọn bằng tiếng Việt, viết thường, không dấu chấm cuối câu
- loại commit gồm: add (thêm tính năng), fix (sửa lỗi),..
4. Các bước yêu cầu tối thiểu phải đạt đã viết trong file ipynb. Đặt tên biến ngắn gọn, có nghĩa, bằng tiếng anh.
5. Khi nào muốn merge phải liên hệ với trưởng nhóm.

