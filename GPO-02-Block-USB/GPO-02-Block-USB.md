# 📄 Tài liệu GPO: Corp - Block USB Devices

### 🎯 Mục tiêu
Giảm thiểu rủi ro thất thoát dữ liệu và lây nhiễm mã độc bằng cách vô hiệu hóa quyền truy cập vào các thiết bị lưu trữ USB trên tất cả máy trạm của **Công ty MinhTam**.

### ⚙️ Chi tiết cấu hình
-   **Đối tượng áp dụng:** Liên kết tới OU `MinhTam/Company/Computers`.
-   `[Ảnh chụp màn hình GPM, cho thấy GPO được link vào OU Computers]`
-   **Chính sách:** `All Removable Storage classes: Deny all access` được đặt thành `Enabled`.
> **Đường dẫn:** `Computer Configuration\Policies\Administrative Templates\System\Removable Storage Access`
-   `[Ảnh chụp màn hình chi tiết chính sách "Deny all access" được bật]`

### Kết quả xác thực
-   **Trước khi áp dụng:** USB được nhận và có thể truy cập dữ liệu.
    `[Ảnh chụp màn hình File Explorer cho thấy ổ đĩa USB (ví dụ: E:) hoạt động bình thường]`
-   **Sau khi áp dụng:** Khi truy cập USB, hệ thống hiển thị lỗi "Access is denied".
    `[Ảnh chụp màn hình thông báo lỗi "Access is denied" khi click vào ổ USB]`