# 📄 Tài liệu GPO: Corp - Security Policy

### 🎯 Mục tiêu
Thực thi một bộ chính sách bảo mật nền tảng cho toàn bộ **Công ty MinhTam**, nhằm tăng cường phòng tuyến an ninh cho hệ thống định danh.

### ⚙️ Chi tiết cấu hình
-   **Đối tượng áp dụng:** Liên kết tới gốc domain `minhtam.server` để đảm bảo phạm vi ảnh hưởng toàn công ty.
-   `[Ảnh chụp màn hình GPM, cho thấy GPO được link vào domain minhtam.server]`

#### 1. Chính sách Mật khẩu (Computer Configuration)
> **Đường dẫn:** `Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Password Policy`
-   **Password must meet complexity requirements:** `Enabled`
-   **Minimum password length:** `8 characters`
-   **Enforce password history:** `24 passwords remembered`
-   `[Ảnh chụp màn hình chi tiết các cấu hình trong Password Policy]`

#### 2. Chính sách Khóa màn hình (User Configuration)
> **Đường dẫn:** `User Configuration\Policies\Administrative Templates\Control Panel\Personalization`
-   **Enable screen saver:** `Enabled`
-   **Password protect the screen saver:** `Enabled`
-   **Screen saver timeout:** `Enabled` (Giá trị: `600` giây)
-   `[Ảnh chụp màn hình chi tiết các cấu hình trong Personalization]`

### Kết quả xác thực
-   **Xác thực mật khẩu:** Hệ thống từ chối các mật khẩu đơn giản, không đáp ứng yêu cầu.
    `[Ảnh chụp màn hình thông báo lỗi khi user cố đặt mật khẩu '123456']`
-   **Xác thực khóa màn hình:** Máy trạm tự động khóa sau 10 phút không sử dụng.
    `[Ảnh chụp màn hình khóa của Windows trên máy MT-CLIENT01]`