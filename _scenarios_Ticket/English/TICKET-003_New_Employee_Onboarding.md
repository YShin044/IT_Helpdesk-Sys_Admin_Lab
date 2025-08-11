### TICKET-003: New Employee Onboarding Process
- **Ticket ID:** TICKET-003
- **Title:** [Request] Create account for new employee - Long Pham
- **Requester:** Human Resources Department
- **Affected Systems:** Active Directory, File Server

#### REQUEST DESCRIPTION
The HR department has submitted a request to create an account for a new employee with the following details:
*   **Full Name:** Long Pham
*   **Department:** IT
*   **Position:** IT Helpdesk
*   **Start Date:** [Today's Date]

#### ANALYSIS & INVESTIGATION
This is a standard Service Request, not an incident. It must be executed following the company's standard onboarding procedure.
1.  **Naming Convention:** `department.lastnamefirstnameinitial` -> `it.longp`.
2.  **OU Placement:** The account will be created in the `IT` OU.
3.  **Access Rights:** Needs to be added to the following groups:
    *   `SG_IT_Users`: General group for all IT staff.
    *   `SG_IT_Share_Modify`: Grants access to the IT department's shared folder.

#### RESOLUTION & ACTIONS
1.  **Create Account:** In `ADUC`, navigate to the `IT` OU and create a new user with the analyzed information.
2.  Set a temporary password and check the box for **"User must change password at next logon"**.
    *Screenshot:* `![Creating the it.longp user account](images/T003_1_CreateUser.png)`
3.  **Assign Group Membership:** Open the properties for `it.longp`, go to the "Member Of" tab, and add the user to the `SG_IT_Users` and `SG_IT_Share_Modify` groups.
    *Screenshot:* `![Assigning groups to the it.longp account](images/T003_2_AddToGroups.png)`
4.  **Create Personal Folder (Optional):** Run a script to create a personal home folder on the File Server and assign permissions.

#### FINAL OUTCOME
-   The `it.longp` account has been successfully created and configured.
-   Login credentials have been generated and sealed in an envelope for delivery to the HR department.
-   Support ticket `TICKET-003` has been updated to **Completed**.

#### RESPONSE TO USER (Human Resources Dept.)
> "Hi HR Team, The IT Department has completed the request to create an account for the new employee, Long Pham (username: `it.longp`). The login credentials have been sealed and will be sent to your department for hand-off. Thank you."