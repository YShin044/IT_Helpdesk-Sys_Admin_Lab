# 📄 Script Documentation: Find Inactive Users

### 🎯 Objective
To perform a periodic security audit by automatically scanning for and identifying user accounts that have been inactive for over 90 days. The script then exports a detailed CSV report for administrative review and action.

### 📋 Prerequisites
-   The script must be run on a Domain Controller or a machine with the Active Directory PowerShell Module installed.
-   The `C:\_MinhTam\Reports` directory will be created automatically if it does not already exist.

### 📜 Script
```powershell
<#
.SYNOPSIS
    Finds and exports a report of inactive user accounts in Active Directory.

.DESCRIPTION
    This script finds all user accounts that have not logged in within a specified
    timeframe (default is 90 days). The results are exported to a CSV file
    for easy review and processing.

.AUTHOR
    Minh Tam

.DATE
    09/Aug/2025

.NOTES
    Run this script with Administrator privileges on a machine with the AD Module installed (typically a Domain Controller).
#>

#--------------------------------------------------------------------------------------
# CONFIGURATION SECTION
#--------------------------------------------------------------------------------------

# Number of days to be considered inactive
$inactiveDays = 90

# Path and filename for the exported report.
# The script will auto-create the C:\_MinhTam\Reports directory if it doesn't exist.
$reportFolder = "C:\_MinhTam\Reports"
if (-not (Test-Path -Path $reportFolder)) {
    New-Item -ItemType Directory -Path $reportFolder
}
$reportPath = Join-Path -Path $reportFolder -ChildPath "Inactive_Users_Report_$(Get-Date -Format 'yyyy-MM-dd').csv"


#--------------------------------------------------------------------------------------
# EXECUTION SECTION
#--------------------------------------------------------------------------------------

Write-Host "Starting the search for inactive accounts..." -ForegroundColor Cyan

try {
    # 1. Search for inactive accounts.
    $inactiveUsers = Search-ADAccount -AccountInactive -TimeSpan ([System.TimeSpan]::FromDays($inactiveDays)) -UsersOnly -ResultPageSize 0
    
    if ($null -ne $inactiveUsers) {
        # 2. Select the required properties and format the OU column.
        $reportData = $inactiveUsers | Select-Object Name, SamAccountName, LastLogonDate, @{
            Name       = 'OrganizationalUnit'
            Expression = { ($_.DistinguishedName -split ',', 2) }
        }

        # 3. Export the formatted results to a CSV file.
        $reportData | Export-Csv -Path $reportPath -NoTypeInformation -Encoding UTF8

        Write-Host "Complete! The report has been saved to:" -ForegroundColor Green
        Write-Host $reportPath -ForegroundColor Yellow
    }
    else {
        Write-Host "No inactive accounts found within the last $inactiveDays days." -ForegroundColor Green
    }
}
catch {
    Write-Error "An error occurred: $_"
}

Write-Host "--- SCRIPT FINISHED ---" -ForegroundColor Cyan
```
### ⚡ Execution Guide
1.  Run PowerShell as an Administrator.
2.  Navigate to the script's directory: `cd C:\_MinhTam`
3.  Execute the script: `.\Find-InactiveUsers.ps1`

### ✅ Validation Results

The script provides two clear outputs upon successful execution.

#### 1. PowerShell Console Output
The console confirms that the process has completed and provides the full path to the newly created report file.

<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/Script_Find-InactiveUsers/report_create.png" alt="PowerShell output showing a successful report creation" width="900" />

---

#### 2. Generated CSV Report
The exported CSV file provides a clean, actionable list of all inactive users, including their full name, login name, last logon date, and their location (OU) within Active Directory.

<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/Script_Find-InactiveUsers/result.png" alt="The final CSV report opened in Excel" width="900" />
