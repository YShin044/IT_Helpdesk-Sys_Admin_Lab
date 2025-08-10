# IT Helpdesk & System Administration Lab
![Project Status](https://img.shields.io/badge/status-ongoing-green)
![Tech](https://img.shields.io/badge/PowerShell-5.1-blue)
![Tech](https://img.shields.io/badge/Windows%20Server-2019-blue)
![Tech](https://img.shields.io/badge/Active%20Directory-Deployed-green)

A hands-on lab environment simulating the IT infrastructure of **MinhTam Company**, a small-to-medium enterprise. This project demonstrates practical skills in system administration, security hardening, and process automation to solve real-world business challenges.

---

## 📖 Project Overview

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
The default AD structure was replaced with a custom, multi-tiered Organizational Unit (OU) design. This logical hierarchy is optimized for granular permission delegation and targeted GPO application.
<img src="https://raw.githubusercontent.com/YShin044/IT_Helpdesk-Sys_Admin_Lab/master/AD_Structure.png" alt="Custom Active Directory OU Structure" width="700" />

### 2. Centralized Management: Policy Enforcement via GPO
Group Policy was leveraged as the primary tool to enforce security standards and deploy configurations across the organization.

| Icon | GPO Name | Business Objective | Detailed Documentation |
| :---: | :--- | :--- | :--- |
| 🛡️ | **Corp - Security Policy** | Enforced a strong password policy & an automatic screen lock to secure endpoints. | [View Docs](./GPO-01-Security-Policy/GPO-01-Security-Policy.md) |
| ⛔ | **Corp - Block USB Devices** | Mitigated data leakage and malware risks by disabling removable storage devices. | [View Docs](./GPO-02-Block-USB/GPO-02-Block-USB.md) |
| 📦 | **Corp - Deploy Python-3.4.3** | Automated the deployment of essential software (Python) to all workstations. | [View Docs](./GPO-03-Deploy-Software/GPO-03-Deploy-Software.md) |
| 🔗 | **KinhDoanh - Map Drive S** | Provided seamless access to departmental data by auto-mapping a network drive. | [View Docs](./GPO-04-Map-Network-Drive/GPO-04-Map-Network-Drive.md) |
| 🌐 | **Corp - Set Default Language** | Chuẩn hóa ngôn ngữ nhập liệu mặc định (US English). | [View Docs](./GPO-05-Set-Default-Language/GPO-05-Set-Default-Language.md) |

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

---

## 🛠️ Technology & Skills Stack
-   **Operating Systems:** Windows Server 2019, Windows 10/11
-   **Core Services:** Active Directory Domain Services (AD DS), DNS
-   **Administration Tools:** Group Policy Management Console, PowerShell ISE
-   **Scripting Language:** **PowerShell 5.1**
-   **Professional Skills:** Technical Writing, Problem Solving, Process Automation, System Design

---

## 🌱 Future Development Roadmap
-   [ ] **File Server & NTFS Permissions:** Implement a dedicated file server with granular, role-based access controls.
-   [ ] **DHCP Server:** Deploy and manage a centralized DHCP service for the network.
-   [ ] **Windows Server Update Services (WSUS):** Centrally manage and deploy Windows updates to all clients.
-   [ ] **Automated Off-boarding Script:** Develop a comprehensive script to fully automate the employee departure process (disable account, archive data, remove group memberships).

---

## 👨‍💻 Author
*   **Name:** Nguyễn Minh Tâm
*   **Email:** minhtam26052b@gmail.com
*   **LinkedIn:** [Nguyen Minh Tam](https://www.linkedin.com/in/minh-t%C3%A2m-a787012b8/)
