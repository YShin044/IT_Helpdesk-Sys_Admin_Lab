# 📄 GPO-01 Documentation: Corp - Security Policy

### 🎯 Objective
To enforce a set of foundational security policies across the entire **MinhTam Company**, strengthening the security posture of the identity system.

### ⚙️ Configuration Details
-   **Scope of Application:** Linked to the root of the `minhtam.server` domain to ensure company-wide enforcement.
<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-01-Security-Policy/Corp-Security_Link.png" alt="GPO linked to the domain root" width="800" />

#### 1. Password Policy (Computer Configuration)
> **Path:** `Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Password Policy`
-   **Password must meet complexity requirements:** `Enabled`
-   **Minimum password length:** `8 characters`
-   **Enforce password history:** `24 passwords remembered`
<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-01-Security-Policy/Detail_Password-Policy.png" alt="Password Policy configuration details" width="800" />

#### 2. Screen Lock Policy (User Configuration)
> **Path:** `User Configuration\Policies\Administrative Templates\Control Panel\Personalization`
-   **Enable screen saver:** `Enabled`
-   **Password protect the screen saver:** `Enabled`
-   **Screen saver timeout:** `Enabled` (Value: `600` seconds)
<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-01-Security-Policy/Detail_Personalization.png" alt="Screen Lock Policy configuration details" width="800" />

### Validation Results
-   **Password Validation:** The system rejects simple passwords that do not meet the complexity requirements.
<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-01-Security-Policy/Refuse-Password.png" alt="Error message for non-compliant password" width="800" />

-   **Screen Lock Validation:** The workstation automatically locks after 10 minutes of inactivity.
<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-01-Security-Policy/Auto-Sleep-Screen.png" alt="Windows lock screen after timeout" width="800" />
