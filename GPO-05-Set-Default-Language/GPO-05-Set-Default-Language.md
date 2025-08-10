# 📄 Tài liệu GPO: Corp - Set Default Language

### 🎯 Mục tiêu
Chuẩn hóa ngôn ngữ nhập liệu (bàn phím) mặc định cho tất cả người dùng trong **Công ty MinhTam** thành **English (United States)**. Việc này giải quyết vấn đề các máy tính mới cài đặt Windows có thể mặc định là English (United Kingdom), gây ra sự khác biệt trong layout bàn phím và trải nghiệm người dùng.

### 💡 Phương pháp tiếp cận
Sử dụng **Group Policy Preferences (GPP)** để trực tiếp chỉnh sửa Registry của người dùng khi họ đăng nhập. Đây là phương pháp hiệu quả và đáng tin cậy nhất để ghi đè các cài đặt mặc định của hệ thống.

-   **Mã ngôn ngữ cho English (United States):** `00000409`
-   **Mã ngôn ngữ cho English (United Kingdom):** `00000809`

### ⚙️ Chi tiết cấu hình
1.  **Tạo và liên kết GPO:** GPO được liên kết tới OU `MinhTam/Company/Users`.
    *   `[Ảnh chụp màn hình GPM, cho thấy GPO được link vào OU Users]`

2.  **Cấu hình Registry qua GPP:**
    > **Đường dẫn:** `User Configuration -> Preferences -> Windows Settings -> Registry`

    **Hành động 1: Dọn dẹp (Delete)**
    *   Tạo một Registry Item để xóa toàn bộ các giá trị trong key `Keyboard Layout\Preload` nhằm đảm bảo một môi trường sạch sẽ.
    *   `[Ảnh chụp màn hình cửa sổ cấu hình Registry cho hành động Delete]`

    **Hành động 2: Thiết lập mặc định (Update)**
    *   Tạo một Registry Item thứ hai để thiết lập giá trị `1` (mặc định) thành `00000409`.
    *   `[Ảnh chụp màn hình cửa sổ cấu hình Registry cho hành động Update]`

### Kết quả xác thực
Hành động được xác thực bằng cách so sánh trạng thái của máy trạm trước và sau khi áp dụng chính sách.

| Trước khi áp dụng GPO | Sau khi áp dụng GPO |
| :---: | :---: |
| *Thanh ngôn ngữ mặc định là 'ENG UK'* | *Thanh ngôn ngữ đã được chuẩn hóa thành 'ENG US'* |
| <img src="đường/dẫn/tới/ảnh/trước.png" alt="Taskbar hiển thị ENG UK" width="350" /> | <img src="đường/dẫn/tới/ảnh/sau.png" alt="Taskbar hiển thị ENG US" width="350" /> |

### ⭐ Mẹo chuyên nghiệp
Phương pháp này rất linh hoạt. Để thêm một ngôn ngữ thứ hai (ví dụ: Tiếng Việt) mà không làm nó trở thành mặc định, bạn chỉ cần tạo thêm một Registry Item với `Value name` là `2` và `Value data` là `0000042a`.