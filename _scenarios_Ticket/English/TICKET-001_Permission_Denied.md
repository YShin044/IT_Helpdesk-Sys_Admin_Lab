### TICKET-001: Cannot Write to Shared Drive
- **Ticket ID:** TICKET-001
- **Title:** User cannot save files to S: drive
- **Requester:** An Nguyen - Sales Department
- **Affected System:** File Server (`\\minhtam.server\Shares\Sales`)

#### INCIDENT DESCRIPTION
> "Hi IT, I can open and view files in the Sales department's S: drive, but when I try to create a new file or save an edited one, the system returns a 'Permission Denied' error. Could you please check this for me?"

#### ANALYSIS & INVESTIGATION
1.  **Check Group Membership:** Opened `Active Directory Users and Computers` (ADUC), located the user account `sales.annguyen`. Checked the "Member Of" tab.
2.  **Finding:** The user is only a member of the `SG_Sales_Share_Read` group. The user is not a member of the `SG_Sales_Share_Modify` group.
3.  **Validate Permissions:** Checked the NTFS permissions on the `\\minhtam.server\Shares\Sales` shared folder, confirming that the `SG_Sales_Share_Modify` group has the correct `Modify` permissions.

#### ROOT CAUSE
Due to an oversight during the onboarding process, the user's account was not added to the security group that grants write permissions (`Modify`), resulting in read-only access.

#### RESOLUTION & ACTIONS
1.  In `ADUC`, add the `sales.annguyen` account to the `SG_Sales_Share_Modify` security group.
2.  Instruct the user to **Sign out and Sign back in** to allow the system to refresh their access token.

#### FINAL OUTCOME
-   The user can now successfully read and write to the S: drive as expected.
-   Support ticket `TICKET-001` has been updated to **Resolved**.

#### RESPONSE TO USER
> "Hi An, IT has investigated the issue and identified a problem with your account's access rights. We have now updated your permissions. Please **sign out and sign back in** for the changes to take effect. After logging back in, you should be able to save files to the S: drive normally. Thank you."