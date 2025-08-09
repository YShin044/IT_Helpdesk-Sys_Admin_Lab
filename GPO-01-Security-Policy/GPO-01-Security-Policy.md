# 📄 Tài liệu GPO: Corp - Security Policy

### 🎯 Mục tiêu
Thực thi một bộ chính sách bảo mật nền tảng cho toàn bộ **Công ty MinhTam**, nhằm tăng cường phòng tuyến an ninh cho hệ thống định danh.

### ⚙️ Chi tiết cấu hình
-   **Đối tượng áp dụng:** Liên kết tới gốc domain `minhtam.server` để đảm bảo phạm vi ảnh hưởng toàn công ty.
<img src="https://github.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/blob/master/GPO-01-Security-Policy/Corp-Security_Link.png" width="800" />

#### 1. Chính sách Mật khẩu (Computer Configuration)
> **Path:** `Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Password Policy`
-   **Password must meet complexity requirements:** `Enabled`
-   **Minimum password length:** `8 characters`
-   **Enforce password history:** `24 passwords remembered`
<img src="https://github.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/blob/master/GPO-01-Security-Policy/Detail_Password-Policy.png" width="800" />

#### 2. Chính sách Khóa màn hình (User Configuration)
> **Path:** `User Configuration\Policies\Administrative Templates\Control Panel\Personalization`
-   **Enable screen saver:** `Enabled`
-   **Password protect the screen saver:** `Enabled`
-   **Screen saver timeout:** `Enabled` (Giá trị: `600` giây)
<img src="https://github.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/blob/master/GPO-01-Security-Policy/Detail_Personalization.png" width="800" />

### Kết quả xác thực
-   **Xác thực mật khẩu:** Hệ thống từ chối các mật khẩu đơn giản, không đáp ứng yêu cầu.
<img src="https://github.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/blob/master/GPO-01-Security-Policy/Refuse-Password.png" width="800" />

-   **Xác thực khóa màn hình:** Máy trạm tự động khóa sau 10 phút không sử dụng.
<img src="https://github.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/blob/master/GPO-01-Security-Policy/Auto-Sleep-Screen.png" width="800" />
