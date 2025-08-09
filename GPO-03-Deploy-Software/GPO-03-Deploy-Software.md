# 📄 Tài liệu GPO: Corp - Deploy Python-3.4.3

### 🎯 Mục tiêu
Tự động hóa việc cài đặt phần mềm Python cho tất cả máy trạm mới và hiện có, đảm bảo mọi người dùng đều có công cụ cần thiết và giảm tải công việc cho đội IT.

### 📋 Yêu cầu chuẩn bị
1.  **File cài đặt:** Tải về `python-3.4.3.msi` (64-bit).
2.  **Thư mục chia sẻ:** Tạo một thư mục chia sẻ trên server (ví dụ: `\\MT-DC01\Company_Software`).
3.  **Phân quyền:** Cấp quyền `Read` cho nhóm `Authenticated Users` trên thư mục chia sẻ này.
    `[Ảnh chụp màn hình tab Sharing của thư mục SoftwareDeployment]`

### ⚙️ Chi tiết cấu hình
-   **Đối tượng áp dụng:** Liên kết tới OU `MinhTam/Company/Computers`.
-   **Phương thức:** `Assigned` (Bắt buộc cài đặt).
> **Đường dẫn:** `Computer Configuration\Policies\Software Settings\Software installation`
-   `[Ảnh chụp màn hình cửa sổ Software installation cho thấy gói 7-Zip đã được thêm]`

### Kết quả xác thực
-   **Hành động:** Khởi động lại một máy trạm trong OU.
-   **Kết quả:** Sau khi đăng nhập, ứng dụng `7-Zip File Manager` đã được cài đặt và sẵn sàng sử dụng trong Start Menu.
    `[Ảnh chụp màn hình Start Menu của MT-CLIENT01 hiển thị ứng dụng 7-Zip]`