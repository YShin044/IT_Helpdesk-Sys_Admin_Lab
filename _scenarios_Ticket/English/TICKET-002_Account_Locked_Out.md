### TICKET-002: User Account Locked Out Due to Incorrect Password Attempts
- **Ticket ID:** TICKET-002
- **Title:** Domain account is locked out - Cannot log in
- **Requester:** Binh Tran - Marketing Department
- **Affected System:** Active Directory

#### INCIDENT DESCRIPTION
> "Hi IT, I can't log into my computer this morning. I tried my password a few times, and now the system says 'Your account has been locked out.' Please help."

#### ANALYSIS & INVESTIGATION
1.  **Check Account Status:** Opened `Active Directory Users and Computers` (ADUC), located the user account `marketing.binhtran` in the Marketing OU.
2.  Opened the account's `Properties` and selected the **"Account"** tab.
3.  **Finding:** The checkbox for **"Unlock account. This account is currently locked out on this Active Directory Domain Controller"** is checked. This confirms the account is locked.
    *Screenshot:* `![Binh Tran's account is locked](images/T002_1_AccountLocked.png)`

#### ROOT CAUSE
The user exceeded the maximum number of failed password attempts as defined by the **Default Domain Password Policy**. This triggered the automatic account lockout mechanism to protect the system.

#### RESOLUTION & ACTIONS
1.  In the "Account" tab for `marketing.binhtran`, **uncheck** the "Unlock account" box.
2.  Click `Apply` to unlock the account.
3.  **Proactive Step:** Since the user likely forgot the password, proceed with a password reset. Right-click the user account and select `Reset Password`.
4.  Set a strong temporary password and check the box for **"User must change password at next logon"**.
    *Screenshot:* `![Resetting password for Binh Tran's account](images/T002_2_ResetPassword.png)`

#### FINAL OUTCOME
-   The account was successfully unlocked and the password has been reset.
-   The user was able to log in with the temporary password and set a new personal password.
-   Support ticket `TICKET-002` has been updated to **Resolved**.

#### RESPONSE TO USER
> "Hi Binh, IT has investigated and unlocked your account. We have also reset your password. Please check your personal email (or other designated communication channel) for the temporary password. When you log in again, the system will prompt you to set a new password for yourself. Thank you."