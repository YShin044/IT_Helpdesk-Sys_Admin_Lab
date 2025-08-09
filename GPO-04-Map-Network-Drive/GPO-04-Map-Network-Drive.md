# 📄 Tài liệu GPO: KinhDoanh - Map Drive S

### 🎯 Mục tiêu
Cung cấp cho nhân viên phòng Kinh Doanh quyền truy cập nhanh và nhất quán vào ổ đĩa mạng dùng chung bằng cách tự động ánh xạ ổ `S:` (Sales) khi họ đăng nhập.

### 📋 Yêu cầu chuẩn bị
1.  **Thư mục chia sẻ:** Tạo thư mục `C:\Shares\Sales` trên server `MT-DC01`.
2.  **Phân quyền:** Cấu hình đồng thời **Share Permissions** và **NTFS Permissions**, cấp quyền `Modify` cho nhóm bảo mật `SG_KinhDoanh_Share_Modify`.
    `[Ảnh chụp màn hình tab Security (NTFS) của thư mục Sales]`

### ⚙️ Chi tiết cấu hình
-   **Đối tượng áp dụng:** Liên kết tới OU `MinhTam/Company/Users/02_PhongKinhDoanh`.
-   **Hành động:** `Update`
-   **Drive Letter:** `S:`
> **Đường dẫn:** `User Configuration\Preferences\Windows Settings\Drive Maps`
-   `[Ảnh chụp màn hình cửa sổ cấu hình Mapped Drive chi tiết]`

### Kết quả xác thực
-   **Người dùng Kinh Doanh:** Đăng nhập bằng tài khoản thuộc phòng Kinh Doanh, ổ đĩa `Sales Share (S:)` xuất hiện trong This PC.
    `[Ảnh chụp màn hình This PC của user Kinh Doanh, thấy rõ ổ S:]`
-   **Người dùng khác:** Đăng nhập bằng tài khoản phòng Kế Toán, không thấy ổ `S:`.
    `[Ảnh chụp màn hình This PC của user Kế Toán, không có ổ S:]`