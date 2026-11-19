# 🛡️ CIS Microsoft Azure Foundations Benchmark Hardening Checklist

Production baseline security controls aligned with the **CIS Microsoft Azure Foundations Benchmark v2.0**.

---

## 🔑 1. Identity and Access Management (IAM)

- [ ] **1.1 Multi-Factor Authentication (MFA)**: Enforce MFA for all privileged users (Global Administrators, Subscription Owners, Contributors) using Microsoft Entra Conditional Access.
- [ ] **1.2 Deprecate Permanent Privileged Roles**: Enforce Just-In-Time (JIT) access using Entra Privileged Identity Management (PIM) with maximum 8-hour activation windows.
- [ ] **1.3 Limit External / Guest Users**: Restrict guest user invite permissions to designated admins only.
- [ ] **1.4 Block Legacy Authentication**: Disable basic authentication protocols (POP3, IMAP, SMTP) vulnerable to password spraying attacks.

---

## 💾 2. Storage Accounts

- [ ] **2.1 Disallow Public Blob Access**: Ensure `allowBlobPublicAccess = false` on every storage account.
- [ ] **2.2 Require Secure Transfer (HTTPS)**: Ensure `supportsHttpsTrafficOnly = true`.
- [ ] **2.3 Minimum TLS Version 1.2**: Ensure `minimumTlsVersion = "TLS1_2"`.
- [ ] **2.4 Infrastructure Encryption**: Enable double encryption for highly sensitive datasets.
- [ ] **2.5 Soft Delete & Versioning**: Enable 14+ day soft delete on blobs and containers to safeguard against ransomware.

---

## 🌐 3. Networking & Perimeter Defense

- [ ] **3.1 Restrict RDP / SSH Access**: Deny inbound RDP (port 3389) and SSH (port 22) from the internet (`0.0.0.0/0`) on all NSGs. Enforce Azure Bastion.
- [ ] **3.2 Hub-and-Spoke Traffic Inspection**: Route all inter-spoke and outbound traffic through Azure Firewall or certified NVA.
- [ ] **3.3 Enable Network Watcher Flow Logs**: Export NSG flow logs to Log Analytics with Traffic Analytics enabled.
- [ ] **3.4 Enforce Private Endpoints**: Provision Private Link for all PaaS services (Azure SQL, Cosmos DB, Key Vault, Storage).

---

## 🖥️ 4. Virtual Machines & Compute

- [ ] **4.1 OS & Data Disk Encryption**: Enforce Azure Disk Encryption (ADE) with Customer-Managed Keys (CMK) in Azure Key Vault.
- [ ] **4.2 Enable Automated Patching**: Configure Azure Update Manager for monthly security patch maintenance windows.
- [ ] **4.3 Microsoft Defender for Servers**: Enable Defender for Cloud Plan 2 for behavioral runtime threat detection and file integrity monitoring.
