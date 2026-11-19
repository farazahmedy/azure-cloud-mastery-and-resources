# 📜 Enterprise Azure Policy & Governance Guide

Azure Policy enforces organizational standards and assesses compliance at scale across Management Groups, Subscriptions, and Resource Groups.

---

## 🏛️ Governance Hierarchy

```
[ Root Management Group (Tenant) ]
             |
   +---------+---------+
   |                   |
[ Platform ]      [ Landing Zones ]
   |                   |
   +-- Identity        +-- Corp
   +-- Management      +-- Online
   +-- Connectivity
```

---

## 🎯 Top Must-Have Azure Policies

### 1. Allowed Deployment Locations (Geographical Restriction)
Ensures resources are created only in approved data regions to comply with data residency and GDPR regulations.
- **Effect**: `Deny`
- **Allowed Regions**: `["eastus", "westus", "centralindia", "westeurope"]`

### 2. Mandatory Resource Tagging
Enforces that every resource and resource group possesses required metadata tags (`Environment`, `Owner`, `CostCenter`, `Project`).
- **Effect**: `Deny` on creation if tags are missing, or `Modify` to inherit tags from parent resource group.

### 3. Restrict Public IP Addresses on Virtual Machines
Blocks provisioning of direct Public IP addresses on VMs in spoke networks.
- **Effect**: `Deny`

### 4. Require Secure Transfer (HTTPS) & TLS 1.2 on Storage Accounts
Ensures all storage accounts enforce encrypted transport and modern cipher suites.
- **Effect**: `Deny`

### 5. Enforce Disk Encryption & Key Vault Purge Protection
Prevents accidental permanent deletion of cryptographic keys and compliance breaches.
- **Effect**: `AuditIfNotExists` or `Deny`
