# 📄 Tài liệu GPO: Corp - Block USB Devices

### 🎯 Mục tiêu
Giảm thiểu rủi ro thất thoát dữ liệu và lây nhiễm mã độc bằng cách vô hiệu hóa quyền truy cập vào các thiết bị lưu trữ USB trên tất cả máy trạm của **Công ty MinhTam**.

### ⚙️ Chi tiết cấu hình
-   **Đối tượng áp dụng:** Liên kết tới OU `MinhTam/Company/Computers`.
<img src="" width="800" />

-   **Chính sách:** `All Removable Storage classes: Deny all access` được đặt thành `Enabled`.
> **Đường dẫn:** `Computer Configuration\Policies\Administrative Templates\System\Removable Storage Access`
<img src="https://github.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/blob/master/GPO-02-Block-USB/deny-all-access_Policy.png" width="800" />

### Kết quả xác thực
-   **Trước khi áp dụng:** USB được nhận và có thể truy cập dữ liệu.
<img src="https://github.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/blob/master/GPO-02-Block-USB/Before.png" width="900" />
-   **Sau khi áp dụng:** Khi truy cập USB, hệ thống hiển thị lỗi "Access is denied".
<img src="https://github.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/blob/master/GPO-02-Block-USB/After.png" width="900" />
