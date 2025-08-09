# 📄 GPO-04 Documentation: KinhDoanh - Map Drive S

### 🎯 Objective
To provide Sales department employees with quick and consistent access to their shared network drive by automatically mapping the `S:` (Sales) drive upon login.

### 📋 Prerequisites
1.  **Shared Folder:** The `C:\Shares\Sales` folder is created on the server `MT-DC01`.
2.  **Permissions:** Both Share and NTFS permissions are configured to grant granular access using two distinct security groups:
    -   The `SG_KinhDoanh_Share_Modify` group is granted `Modify` rights.
    
    <img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-04-Map-Network-Drive/SG_KinhDoanh_Share_Modify.png" alt="Modify permissions for the Modify group" width="300" />
   
    -   The `SG_KinhDoanh_Share_Read` group is granted `Read` rights only.
    
    <img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-04-Map-Network-Drive/SG_KinhDoanh_Share_Read.png" alt="Read-only permissions for the Read group" width="300" />

### ⚙️ Configuration Details
-   **Scope of Application:** Linked to the `MinhTam/Company/Users/02_PhongKinhDoanh` OU.
-   **Action:** `Update`
-   **Drive Letter:** `S:`
> **Path:** `User Configuration\Preferences\Windows Settings\Drive Maps`
<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-04-Map-Network-Drive/Mapped_Drive-Detail.png" alt="Mapped Drive configuration details" width="800" />

### Validation Results
The policy was verified by logging in with both a targeted (Sales) user and a non-targeted (IT) user.

| Sales User (Targeted) | Non-Sales User (IT Department) |
| :---: | :---: |
| *The `S:` drive is successfully mapped and visible.* | *The `S:` drive is correctly not mapped, as expected.* |
| <img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-04-Map-Network-Drive/sales_member.png" alt="The S drive is visible for the Sales user" width="450" /> | <img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-04-Map-Network-Drive/it_member.png" alt="The S drive is not visible for the IT user" width="450" /> |
