### TICKET-001: Không thể ghi file lên ổ đĩa dùng chung
- **Mã phiếu:** TICKET-001
- **Tiêu đề:** Người dùng không thể lưu file vào ổ đĩa S:
- **Người yêu cầu:** Nguyễn Văn An - Phòng Kinh Doanh
- **Hệ thống ảnh hưởng:** File Server (`\\minhtam.server\Shares\Sales`)

#### MÔ TẢ SỰ CỐ
> "Chào IT, tôi có thể mở và xem các file trong ổ đĩa S: của phòng Kinh Doanh, nhưng khi tôi cố gắng tạo file mới hoặc lưu một file đã chỉnh sửa, hệ thống báo lỗi 'Permission Denied'. Vui lòng kiểm tra giúp tôi."

#### PHÂN TÍCH & ĐIỀU TRA
1.  **Kiểm tra thành viên nhóm:** Mở `Active Directory Users and Computers` (ADUC), tìm tài khoản `kinhdoanh.vananng`. Kiểm tra tab "Member Of".
2.  **Phát hiện:** Người dùng chỉ là thành viên của nhóm `SG_KinhDoanh_Share_Read`. Người dùng không thuộc nhóm `SG_KinhDoanh_Share_Modify`.
3.  **Xác thực quyền:** Kiểm tra quyền NTFS trên thư mục chia sẻ `\\minhtam.server\Shares\Sales`, xác nhận nhóm `SG_KinhDoanh_Share_Modify` đã được cấp quyền `Modify` chính xác.

#### NGUYÊN NHÂN GỐC RỄ
Do sơ suất trong quy trình khởi tạo, tài khoản của người dùng đã không được thêm vào nhóm bảo mật có quyền ghi (`Modify`), dẫn đến việc chỉ có quyền đọc dữ liệu.

#### GIẢI PHÁP & HÀNH ĐỘNG
1.  Trong `ADUC`, thêm tài khoản `kinhdoanh.vananng` vào nhóm bảo mật `SG_KinhDoanh_Share_Modify`.
2.  Yêu cầu người dùng **đăng xuất (Sign out) và đăng nhập lại** để hệ thống làm mới thẻ bài truy cập (access token).

#### KẾT QUẢ XỬ LÝ
-   Người dùng đã có thể đọc/ghi trên ổ đĩa S: như mong đợi.
-   Phiếu hỗ trợ `TICKET-001` được cập nhật trạng thái **Đã giải quyết**.

#### Phản hồi cho người dùng
> "Chào anh An, bộ phận IT đã kiểm tra và xác định vấn đề nằm ở quyền truy cập của tài khoản. Chúng tôi đã cập nhật lại quyền cho anh. Vui lòng **đăng xuất và đăng nhập lại** để thay đổi có hiệu lực. Sau khi đăng nhập lại, anh sẽ có thể lưu file vào ổ S: như bình thường. Cảm ơn anh."