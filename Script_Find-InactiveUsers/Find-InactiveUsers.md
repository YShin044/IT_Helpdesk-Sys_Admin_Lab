# 📄 Tài liệu Script: Find-InactiveUsers.ps1

### 🎯 Chức năng
Thực hiện kiểm toán bảo mật định kỳ bằng cách tự động quét và xác định các tài khoản người dùng không hoạt động (trên 90 ngày), sau đó xuất ra một báo cáo CSV chi tiết để quản trị viên có thể xem xét và xử lý.

### 📋 Yêu cầu chuẩn bị
-   Chạy script trên Domain Controller hoặc máy có cài đặt AD Module.
-   Thư mục `C:\_MinhTam\Reports` sẽ được tự động tạo nếu chưa tồn tại.

### 📜 Nội dung Script
```powershell
<#
.SYNOPSIS
    Tim kiem va xuat bao cao cac tai khoan nguoi dung khong hoat dong trong Active Directory.

.DESCRIPTION
    Script se tim tat ca cac tai khoan nguoi dung khong dang nhap trong mot khoang thoi gian
    nhat dinh (mac dinh la 90 ngay).
    Ket qua se duoc xuat ra mot file CSV de de dang xem va xu ly.

.AUTHOR
    Minh Tam

.DATE
    09/08/2025

.NOTES
    Chạy script này với quyền Administrator trên một máy đã cài AD Module (thường là Domain Controller).
#>

#--------------------------------------------------------------------------------------
# PHẦN CẤU HÌNH
#--------------------------------------------------------------------------------------

# Số ngày được tính là không hoạt động
$inactiveDays = 90

# Đường dẫn và tên file báo cáo sẽ được xuất ra.
# Script sẽ tự động tạo thư mục C:\Company\Reports nếu nó chưa tồn tại.
$reportFolder = "C:\_MinhTam\Reports"
if (-not (Test-Path -Path $reportFolder)) {
    New-Item -ItemType Directory -Path $reportFolder
}
$reportPath = Join-Path -Path $reportFolder -ChildPath "Inactive_Users_Report_$(Get-Date -Format 'yyyy-MM-dd').csv"


#--------------------------------------------------------------------------------------
# PHẦN THỰC THI
#--------------------------------------------------------------------------------------

Write-Host "Bat dau qua trinh tim kiem cac tai khoan khong hoat dong..." -ForegroundColor Cyan

try {
    # 1. Tim kiem cac tai khoan khong hoat dong.
    $inactiveUsers = Search-ADAccount -AccountInactive -TimeSpan ([System.TimeSpan]::FromDays($inactiveDays)) -UsersOnly -ResultPageSize 0
    
    if ($null -ne $inactiveUsers) {
        # 2. Lựa chọn các thuộc tính cần thiết và định dạng lại cột OU.
        $reportData = $inactiveUsers | Select-Object Name, SamAccountName, LastLogonDate, @{
            Name       = 'OrganizationalUnit'
            Expression = { ($_.DistinguishedName -split ',', 2)[1] }
        }

        # 3. Xuất kết quả đã được định dạng ra file CSV.
        $reportData | Export-Csv -Path $reportPath -NoTypeInformation -Encoding UTF8

        Write-Host "Hoan tat! Bao cao da duoc luu tai:" -ForegroundColor Green
        Write-Host $reportPath -ForegroundColor Yellow
    }
    else {
        Write-Host "Khong tim thay tai khoan nao khong hoat dong trong $inactiveDays ngay qua." -ForegroundColor Green
    }
}
catch {
    Write-Error "Da xay ra loi: $_"
}

Write-Host "--- KET THUC SCRIPT ---" -ForegroundColor Cyan ```

#⚡ Hướng dẫn thực thi
Mở PowerShell với quyền Administrator.
Điều hướng tới thư mục script: cd C:\MinhTam\Scripts
Chạy lệnh: .\Find-InactiveUsers.ps1

# Kết quả kỳ vọng
PowerShell thông báo hoàn tất và chỉ đường dẫn tới file báo cáo.
Một file báo cáo có tên Inactive_Users_Report_YYYY-MM-DD.csv được tạo trong C:\MinhTam\Reports.
File báo cáo chứa các thông tin quan trọng: Name, SamAccountName, LastLogonDate, và OrganizationalUnit.
[Ảnh chụp màn hình PowerShell thông báo đã xuất báo cáo thành công]
[Ảnh chụp màn hình file CSV kết quả mở bằng Excel]