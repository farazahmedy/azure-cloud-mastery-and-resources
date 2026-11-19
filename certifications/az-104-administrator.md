# 📘 AZ-104: Microsoft Azure Administrator Associate Study Guide

The AZ-104 exam validates technical skills required to implement, manage, and monitor an organization’s Microsoft Azure environment, covering virtual networks, storage, compute, identity, security, and governance.

---

## 🎯 Exam Domain Breakdown

1. **Manage Azure Identities and Governance (20–25%)**
2. **Implement and Manage Storage (15–20%)**
3. **Deploy and Manage Azure Compute Resources (20–25%)**
4. **Implement and Manage Virtual Networking (20–25%)**
5. **Monitor and Maintain Azure Resources (10–15%)**

---

## 🔑 1. Azure Identities & Governance

### Microsoft Entra ID
- **Users & Groups**: Dynamic membership rules (e.g., `user.department -eq "Sales"`).
- **Administrative Units (AUs)**: Delegate admin control over a subset of users or groups.
- **Self-Service Password Reset (SSPR)**: Configuration, authentication methods, writeback to on-prem AD.
- **External Identities**: B2B (guest user collaboration) and B2C (customer identity management).

### RBAC & Azure Policy
- **Custom RBAC Roles**: Created using JSON specifying `Actions`, `NotActions`, `DataActions`, and `AssignableScopes`.
- **Azure Policy**:
  - Evaluation stages: `Disabled`, `Append`, `Audit`, `Deny`, `DeployIfNotExists`, `Modify`.
  - Remediation tasks for non-compliant resources.
- **Resource Locks**: Take precedence over RBAC permissions (even Subscription Owners cannot delete a resource locked with `CanNotDelete`).

---

## 💾 2. Implement & Manage Storage

### Azure Storage Accounts
- **Account Types**: Standard General-purpose v2, Premium Block Blobs, Premium Page Blobs, Premium File Shares.
- **Redundancy Options**:
  - **LRS (Locally Redundant)**: 3 copies within a single datacenter (11 9s durability).
  - **ZRS (Zone Redundant)**: 3 copies across 3 availability zones in the primary region (12 9s).
  - **GRS (Geo-Redundant)**: LRS in primary region + LRS in secondary paired region (16 9s).
  - **GZRS (Geo-Zone-Redundant)**: ZRS in primary region + LRS in secondary region (16 9s).
  - **RA-GRS / RA-GZRS**: Read access to the secondary replica.

### Blob Lifecycle Management
- Automated rule-based tiering: Move to `Cool` after 30 days, `Archive` after 90 days, delete after 365 days.
- **Rehydration**: Moving archive blobs back to hot/cool: Standard (up to 15 hours) or High Priority (under 1 hour).

### Azure Files & Azure File Sync
- Multi-protocol shares (SMB 3.0 / NFS).
- **Azure File Sync**: Centralizes file shares in Azure while keeping local cache on Windows Server.
  - Storage Sync Service, Sync Groups, Cloud Endpoints, Server Endpoints, and Cloud Tiering.

---

## 💻 3. Deploy & Manage Azure Compute

### Virtual Machines & Scale Sets
- **Availability Sets**: Fault Domains (FDs - shared power/switch, max 3) and Update Domains (UDs - rebooted together during maintenance, max 20).
- **Virtual Machine Scale Sets (VMSS)**: Horizontal auto-scaling based on CPU/RAM metrics or schedules. Flexible orchestration vs. Uniform.
- **Run Command & Custom Script Extensions**: Automated post-deployment configuration.

### Containers & App Services
- **Azure App Service**:
  - App Service Plans (Free, Basic, Standard, Premium, Isolated).
  - Deployment Slots: Zero-downtime traffic switching (swap slot), auto-swap, testing in staging.
- **Azure Container Instances (ACI)**: Fast, serverless container startup without managing VMs.
- **Azure Kubernetes Service (AKS)**:
  - Node pools (System vs. User), Azure CNI vs. Kubenet networking, Azure Key Vault Secrets Store CSI Driver.

---

## 🌐 4. Virtual Networking (The Core of AZ-104)

### VNets & Subnets
- Private IP addressing (RFC 1918: `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`).
- Azure reserves 5 IP addresses per subnet:
  - `.0`: Network address.
  - `.1`: Default gateway.
  - `.2`, `.3`: Azure DNS mapping.
  - `.255`: Network broadcast address.

### Virtual Network Peering
- Links two VNets with low-latency private Microsoft backbone traffic.
- Non-transitive: If VNet A peers with B, and B peers with C, A cannot communicate with C without an intermediate router/firewall (NVA) and UDRs.
- `Allow gateway transit` and `Use remote gateways` for hub-and-spoke connectivity.

### Traffic Control & Security
- **Network Security Groups (NSGs)**: 5-tuple security rules (Source, Source Port, Destination, Destination Port, Protocol). Evaluated by priority (lower number = higher priority).
- **Application Security Groups (ASGs)**: Group VMs under a logical tag to simplify NSG rules without hardcoding IP addresses.
- **User-Defined Routes (UDR)**: Route tables overriding default system routes to force traffic through a Network Virtual Appliance (NVA) or Azure Firewall (`0.0.0.0/0` -> Next Hop: Virtual Appliance).

### Load Balancing & Gateways
| Service | Layer | Scope | Protocol | Features |
| :--- | :--- | :--- | :--- | :--- |
| **Azure Load Balancer** | Layer 4 (Transport) | Regional | TCP / UDP | Ultra-low latency, port forwarding, public or internal |
| **Azure Application Gateway** | Layer 7 (Application) | Regional | HTTP / HTTPS | URL routing, SSL termination, Web Application Firewall (WAF) |
| **Azure Front Door** | Layer 7 (Global) | Global CDN | HTTP / HTTPS | Global load balancing, edge acceleration, WAF |
| **Azure Traffic Manager** | DNS-based | Global | Any | DNS query routing (Performance, Priority, Weighted) |

---

## 📈 5. Monitoring & Backup

### Azure Monitor & Log Analytics
- **Metrics vs. Logs**: Numerical time-series data vs. structured queryable text logs.
- **Log Analytics Workspaces**: Central repository queried with KQL (Kusto Query Language).
- **Action Groups**: Notifications (email, SMS, webhook, logic app, runbook) triggered by alerts.

### Azure Backup & Recovery Services
- **Recovery Services Vault**: Backup policies for Azure VMs, SQL DBs, and on-premises servers.
- **Azure Site Recovery (ASR)**: Disaster recovery orchestration with continuous replication and failover test drills.
