# 📄 GPO-02 Documentation: Corp - Block USB Devices

### 🎯 Objective
To mitigate the risk of data leakage and malware infection by disabling access to USB storage devices on all workstations within **MinhTam Company**.

### ⚙️ Configuration Details
-   **Scope of Application:** Linked to the `MinhTam/Company/Computers` OU.
<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-02-Block-USB/Link_to_Computers.png" alt="GPO linked to the Computers OU" width="800" />

-   **Policy:** `All Removable Storage classes: Deny all access` is set to `Enabled`.
> **Path:** `Computer Configuration\Policies\Administrative Templates\System\Removable Storage Access`
<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-02-Block-USB/deny-all-access_Policy.png" alt="Deny all access policy enabled" width="800" />

### Validation Results
The policy was tested by attempting to access a USB drive before and after the GPO was applied.

| Before Applying GPO | After Applying GPO |
| :---: | :---: |
| *The USB drive is detected and fully accessible.* | *The system blocks access, showing an "Access is denied" error.* |
| <img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-02-Block-USB/Before.png" alt="USB drive accessible before policy" width="450" /> | <img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-02-Block-USB/After.png" alt="Access denied error after policy" width="450" /> |
