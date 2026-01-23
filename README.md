# Hybrid Identity Lab — Active Directory & Microsoft Entra ID

## 📌 Project Overview
This project demonstrates the design, implementation, and validation of a **hybrid Identity and Access Management (IAM)** environment integrating on-premises Active Directory with Microsoft Entra ID using Azure AD Connect.

The lab simulates a real-world enterprise identity architecture where identities are managed on-premises and securely authenticated in the cloud using modern authentication controls.

---

## 🎯 Objectives
- Deploy an on-prem Active Directory Domain Services (AD DS) environment
- Synchronize identities to Microsoft Entra ID using Azure AD Connect
- Enforce secure authentication with Multi-Factor Authentication (MFA)
- Automate user provisioning with PowerShell
- Monitor authentication and identity changes using Entra ID logs

---

## 🏗 Architecture Overview

```text
┌────────────────────────────┐
│          End User          │
│     Password + MFA Login   │
└─────────────┬──────────────┘
              │
              ▼
┌────────────────────────────┐
│     Microsoft Entra ID     │
│  • Authentication          │
│  • MFA Enforcement         │
│  • Conditional Access      │
│  • Sign-In Logs            │
│  • Audit Logs              │
└─────────────▲──────────────┘
              │ Identity Sync
              │ (Password Hash Sync)
┌─────────────┴──────────────┐
│    Azure AD Connect        │
│  • Initial Sync            │
│  • Delta Sync              │
│  • Scheduler               │
└─────────────▲──────────────┘
              │ Authoritative Source
              │
┌─────────────┴──────────────┐
│  On-Prem Active Directory  │
│  • AD DS                   │
│  • DNS                     │
│  • Users / Groups / OUs    │
│  • PowerShell Automation   │
└────────────────────────────┘
```


- Active Directory serves as the authoritative identity source
- Azure AD Connect synchronizes identities to the cloud
- Microsoft Entra ID handles authentication, MFA, and logging

---
## ⭐ Top 5 Evidence

1. [Azure AD Connect Installed Successfully](screenshots/microsoft-ad-connect-installed.png)  
   *Confirms successful deployment of Azure AD Connect and hybrid identity integration.*

2. [Users Synced to Microsoft Entra ID](screenshots/users-synced-to-entraid.png)  
   *Demonstrates on-prem Active Directory users synchronized to the cloud with correct UPNs.*

3. [Sign-In Log — MFA Success](screenshots/sign-in-MFA-log.png)  
   *Validates secure authentication using password + Multi-Factor Authentication.*

4. [Audit Log — Directory Sync Verified](screenshots/audit-log-directory-sync-verified.png)  
   *Shows directory synchronization activity recorded in Entra ID audit logs.*

5. [PowerShell User Provisioning Output](screenshots/powershell-user-provisioning.png)  
   *Proves automated user, OU, and group provisioning using PowerShell.*


## 🖥 Environment

### On-Prem (Virtualized)
- Windows Server 2025
- Active Directory Domain Services (AD DS)
- DNS
- Azure AD Connect
- VMware Workstation (NAT networking)
- Powershell

### Virtual Machine Configuration

| Setting | Value |
|-------|-------|
| VM Name | Kalypton-dc1 |
| OS | Windows Server 2025 |
| CPU | 4 vCPU |
| RAM | 8 GB |
| Disk | 80 GB |
| Network | VMnet8 (NAT) |
| Subnet | 10.0.0.0/24 |

### Cloud
- Microsoft Entra ID (Workforce tenant)
- Entra ID domain: `kalytpn.onmicrosoft.com` 
- Microsoft Entra ID (Conditional Access)

---

## 🔧 Implementation Phases

### Phase 1 — Active Directory Foundation
- Installed AD DS and DNS
- Promoted server to Domain Controller
- Created structured Organizational Units (OUs)
- Standardized naming conventions and UPN suffixes

---

### Phase 2 — Identity Automation (PowerShell)
- Created superhero-themed OUs and security groups
- Automated user creation using PowerShell
- Enforced:
  - `firstname.lastname` naming convention
  - Group-based access
  - Non-expiring passwords (lab-safe)
- Script outputs each created object for validation and troubleshooting

---

### Phase 3 — Microsoft Entra ID Tenant Setup
- Created a workforce Microsoft Entra ID tenant
- Verified custom domain (`kalytpon.com`) - *did not use for project*
- Enabled sign-in and audit logging
- Prepared tenant for hybrid synchronization

---

### Phase 4 — Azure AD Connect
- Installed Azure AD Connect on the Domain Controller
- Configured Password Hash Synchronization
- Verified initial and delta synchronization cycles
- Confirmed users synchronized with correct UPNs

---

### Phase 5 — Authentication & MFA
- Enabled Microsoft Entra ID Security Defaults
- Enforced MFA for all users and administrators
- Tested first-time MFA registration
- Validated successful cloud authentication

---

### Phase 6 — Monitoring & Logging
- Reviewed Microsoft Entra ID sign-in logs
- Verified MFA success and authentication methods
- Reviewed audit logs for directory synchronization activity
- Simulated failed sign-ins to understand troubleshooting patterns

---

### Phase 7 — Final Validation
- Verified end-to-end authentication flow
- Confirmed Azure AD Connect synchronization health
- Captured evidence screenshots
- Finalized documentation and automation scripts

---
## 🖼 Evidence & Quick Links

### 🏗 Active Directory Structure (On-Prem)
- [Domain Users OU](screenshots/dc-users.png) — Shows standard user accounts organized in on-prem Active Directory.
- [Domain Admins OU](screenshots/dc-admins.png) — Demonstrates separation of privileged accounts from standard users.
- [Security Groups](screenshots/groups.png) — Confirms role-based security groups used for access management.
- [Marvel Users OU](screenshots/marvel-users.png) — Example of structured OU design for delegated administration.
- [Marvel Admins OU](screenshots/marvel-admins.png) — Shows admin account isolation following least-privilege principles.

---

### ⚙ Identity Automation (PowerShell)
- [PowerShell User Provisioning Output](screenshots/powershell-user-provisioning.png) — Verifies automated user, OU, and group creation with visible script output.
- [PowerShell Sync Trigger Verified](screenshots/powershell-sync-verified.png) — Confirms manual synchronization trigger and Azure AD Connect scheduler status.

---

### ☁ Microsoft Entra ID — Tenant & Overview
- [Entra ID Tenant Overview](screenshots/Entra-Id-Overview.png) — Shows Microsoft Entra ID tenant configuration and readiness for hybrid identity.
- [Users Synced to Entra ID](screenshots/users-synced-to-entraId.png) — Confirms on-prem Active Directory users successfully synchronized to Entra ID.
- [On-Prem Groups Synced to Entra ID](screenshots/onprem-groups-synced-to-entraid.png) — Demonstrates group objects syncing from on-prem AD to the cloud.

---

### 🔄 Azure AD Connect
- [Azure AD Connect Installed Successfully](screenshots/microsoft-ad-connect-installed.png) — Confirms successful Azure AD Connect installation and configuration.
- [Audit Logs Before Sync](screenshots/audit-logs-before-sync.png) — Establishes baseline audit state prior to directory synchronization.
- [Audit Log — Directory Sync Verified](screenshots/audit-log-directory-sync-verified.png) — Verifies directory synchronization events generated by Azure AD Connect.

---

### 🔐 Authentication & MFA
- [MFA Policy Configuration](screenshots/MFA-policy.png) — Shows MFA enforcement configuration within Microsoft Entra ID.
- [MFA Policy (Additional View)](screenshots/MFA-policy2.png) — Confirms MFA policy scope and enforcement settings.
- [Testing Sign-In with MFA (Step 1)](screenshots/testing-sign-on-mfa1.png) — Initial user sign-in triggering MFA registration.
- [Testing Sign-In with MFA (Step 2)](screenshots/testing-sign-on-mfa2.png) — MFA setup and verification process.
- [Testing Sign-In with MFA (Step 3)](screenshots/testing-sign-on-mfa3.png) — MFA challenge presented during authentication.
- [Testing Sign-In with MFA (Step 4)](screenshots/testing-sign-on-mfa4.png) — Successful MFA approval by the user.
- [Testing Sign-In with MFA (Step 5)](screenshots/testing-sign-on-mfa5.png) — Completion of secure authentication workflow.
- [Testing Sign-In with MFA (Step 6)](screenshots/testing-sign-on-mfa6.png) — Post-authentication confirmation.
- [Testing Sign-In with MFA (Step 7)](screenshots/testing-sign-on-mfa7.png) — Continued validation of MFA enforcement.
- [Testing Sign-In with MFA (Step 8)](screenshots/testing-sign-on-mfa8.png) — Final confirmation of successful MFA-protected sign-in.

---

### 📊 Monitoring & Logging
- [Sign-In Logs Before Sync](screenshots/sign-in-logs-before-sync.png) — Baseline sign-in activity prior to hybrid identity integration.
- [Sign-In Logs Filtered](screenshots/sign-in-logs-filtered.png) — Demonstrates filtering and analysis of authentication events.
- [Sign-In Log — MFA Success](screenshots/sign-in-MFA-log.png) — Confirms successful password and MFA authentication.
- [Sign-In Log — Failed Attempt (Simulated)](screenshots/sign-in-log-failed-simulated-attempt.png) — Shows failed authentication attempt used for troubleshooting practice.
- [Recent Audit Logs](screenshots/recent-audit-logs.png) — Demonstrates ongoing visibility into identity and configuration changes.

---

## 📊 Results
- Users successfully synchronized from on-prem AD to Microsoft Entra ID
- MFA enforced for all cloud authentication
- Authentication and identity changes fully auditable
- Identity provisioning automated via PowerShell
- Hybrid identity validated end-to-end

---

## 📘 Lessons Learned
- DNS and UPN alignment are critical for hybrid identity success
- Azure AD Connect depends heavily on identity hygiene
- MFA enforcement must be validated through logs, not assumptions
- Automation improves consistency and reduces human error
- IAM monitoring is as important as configuration
- Confirm policies are enabled instead of "Report Only"
- During teardown, on-prem Active Directory objects were removed successfully; however, Azure AD Connect export deletion protection prevented automatic removal of cloud identities after large-scale OU deletion. Remaining Entra ID objects were manually cleaned up, reflecting standard decommissioning procedures when hybrid sync scope changes.


---

## 🧠 Skills Demonstrated
- Hybrid identity architecture
- Active Directory administration
- Azure AD Connect configuration
- Microsoft Entra ID tenant management
- Multi-Factor Authentication (MFA)
- IAM monitoring and audit analysis
- PowerShell automation

---

📈 Lab Scale & Enhancements

## This lab was expanded beyond basic hybrid identity demonstrations to reflect enterprise-scale identity operations:

- 750 unique user accounts (validated, no duplicates)
- 60+ Organizational Units (OUs) with hierarchical structure
- 150+ security groups supporting role-based access models
- Automatic domain DN detection (no hardcoded LDAP paths)
- Microsoft Entra ID sync awareness built into teardown logic
- Comprehensive error handling with safe exits and validation
- Progress tracking and structured logging for long-running scripts
- Reusable prompt templates for custom user and OU generation
- Complete documentation suite supporting rebuild and review

---

## 🚀 Future IAM Lab Enhancements (Roadmap)

The following checklist outlines planned extensions to this project to deepen IAM capabilities and align with enterprise identity requirements.

### 🔐 Authentication & Federation
- [x] Implement **SAML-based Single Sign-On (SSO)** for a SaaS application - completed 1/22/26   
  *Skills: SAML, federation, claims mapping, SaaS integration*
- [x] Configure **[OAuth 2.0 / OpenID Connect (OIDC)](https://github.com/ryanbynoe/hybrid-identity-iam/blob/main/enhancements/OauthOIDC/Oauth.md)** application authentication  
  *Skills: OAuth flows, token-based authentication, modern identity protocols* - completed 1/22/26

### 🛡 Access Control & Zero Trust
- [x] Create **Conditional Access policies** (MFA enforcement, legacy auth blocking) completed 1/21/26  
  *Skills: Conditional Access, Zero Trust principles*
- [x] Implement **Privileged Identity Management (PIM)** with just-in-time role elevation - completed 1/22/26
  *Skills: Privileged access, least privilege, role lifecycle management*

### 🔁 Identity Governance (IGA)
- [ ] Configure **Access Reviews** for groups and privileged roles  
  *Skills: Identity governance, compliance, access certification*
- [ ] Simulate **joiner / mover / leaver** identity lifecycle workflows  
  *Skills: IGA processes, lifecycle management*

### 🤖 Automation & Provisioning
- [ ] Extend automation to **CSV- or HR-driven user provisioning**  
  *Skills: Identity lifecycle automation, data-driven provisioning*
- [ ] Integrate **Microsoft Graph API** for cloud-based identity automation  
  *Skills: API-based IAM automation*

### 👑 Non-Human & Service Identities
- [ ] Implement **service accounts / app registrations** with scoped permissions  
  *Skills: Non-human identities, credential management*
- [ ] Manage **secrets and certificates** for applications securely  
  *Skills: Credential lifecycle, security best practices*

### 📊 Monitoring, Troubleshooting & Incidents
- [ ] Simulate and document **authentication failures** (MFA, sync, token issues)  
  *Skills: IAM troubleshooting, root cause analysis*
- [ ] Create **incident-style investigations** using Entra ID logs  
  *Skills: Log analysis, IAM incident response*

### 🔐 PKI & Advanced Security (Optional)
- [ ] Deploy **Active Directory Certificate Services (AD CS)**  
  *Skills: PKI, certificates, SSL/TLS*
- [ ] Implement **certificate-based authentication** scenarios  
  *Skills: Digital trust, strong authentication*

---

*This roadmap reflects a structured approach to expanding IAM expertise, covering authentication protocols, access control, governance, automation, and security monitoring commonly required in enterprise environments.*
