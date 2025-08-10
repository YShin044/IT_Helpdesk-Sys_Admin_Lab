# 📄 GPO-05 Documentation: Corp - Set Default Language

### 🎯 Objective
To standardize the default input language for all users within **MinhTam Company** to **English (United States)**. This policy resolves user experience issues, such as incorrect keyboard layouts, that arise from system defaults like English (United Kingdom).

### 💡 Technical Approach
This policy leverages **Group Policy Preferences (GPP)** to directly modify the user's registry upon login. This is the most reliable method for enforcing a specific setting and overriding any pre-existing user or system defaults.

-   **Code for English (United States):** `00000409`
-   **Code for English (United Kingdom):** `00000809`

### ⚙️ Configuration Details

**1. GPO Linking & Scope:**
The GPO is linked to the `_MinhTam Company/Company/Users` OU to apply to all user accounts.
<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-05-Set-Default-Language/Link_OU_Users.png" alt="GPO linked to the Users OU" width="800" />

**2. GPP Registry Configuration:**
> **Path:** `User Configuration -> Preferences -> Windows Settings -> Registry`

**Action 1: Cleanup (Delete)**
*   A Registry Item is configured to delete all existing values under the `Keyboard Layout\Preload` key. This ensures a clean slate before applying the new default.
<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-05-Set-Default-Language/RegistryItem_Delete.png" alt="Registry Item configured to Delete" width="600" />

**Action 2: Set Default (Update)**
*   A second Registry Item is created to set the value `1` (for default) to `00000409`.
<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-05-Set-Default-Language/RegistryItem_Create.png" alt="Registry Item configured to Create/Update" width="600" />

### Validation Results
The policy was validated by comparing a workstation's state before and after the GPO was applied.

| Before Applying GPO | After Applying GPO |
| :---: | :---: |
| *The taskbar shows the default 'ENG UK' input.* | *The taskbar now correctly shows 'ENG US' as the default.* |
| <img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-05-Set-Default-Language/Before.png" alt="Taskbar showing ENG UK input method before policy" width="450" /> | <img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/GPO-05-Set-Default-Language/After.png" alt="Taskbar showing ENG US input method after policy" width="450" /> |

### ⭐ Tip
This GPP method is highly flexible. To add a secondary language (e.g., Vietnamese) without making it the default, simply create another Registry Item with the `Value name` set to `2` and the `Value data` set to its corresponding code (`0000042a`).
