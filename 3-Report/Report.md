Internal Active Directory Security Assessment – Enterprise Environment
AuraxTech Internal Network
Prepared by: Sam
Assessment Type: Internal Active Directory Security Assessment
Environment: Custom Enterprise Active Directory (Self-Designed)
Date: 12/01/2026

1. Executive Summary
This assessment evaluated the security posture of a custom-built enterprise Active Directory environment designed to reflect real-world corporate operations. The objective was to assess identity architecture, administrative trust relationships, and inherent internal attack surfaces that could be leveraged by an attacker with internal network access.
The environment was engineered from the ground up and includes multiple servers, workstations, organizational units, users, security groups, and service accounts. Rather than relying on preconfigured labs, all components were manually designed to mirror realistic enterprise identity and access management practices.
The assessment identified several high-impact attack surfaces, including Kerberos service account exposure, weak privilege boundaries, and centralized administrative trust through Group Policy. When combined, these conditions could enable privilege escalation, lateral movement, and full domain compromise.
This report documents the enterprise architecture, security assessment methodology, identified risks, and remediation guidance.

2. Scope & Methodology
2.1 Scope
The assessment included the following systems and components:
•	Active Directory Domain Services
•	DNS integrated with Active Directory
•	Domain Controller (DC01)
•	File Server (FS01)
•	Web / Application Server (WEB01)
•	Management Server (MGMT01)
•	Employee Workstation (EMP01)
•	Organizational Units, users, groups, and service accounts

2.2 Methodology
The assessment followed a standard internal security assessment approach:
1.	Enterprise environment review
2.	Identity and access architecture analysis
3.	Administrative trust and privilege boundary review
4.	Attack surface identification
5.	Impact and risk assessment
6.	Remediation planning
This approach mirrors real-world internal penetration testing and Active Directory security reviews.

3. Enterprise Environment Overview
3.1 Domain Architecture
•	Domain Name: corp.local
•	Authentication: Kerberos
•	Directory Services: Active Directory Domain Services
•	Name Resolution: Integrated DNS
•	Centralized Management: Group Policy
Figure 1 – Domain Controller with Active Directory Services
(Screenshot showing DC01 with Server Manager and AD DS installed)
Figure 2 – DNS Integrated with Active Directory
(Screenshot of DNS Manager showing corp.local forward lookup zone)

3.2 Host Roles and Network Design
The environment was designed as a multi-host enterprise network with clear role separation.
Host	Role
DC01	Domain Controller, DNS, authentication authority
FS01	Centralized file services
WEB01	Internal web/application services
MGMT01	Administrative and management services
EMP01	Employee workstation
Figure 3 – Enterprise Host Inventory
(Screenshot of virtualization platform showing all enterprise systems)
Figure 4 – Internal Network Configuration
(Screenshot of network adapter configuration or ipconfig output)

3.3 Organizational Unit Structure
A structured Organizational Unit hierarchy was implemented to reflect corporate departments and operational boundaries.
Top-Level OU: AuraxTech
Sub-OUs include:
•	HR
•	Development
•	Finance
•	IT
•	Servers
•	Workstations
•	Groups
•	Service Accounts
Figure 5 – Active Directory Organizational Unit Hierarchy
(Screenshot of ADUC displaying the full OU structure)

4. Identity & Access Architecture
4.1 User Accounts
Multiple user accounts were created to represent standard business roles across departments such as HR, Development, Finance, and IT.
Figure 6 – Departmental User Accounts
(Screenshot showing users placed within departmental OUs)

4.2 Security Groups
Role-based security groups were implemented to define administrative responsibility and access control.
Examples include:
•	Server-Admins
•	Workstation-Admins
•	Web-Service-Admins
•	Backup-Operators
Figure 7 – Enterprise Security Groups
(Screenshot of Groups OU listing role-based security groups)
Figure 8 – Security Group Membership Configuration
(Screenshot of group properties showing assigned members)

4.3 Service Accounts
Dedicated service accounts were deployed to support internal applications and services.
•	svc-web – Web application service account
•	Service Principal Name (SPN) configured for Kerberos authentication
Figure 9 – Service Account Configuration
(Screenshot of svc-web account in Service Accounts OU)
Figure 10 – Kerberos SPN Configuration
(Screenshot of SPN configuration via setspn or Attribute Editor)

5. Attack Surface Assessment & Findings
Finding 1: Kerberos Service Account Exposure
Risk Rating: High
Service accounts configured with Kerberos Service Principal Names introduce exposure to service ticket abuse. If service account passwords are weak or reused, an attacker could obtain Kerberos tickets and perform offline password attacks.
Impact:
Compromise of service credentials could allow escalation of privileges, application compromise, and lateral movement.
Figure 11 – Kerberos Service Account Exposure
(Screenshot showing SPN-associated service account)

Finding 2: Weak Privilege Boundaries
Risk Rating: High
Administrative responsibilities are distributed across multiple security groups and organizational units. While this reflects real enterprise design, misconfigured group memberships and delegated rights can allow attackers to escalate privileges through trust relationships.
Impact:
Unauthorized elevation of privileges and access to sensitive systems.
Figure 12 – Administrative Group Relationships
(Screenshot showing administrative groups and memberships)
Figure 13 – Privilege Placement Within OUs
(Screenshot showing users/computers placed in IT or Server OUs)

Finding 3: Centralized Group Policy Trust
Risk Rating: Medium–High
Centralized Group Policy management introduces implicit trust across systems. Improperly scoped or over-permissioned policies can be abused to gain elevated access or move laterally across the environment.
Impact:
Workstation and server compromise through policy abuse.
Figure 14 – Group Policy Management Console
(Screenshot of GPMC showing domain policies)
Figure 15 – Group Policy Linked to Organizational Units
(Screenshot of GPO linkage and scope)

6. Impact Assessment
If the identified weaknesses were exploited together, an attacker with internal access could:
•	Escalate privileges within the domain
•	Move laterally between servers and workstations
•	Gain domain-level administrative control
•	Access sensitive enterprise data
•	Maintain long-term persistence

7. Remediation Recommendations
•	Enforce strong, unique passwords for all service accounts
•	Minimize SPN usage where not required
•	Apply least-privilege principles to security groups
•	Regularly audit group memberships and delegated rights
•	Harden Group Policy permissions and scope
•	Monitor authentication and privilege escalation events

8. Conclusion
This assessment demonstrated that a realistically designed enterprise Active Directory environment can contain multiple high-impact internal attack surfaces if identity and access controls are not carefully managed.
By reviewing the architecture, trust relationships, and administrative design, this engagement highlights how common enterprise misconfigurations can be chained to achieve severe security impact, including full domain compromise.
The environment provides a strong foundation for continued internal security testing, attack simulation, and remediation validation.

 j
