### TICKET-002: Người dùng bị khóa tài khoản do nhập sai mật khẩu
- **Mã phiếu:** TICKET-002
- **Tiêu đề:** Tài khoản domain bị khóa - Không thể đăng nhập
- **Người yêu cầu:** Vũ Hoàng Long - Phòng Marketing
- **Hệ thống ảnh hưởng:** Active Directory

#### MÔ TẢ SỰ CỐ
> "Chào IT, tôi không thể đăng nhập vào máy tính sáng nay. Tôi đã thử nhập mật khẩu vài lần và bây giờ hệ thống báo tài khoản của tôi đã bị khóa (Your account has been locked out). Vui lòng hỗ trợ."

#### PHÂN TÍCH & ĐIỀU TRA
1.  **Kiểm tra trạng thái tài khoản:** Mở `Active Directory Users and Computers` (ADUC), tìm tài khoản `marketing.hoanglongv` trong OU Marketing.
2.  Mở thuộc tính (Properties) của tài khoản, chọn tab **"Account"**.
3.  **Phát hiện:** Ô **"Unlock account. This account is currently locked out on this Active Directory Domain Controller"** đang được tích chọn. Điều này xác nhận tài khoản đang bị khóa.

#### NGUYÊN NHÂN GỐC RỄ
Người dùng đã nhập sai mật khẩu quá số lần cho phép được quy định trong **Chính sách Mật khẩu của Domain** (Default Domain Password Policy), dẫn đến cơ chế khóa tài khoản tự động được kích hoạt để bảo vệ hệ thống.

#### GIẢI PHÁP & HÀNH ĐỘNG
1.  Trong tab "Account" của tài khoản `marketing.hoanglongv`, **bỏ tích** ở ô "Unlock account".
2.  Nhấn `Apply` để mở khóa tài khoản.
3.  **Hành động chủ động:** Vì người dùng có thể đã quên mật khẩu, tiến hành reset. Chuột phải vào tài khoản, chọn `Reset Password`.
4.  Đặt một mật khẩu tạm thời mạnh và tích chọn **"User must change password at next logon"**.

#### KẾT QUẢ XỬ LÝ
-   Tài khoản đã được mở khóa và reset mật khẩu thành công.
-   Người dùng đã có thể đăng nhập bằng mật khẩu tạm thời và tự đặt lại mật khẩu mới.
-   Phiếu hỗ trợ `TICKET-002` được cập nhật trạng thái **Đã giải quyết**.

#### Phản hồi cho người dùng
> "Chào chị Bình, bộ phận IT đã kiểm tra và mở khóa tài khoản cho chị. Chúng tôi cũng đã cấp lại cho chị một mật khẩu tạm thời. Chị vui lòng kiểm tra email cá nhân (hoặc kênh liên lạc khác) để nhận mật khẩu. Khi đăng nhập lại, hệ thống sẽ yêu cầu chị đặt ngay một mật khẩu mới của riêng mình. Cảm ơn chị."