# 📄 Tài liệu Script: Create-NewUsers.ps1

### 🎯 Chức năng
Tự động hóa quy trình on-boarding nhân viên mới. Script đọc thông tin từ file CSV và tạo tài khoản Active Directory theo đúng chuẩn, giảm thiểu sai sót và tiết kiệm hàng giờ làm việc thủ công.

### 📋 Yêu cầu chuẩn bị
-   Một file `DanhSachNhanVien.csv` đặt cùng thư mục với script.
-   **Định dạng CSV:** `Ho,Ten,PhongBan` (Không có dòng tiêu đề).
-   **Ví dụ:**
    ```csv
	Ho,Ten,PhongBan
	Nguyen,Van An,Phong Kinh Doanh
	Tran,Thi Binh,Phong Kinh Doanh
	Le,Minh Cuong,Phong Kinh Doanh
	Hoang,My Duyen,Phong Kinh Doanh
	Pham,Thu Hang,Phong Ke Toan
	Dang,Ngoc Lan,Phong Ke Toan
	Bui,Tien Dung,Phong Ke Toan
	Huynh,Thi Truc,Phong Ke Toan
	Vu,Hoang Long,Phong Marketing
	Mai,Anh Thu,Phong Marketing
	Ho,Gia Huy,Phong Marketing
    ```

### 📜 Nội dung Script
```powershell
# =====================================================================================
# Script Name:      Create-ADUsers-Robust.ps1 (Version 6.0 - Robust)
# Author:           Nguyen Minh Tam
# Date:             09/08/2025
# Description:      Tự động tạo tài khoản AD.
#                   - Kiểm tra xung đột cả sAMAccountName và Common Name (CN)
#                   - Cung cấp cảnh báo chính xác cho từng loại xung đột.
# =====================================================================================

#--------------------------------------------------------------------------------------
# PHẦN 1: CẤU HÌNH BIẾN MÔI TRƯỜNG
#--------------------------------------------------------------------------------------

$csvPath = "C:\_MinhTam\DanhSachNhanVien.csv"
$domainName = "minhtam.server"
$defaultPassword = ConvertTo-SecureString "P@ssword123" -AsPlainText -Force
$ouMapping = @{
    "Phong Kinh Doanh" = "OU=02_PhongKinhDoanh,OU=Users,OU=Company,OU=_MinhTam Company,DC=minhtam,DC=server"
    "Phong Ke Toan"     = "OU=03_PhongKeToan,OU=Users,OU=Company,OU=_MinhTam Company,DC=minhtam,DC=server"
    "Phong Marketing"   = "OU=04_PhongMarketing,OU=Users,OU=Company,OU=_MinhTam Company,DC=minhtam,DC=server"
}
$specialLastNameClusters = @("ng", "nh", "tr", "ch", "th", "kh", "ph", "gh")

#--------------------------------------------------------------------------------------
# PHẦN 2: LOGIC CHÍNH - XỬ LÝ VÀ TẠO TÀI KHOẢN
#--------------------------------------------------------------------------------------
Import-Csv -Path $csvPath | ForEach-Object {
    $ho       = $_.Ho
    $ten      = $_.Ten
    $phongBan = $_.PhongBan

    $fullName = "$ho $ten"
    $cleanTen = $ten -replace '\s',''
    $targetOU = $ouMapping[$phongBan]

    # ... (Toàn bộ logic tạo $samAccountName giữ nguyên như trước)
    $wordsInDept = $phongBan.Split(' '); if ($wordsInDept.Count -gt 1 -and $wordsInDept[0] -eq "Phong") { $phongBanPrefix = ($wordsInDept | Select-Object -Skip 1) -join "" } else { $phongBanPrefix = $phongBan -replace '\s','' }; $lastNameInitial = $ho.Substring(0, 1); foreach ($cluster in $specialLastNameClusters) { if ($ho.StartsWith($cluster, [System.StringComparison]::InvariantCultureIgnoreCase)) { $lastNameInitial = $cluster; break } }; $samAccountName = "$($phongBanPrefix).$($cleanTen)$($lastNameInitial)".ToLower(); if ($samAccountName.Length -gt 20) { Write-Warning "Ten '$samAccountName' (dai: $($samAccountName.Length)) vuot qua 20 ky tu. Tu dong cat."; $samAccountName = $samAccountName.Substring(0, 20); Write-Host "Ten moi: '$samAccountName'" -ForegroundColor Yellow }
    
    $userPrincipalName = "$samAccountName@$domainName"
    
    $samExists = Get-ADUser -Filter {SamAccountName -eq $samAccountName}
    # Get-ADObject dùng để tìm bất kỳ loại đối tượng nào (user, group, contact) có trùng tên CN trong OU
    $cnExists = Get-ADObject -Filter {Name -eq $fullName} -SearchBase $targetOU

    if ($samExists) {
        Write-Warning "Bo qua: Ten dang nhap (sAMAccountName) '$samAccountName' da ton tai trong domain."
    }
    elseif ($cnExists) {
        Write-Warning "Bo qua: Ten hien thi (CN) '$fullName' da ton tai trong OU '$($targetOU.Split(',')[0])'."
    }
    else {
        # Chỉ khi cả hai đều không tồn tại, chúng ta mới tiến hành tạo
        try {
            New-ADUser -Name $fullName `
                -GivenName $ho `
                -Surname $ten `
                -SamAccountName $samAccountName `
                -UserPrincipalName $userPrincipalName `
                -AccountPassword $defaultPassword `
                -ChangePasswordAtLogon $true `
                -Enabled $true `
                -Path $targetOU

            Write-Host "Da tao thanh cong tai khoan cho: $fullName ($samAccountName)" -ForegroundColor Green
        }
        catch {
            Write-Error "Da xay ra loi khong xac dinh khi tao tai khoan '$samAccountName': $_"
        }
    }
}
Write-Host "--- HOAN TAT QUA TRINH TU DONG HOA ---" -ForegroundColor Cyan ```
#⚡ Hướng dẫn thực thi
Mở PowerShell với quyền Administrator.
Điều hướng tới thư mục script: cd C:\MinhTam\Scripts
Chạy lệnh: .\Create-NewUsers.ps1
✅ Kết quả kỳ vọng
PowerShell hiển thị các thông báo thành công màu xanh lá cho mỗi tài khoản được tạo.
Các tài khoản người dùng mới xuất hiện trong OU tương ứng trên Active Directory Users and Computers.
[Ảnh chụp màn hình kết quả chạy script thành công trên PowerShell]
[Ảnh chụp màn hình ADUC cho thấy các user mới đã nằm trong OU chính xác]