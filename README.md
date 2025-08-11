# IT Helpdesk & System Administration Lab
![Project Status](https://img.shields.io/badge/status-ongoing-green)
![Tech](https://img.shields.io/badge/PowerShell-5.1-blue)
![Tech](https://img.shields.io/badge/Windows%20Server-2019-blue)
![Tech](https://img.shields.io/badge/Active%20Directory-Deployed-green)

A hands-on lab environment simulating the IT infrastructure of **MinhTam Company**, a small-to-medium enterprise. This project demonstrates practical skills in system administration, security hardening, and process automation to solve real-world business challenges.

---

## 📖 Project Overview
<p align="center">
<img src="https://github.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/blob/master/Lab_Topology.png" alt="Topology" width="600" />
</p>

This project was designed to move beyond theory and apply system administration principles in a practical setting. The core of the lab is a fully functional Active Directory environment where various policies and automation scripts have been deployed to enhance security, standardize user environments, and improve administrative efficiency.

> **Core Mission:** To build and administer a scalable Active Directory infrastructure for **MinhTam Company**, solving practical challenges related to security, productivity, and IT operations.

### Key Capabilities Demonstrated:
-   **Systematic Design:** Logical and scalable Active Directory architecture.
-   **Problem Solving:** Effective use of Group Policy (GPO) to enforce business rules.
-   **Automation Mindset:** Leveraging PowerShell to eliminate manual, repetitive tasks.
-   **Technical Documentation:** Clear and professional documentation of processes and solutions.

---

## 🚀 Implemented Solutions

### 1. Foundational Design: Active Directory Structure
The default AD structure was replaced with a custom, multi-tiered Organizational Unit (OU) design. This logical hierarchy is optimized for granular permission delegation and targeted GPO application, reflecting best practices for enterprise environments.

```text
📁 _MinhTam Company
├── 🏢 Company
│   ├── 💻 Computers
│   │   ├── 🖥️ Desktops
│   │   └── 💻 Laptops
│   └── 👨‍👩‍👧‍👦 Users
│       ├── 👑 01_BanGiamDoc
│       ├── 📈 02_PhongKinhDoanh
│       ├── 🧾 03_PhongKeToan
│       ├── 📣 04_PhongMarketing
│       ├── 🛠️ 05_PhongIT
│       └── 🚫 DisabledUsers
├── 👤 _AdminAccounts
├── 👥 _Groups
│   ├── 📧 Distribution Groups
│   │   └── DL_All_Staff... (Email lists for departments)
│   └── 🔒 Security Groups
│       ├── SG_Block_USB... (For policy enforcement)
│       └── SG_KinhDoanh_Share... (For resource permissions)
└── ⚙️ _ServiceAccounts
```

### 2. Centralized Management: Policy Enforcement via GPO
Group Policy was leveraged as the primary tool to enforce security standards and deploy configurations across the organization.

| Icon | GPO Name | Business Objective | Detailed Documentation |
| :---: | :--- | :--- | :--- |
| 🛡️ | **Corp - Security Policy** | Enforced a strong password policy & an automatic screen lock to secure endpoints. | [View Docs](./GPO-01-Security-Policy/GPO-01-Security-Policy.md) |
| ⛔ | **Corp - Block USB Devices** | Mitigated data leakage and malware risks by disabling removable storage devices. | [View Docs](./GPO-02-Block-USB/GPO-02-Block-USB.md) |
| 📦 | **Corp - Deploy Python-3.4.3** | Automated the deployment of essential software (Python) to all workstations. | [View Docs](./GPO-03-Deploy-Software/GPO-03-Deploy-Software.md) |
| 🔗 | **KinhDoanh - Map Drive S** | Provided seamless access to departmental data by auto-mapping a network drive. | [View Docs](./GPO-04-Map-Network-Drive/GPO-04-Map-Network-Drive.md) |
| 🌐 | **Corp - Set Default Language** | Ensures a consistent user experience by setting the default input method to English (US). | [View Docs](./GPO-05-Set-Default-Language/GPO-05-Set-Default-Language.md) |

### 3. Efficiency & Automation: The Power of PowerShell
Scripts were developed to solve time-consuming and error-prone administrative tasks.

*   **Scenario 1: New Employee On-boarding (`Create-NewUsers.ps1`)**
    > **Problem:** Manually creating user accounts is time-consuming and leads to inconsistent naming conventions and permissions.
    > **Solution:** A robust PowerShell script that reads from a CSV file to bulk-create standardized user accounts, featuring built-in conflict detection to prevent duplicates.
    >
    > 📄 **View Script & Guide:** [`/Script_Create-NewUsers/Create-NewUsers.md`](./Script_Create-NewUsers/Create-NewUsers.md)

*   **Scenario 2: Security Auditing (`Find-InactiveUsers.ps1`)**
    > **Problem:** Stale, unused accounts ("ghost accounts") are a significant and often overlooked security liability.
    > **Solution:** An automated script that scans the entire domain for accounts inactive for over 90 days and exports a detailed CSV report for administrative review and action.
    >
    > 📄 **View Script & Guide:** [`/Script_Find-InactiveUsers/Find-InactiveUsers.md`](./Script_Find-InactiveUsers/Find-InactiveUsers.md)

### 4. Helpdesk Scenarios

To transform this lab into a dynamic, hands-on environment, I have documented common Helpdesk issues following standard operating procedures. Each scenario is logged as a realistic support ticket.

*   **TICKET-001: User Cannot Write to a Shared Drive**<br>[ `Tiếng Việt`](./_scenarios_Ticket/Vietnamese/TICKET-001_Permission_Denied.md) | [ `English` ](./_scenarios_Ticket/English/TICKET-001_Permission_Denied.md)

*   **TICKET-002: User Account Locked Out**<br>[ `Tiếng Việt`](./_scenarios_Ticket/Vietnamese/TICKET-002_Account_Locked_Out.md) | [ `English` ](./_scenarios_Ticket/English/TICKET-002_Account_Locked_Out.md)

*   **TICKET-003: New Employee Onboarding Process**<br>[ `Tiếng Việt`](./_scenarios_Ticket/Vietnamese/TICKET-003_New_Employee_Onboarding.md) | [ `English` ](./_scenarios_Ticket/English/TICKET-003_New_Employee_Onboarding.md)

---

## 🛠️ Technology & Skills Stack
-   **Operating Systems:** Windows Server 2019, Windows 10/11
-   **Core Services:** Active Directory Domain Services (AD DS), DNS
-   **Administration Tools:** Group Policy Management Console, PowerShell ISE
-   **Scripting Language:** PowerShell 5.1
-   **Professional Skills:** Technical Writing, Problem Solving, Process Automation, System Design

---

## 🌱 Future Development Roadmap

This project serves as a solid foundation. The next logical steps to evolve this lab into a more comprehensive enterprise environment include:

-   [ ] **Implement Core Network Services:** Deploy and manage a centralized DHCP server to handle IP address allocation and a WSUS server to control the deployment of Windows updates to all clients.
-   [x] **File Server & Granular Permissions:** Establish a dedicated File Server, create departmental shares, and apply granular NTFS permissions to enforce role-based access control (RBAC).
-   [ ] **Automate the Full Employee Lifecycle:** Develop a comprehensive PowerShell Off-boarding script to handle employee departures, including disabling the account, archiving data, removing group memberships, and converting the mailbox.
-   [ ] **Establish Hybrid Identity:** Integrate the on-premises Active Directory with Azure Active Directory using Azure AD Connect, enabling a foundational hybrid cloud environment and preparing for modern management.
-   [ ] **Advanced Security Policies:** Implement more advanced GPOs, such as Folder Redirection for user profiles and AppLocker to restrict unauthorized software execution.

---

## 👨‍💻 Author
*   **Name:** Nguyễn Minh Tâm
*   **Email:** minhtam26052b@gmail.com
*   **LinkedIn:** [Nguyen Minh Tam](https://www.linkedin.com/in/minh-t%C3%A2m-a787012b8/)
