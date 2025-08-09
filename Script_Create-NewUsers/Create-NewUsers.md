# 📄 Script Documentation: Create New Users

### 🎯 Function
This script streamlines the employee on-boarding process by programmatically generating standardized Active Directory accounts from a CSV file. It eliminates manual errors, ensures naming consistency, and saves significant administrative time.

### 📋 Prerequisites
-   A CSV file named `EmployeeList.csv` must be placed in the script's directory.
-   **CSV Format**: The file **must** include a header row with the following column names: `FirstName`, `LastName`, `Department`.
-   Example `EmployeeList.csv`:
    ```csv
    FirstName,LastName,Department
    An,Nguyen Van,Phong Kinh Doanh
    Binh,Tran Thi,Phong Kinh Doanh
    Cuong,Le Minh,Phong Kinh Doanh
    Duyen,Hoang My,Phong Kinh Doanh
    Hang,Pham Thu,Phong Ke Toan
    Lan,Dang Ngoc,Phong Ke Toan
    Dung,Bui Tien,Phong Ke Toan
    Truc,Huynh Thi,Phong Ke Toan
    Long,Vu Hoang,Phong Marketing
    Thu,Mai Anh,Phong Marketing
    Huy,Ho Gia,Phong Marketing
    ```

### 📜 Script
```powershell
# =====================================================================================
# Script Name:      Create-ADUsers-Robust.ps1 (Version 6.0 - Robust)
# Author:           Nguyen Minh Tam
# Date:             09/Aug/2025
# Description:      Automates AD account creation.
#                   - Checks for both sAMAccountName and Common Name (CN) conflicts.
#                   - Provides accurate warnings for each conflict type.
# =====================================================================================

#--------------------------------------------------------------------------------------
# PART 1: ENVIRONMENT CONFIGURATION
#--------------------------------------------------------------------------------------

$csvPath = "C:\_MinhTam\EmployeeList.csv"
$domainName = "minhtam.server"
$defaultPassword = ConvertTo-SecureString "P@ssword123" -AsPlainText -Force
$ouMapping = @{
    "Phong Kinh Doanh" = "OU=02_PhongKinhDoanh,OU=Users,OU=Company,OU=_MinhTam Company,DC=minhtam,DC=server"
    "Phong Ke Toan"     = "OU=03_PhongKeToan,OU=Users,OU=Company,OU=_MinhTam Company,DC=minhtam,DC=server"
    "Phong Marketing"   = "OU=04_PhongMarketing,OU=Users,OU=Company,OU=_MinhTam Company,DC=minhtam,DC=server"
}
$specialLastNameClusters = @("ng", "nh", "tr", "ch", "th", "kh", "ph", "gh")

#--------------------------------------------------------------------------------------
# PART 2: MAIN LOGIC - PROCESSING AND ACCOUNT CREATION
#--------------------------------------------------------------------------------------
Import-Csv -Path $csvPath | ForEach-Object {
    $firstName  = $_.FirstName
    $lastName   = $_.LastName
    $department = $_.Department

    $fullName = "$firstName $lastName"
    $cleanLastName = $lastName -replace '\s',''
    $targetOU = $ouMapping[$department]

    # Dynamically generate the sAMAccountName based on department and name
    $wordsInDept = $department.Split(' '); if ($wordsInDept.Count -gt 1 -and $wordsInDept -eq "Phong") { $deptPrefix = ($wordsInDept | Select-Object -Skip 1) -join "" } else { $deptPrefix = $department -replace '\s','' }; $firstNameInitial = $firstName.Substring(0, 1); foreach ($cluster in $specialLastNameClusters) { if ($firstName.StartsWith($cluster, [System.StringComparison]::InvariantCultureIgnoreCase)) { $firstNameInitial = $cluster; break } }; $samAccountName = "$($deptPrefix).$($cleanLastName)$($firstNameInitial)".ToLower(); if ($samAccountName.Length -gt 20) { Write-Warning "Username '$samAccountName' (length: $($samAccountName.Length)) exceeds 20 characters. Auto-truncating."; $samAccountName = $samAccountName.Substring(0, 20); Write-Host "New username: '$samAccountName'" -ForegroundColor Yellow }
    
    $userPrincipalName = "$samAccountName@$domainName"
    
    $samExists = Get-ADUser -Filter {SamAccountName -eq $samAccountName}
    # Use Get-ADObject to find any object type (user, group, contact) with a conflicting CN in the target OU
    $cnExists = Get-ADObject -Filter {Name -eq $fullName} -SearchBase $targetOU

    if ($samExists) {
        Write-Warning "Skipping: Login name (sAMAccountName) '$samAccountName' already exists in the domain."
    }
    elseif ($cnExists) {
        Write-Warning "Skipping: Display Name (CN) '$fullName' already exists in the OU '$($targetOU.Split(','))'."
    }
    else {
        # Only proceed with creation if both checks pass
        try {
            New-ADUser -Name $fullName `
                -GivenName $firstName `
                -Surname $lastName `
                -SamAccountName $samAccountName `
                -UserPrincipalName $userPrincipalName `
                -AccountPassword $defaultPassword `
                -ChangePasswordAtLogon $true `
                -Enabled $true `
                -Path $targetOU

            Write-Host "Successfully created account for: $fullName ($samAccountName)" -ForegroundColor Green
        }
        catch {
            Write-Error "An unexpected error occurred while creating account '$samAccountName': $_"
        }
    }
}
Write-Host "--- AUTOMATION PROCESS COMPLETE ---" -ForegroundColor Cyan
```

### ⚡ Execution Guide
1.  Run PowerShell as an Administrator.
2.  Navigate to the script's directory: `cd C:\_MinhTam`
3.  Execute the script: `.\Create-NewUsers.ps1`

### ✅ Validation Results
The script provides clear visual feedback for different scenarios.

#### Scenario 1: Successful Creation
When new users are created successfully from the CSV file, a green confirmation message is displayed for each account, confirming the action.

<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/Script_Create-NewUsers/success.png" alt="Success messages in PowerShell for new user creation" width="800" />

---

#### Scenario 2: Conflict Detected (User Already Exists)
If the script detects that a user already exists (either by `sAMAccountName` or `Common Name`), it will intelligently skip that entry and display a yellow warning message. This prevents the creation of duplicate accounts and informs the administrator of the conflict.

<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/Script_Create-NewUsers/existed.png" alt="Warning message shown in PowerShell for an existing user" width="800" />
