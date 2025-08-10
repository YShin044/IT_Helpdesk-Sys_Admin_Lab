# 📄 GPO-03 Documentation: Corp - Deploy Python-3.4.3

### 🎯 Objective
To automate the installation of Python across all new and existing workstations, ensuring all users have the necessary tools while reducing the manual workload for the IT team.

### 📋 Prerequisites
1.  **Installation File:** `python-3.4.3.msi` (64-bit) has been downloaded.
2.  **Network Share:** A shared folder is created on the server (e.g., `\\MT-DC01\Company_Software`).
3.  **Permissions:** The `Authenticated Users` group is granted `Read` permissions on the network share.
<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-03-Deploy-Software/Company_Software-Sharing.png" alt="Share permissions for the Company_Software folder" width="800" />

### ⚙️ Configuration Details
-   **Scope of Application:** Linked to the `MinhTam/Company/Computers` OU.
-   **Deployment Method:** `Assigned` (Mandatory installation).
> **Path:** `Computer Configuration\Policies\Software Settings\Software installation`
<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-03-Deploy-Software/Software_Installation.png" alt="Python package added to Software Installation GPO" width="800" />

### ✅ Validation Results
-   **Action:** A workstation within the target OU was restarted.
-   **Result:** After the user logged in, **Python (including IDLE)** was successfully installed and available for use in the Start Menu.
<img src="https://github.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/blob/master/GPO-03-Deploy-Software/Install.png" alt="Python installing" width="800" />
<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-03-Deploy-Software/update.png" alt="Python successfully installed and visible in the Start Menu" width="800" />
