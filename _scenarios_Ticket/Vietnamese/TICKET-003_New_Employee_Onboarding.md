### TICKET-003: Quy trình tiếp nhận và tạo tài khoản cho nhân viên mới
- **Mã phiếu:** TICKET-003
- **Tiêu đề:** [Yêu cầu] Tạo tài khoản cho nhân viên mới - Phạm Hoàng Long
- **Người yêu cầu:** Phòng Nhân sự
- **Hệ thống ảnh hưởng:** Active Directory, File Server

#### MÔ TẢ YÊU CẦU
Phòng Nhân sự gửi yêu cầu tạo tài khoản cho nhân viên mới với thông tin:
*   **Họ và tên:** Phạm Hoàng Long
*   **Phòng ban:** IT
*   **Chức vụ:** IT Helpdesk
*   **Ngày bắt đầu làm việc:** 11-Aug-2025

#### PHÂN TÍCH & ĐIỀU TRA
Đây là một yêu cầu dịch vụ (Service Request) chuẩn, không phải sự cố. Cần thực hiện theo đúng quy trình Onboarding của công ty.
1.  **Quy tắc đặt tên:** `phongban.tenho` -> `it.longph`.
2.  **Vị trí OU:** Tài khoản sẽ được tạo trong OU `IT`.
3.  **Quyền truy cập:** Cần thêm vào các nhóm:
    *   `SG_IT_Users`: Nhóm chung cho nhân viên IT.
    *   `SG_IT_Share_Modify`: Quyền truy cập thư mục chung của phòng IT.

#### GIẢI PHÁP & HÀNH ĐỘNG
1.  **Tạo tài khoản:** Trong `ADUC`, điều hướng đến OU `IT`, tạo mới một người dùng với thông tin đã phân tích.
2.  Đặt mật khẩu tạm thời và tích chọn **"User must change password at next logon"**.
3.  **Gán thành viên nhóm:** Mở thuộc tính tài khoản `it.longph`, tab "Member Of", thêm tài khoản vào các nhóm `SG_IT_Users` và `SG_IT_Share_Modify`.
4.  **Tạo thư mục cá nhân (Nếu có):** (Tùy chọn) Chạy script để tạo thư mục cá nhân trên File Server và gán quyền.

#### KẾT QUẢ XỬ LÝ
-   Tài khoản `it.longph` đã được tạo và cấu hình thành công.
-   Thông tin đăng nhập đã được tạo và niêm phong trong bì thư để gửi cho Phòng Nhân sự.
-   Phiếu hỗ trợ `TICKET-003` được cập nhật trạng thái **Đã hoàn thành**.

#### Phản hồi cho người dùng (Phòng Nhân sự)
> "Chào phòng Nhân sự, bộ phận IT đã hoàn tất yêu cầu tạo tài khoản cho nhân viên mới Phạm Hoàng Long (tên đăng nhập: `it.longph`). Thông tin đăng nhập đã được niêm phong và sẽ được gửi qua cho quý phòng để bàn giao. Cảm ơn."