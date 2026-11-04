# GreenLogistics – Phân tích hiệu năng website

## Phần 1. Phân tích

Mở `F12 → Network → Disable cache → F5`, xem cột **Status**, **Size**, **Time** và biểu đồ **Waterfall**.

- **404:** Tài nguyên không tìm thấy, có thể làm mất ảnh bản đồ.
- **Ảnh quá lớn:** Tải chậm, tốn băng thông.
- **Request kéo dài:** Xem phần **Timing** để xác định nút thắt (chờ server hay tải dữ liệu).

**Kết luận:** Chưa đủ số liệu để khẳng định nguyên nhân duy nhất; ưu tiên kiểm tra request 404 và các request lâu nhất.

## Phần 2. Triển khai

1. **Sửa 404:** Kiểm tra đường dẫn file và API bản đồ.
2. **Nén ảnh:** Dùng WebP/AVIF, kích thước phù hợp; lazy-load ảnh không cần hiển thị ngay.
3. **Bật Browser Cache:** Cấu hình `Cache-Control` cho CSS, JavaScript, ảnh tĩnh; dùng tên file có phiên bản để tránh cache cũ.

Đảm bảo CSS/JS quan trọng tải thành công (`200 OK` lần tải mới; `304 Not Modified` hoặc cache hợp lệ khi tải lại). Không nhất thiết tất cả phải trả `200` ở mọi lần tải.

## Phần 3. Kiểm thử

**304 Not Modified** nghĩa là tài nguyên chưa đổi. Trình duyệt dùng lại bản đã lưu thay vì tải toàn bộ file, giúp **tiết kiệm băng thông**.

**Lưu ý:** Muốn kiểm thử hiệu quả cache khi reload, hãy **bỏ chọn Disable cache** rồi tải lại trang.
