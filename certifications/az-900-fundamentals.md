# 📘 AZ-900: Microsoft Azure Fundamentals Study Guide

The AZ-900 certification validates foundational knowledge of cloud concepts and core Microsoft Azure services, security, privacy, compliance, trust, and pricing.

---

## 🎯 Exam Domain Breakdown

1. **Describe Cloud Concepts (25–30%)**
2. **Describe Azure Architecture and Services (35–40%)**
3. **Describe Azure Management and Governance (30–35%)**

---

## ☁️ 1. Cloud Concepts

### Cloud Computing Benefits
- **High Availability (HA)**: Ensures system uptime with minimal downtime (SLAs like 99.9% - 99.99%).
- **Scalability**: Ability to allocate resources based on demand:
  - *Vertical Scaling (Scale Up/Down)*: Increasing CPU, RAM, or Disk size of an existing instance.
  - *Horizontal Scaling (Scale Out/In)*: Adding or removing instances (VM Scale Sets).
- **Elasticity**: Dynamically scaling in and out automatically based on load.
- **Agility**: Rapid deployment and configuration of cloud services.
- **Disaster Recovery (DR)**: Safeguarding data and services using geo-redundancy and backups.

### Cloud Service Models
| Model | Description | What You Manage | What Microsoft Manages | Example |
| :--- | :--- | :--- | :--- | :--- |
| **IaaS** | Infrastructure as a Service | OS, Middleware, Runtime, Apps, Data | Virtualization, Servers, Storage, Networking | Azure VMs, VNet, Disks |
| **PaaS** | Platform as a Service | Applications, Data | OS, Runtime, Middleware, Infrastructure | Azure App Service, Azure SQL |
| **SaaS** | Software as a Service | User Access, Config | Everything else | Microsoft 365, Dynamics 365 |

### Cloud Deployment Models
- **Public Cloud**: Owned and operated by third-party provider (Microsoft); shared infrastructure over the internet.
- **Private Cloud**: Dedicated exclusively to a single organization (on-prem or hosted).
- **Hybrid Cloud**: Combines public and private clouds (connected via VPN or ExpressRoute).
- **Multi-Cloud**: Using multiple cloud providers (Azure + AWS + GCP).

### CapEx vs. OpEx
- **CapEx (Capital Expenditure)**: Upfront spending on physical infrastructure (servers, data centers). Depreciated over time.
- **OpEx (Operational Expenditure)**: Pay-as-you-go recurring cost for cloud services actually consumed. Immediate tax deduction.

---

## 🏛️ 2. Azure Architecture & Core Services

### Structural Components
- **Geographies**: Discreet markets containing two or more regions that preserve data residency (e.g., Americas, Europe, Asia Pacific).
- **Regions**: Geographical area containing one or more datacenters networked together with low-latency links.
- **Region Pairs**: Two regions within the same geography paired 300+ miles apart for disaster recovery updates (e.g., East US & West US).
- **Availability Zones (AZs)**: Physically separated datacenters within an Azure region, each with independent power, cooling, and networking. Provides 99.99% VM uptime SLA.
- **Resource Groups (RG)**: Logical container holding related Azure resources for unified lifecycle management, RBAC, and billing tags.
- **Subscriptions**: Logical unit of Azure services linked to an Azure account; boundaries for billing and resource quotas.
- **Management Groups**: Containers to manage access, policy, and compliance across multiple subscriptions.

### Core Azure Services
- **Compute**: Azure Virtual Machines, Virtual Machine Scale Sets (VMSS), Azure App Services, Azure Container Instances (ACI), Azure Kubernetes Service (AKS), Azure Functions (Serverless).
- **Networking**: Azure Virtual Network (VNet), Subnets, Peering, Azure VPN Gateway, Azure ExpressRoute (private fiber connection), Azure DNS, Application Gateway, Azure Front Door.
- **Storage**: Azure Blob Storage (Hot, Cool, Cold, Archive tiers), Azure Files (SMB/NFS shares), Azure Managed Disks, Azure Queue, Azure Table Storage.
- **Databases**: Azure SQL Database, Azure Cosmos DB (globally distributed NoSQL), Azure Database for PostgreSQL / MySQL.

---

## 🔐 3. Azure Management & Governance

### Identity & Access
- **Microsoft Entra ID (formerly Azure Active Directory)**: Cloud-based Identity and Access Management (IAM) service.
  - Multi-Factor Authentication (MFA)
  - Single Sign-On (SSO)
  - Conditional Access Policies
- **Role-Based Access Control (RBAC)**: Granting granular permissions based on roles:
  - *Owner*: Full access to manage all resources + assign permissions.
  - *Contributor*: Create and manage all resources, but cannot assign roles.
  - *Reader*: View resources only.
  - *User Access Administrator*: Manage user access/roles only.

### Compliance & Governance
- **Azure Policy**: Enforces organizational standards and assesses compliance (e.g., allow only specific VM sizes, enforce resource tagging, restrict deployment regions).
- **Azure Blueprints / Template Specs**: Packaging resource templates, policies, and role assignments for repeatable landing zones.
- **Resource Locks**:
  - `CanNotDelete`: Users can read and modify, but cannot delete.
  - `ReadOnly`: Users can only read; cannot modify or delete.

### Cost Management
- **Total Cost of Ownership (TCO) Calculator**: Compares costs of on-prem datacenter vs. Azure cloud migration.
- **Azure Pricing Calculator**: Estimates costs before provisioning resources.
- **Azure Cost Management + Billing**: Monitors cloud spending, sets budget alerts, and analyzes resource costs.
- **Azure Advisor**: Provides actionable recommendations for High Availability, Security, Performance, Operational Excellence, and Cost Optimization.

---

## 📝 Practice Tips for the Exam
1. Focus heavily on understanding the difference between IaaS, PaaS, and SaaS.
2. Memorize the hierarchy: `Management Groups -> Subscriptions -> Resource Groups -> Resources`.
3. Understand the distinction between Region Pairs and Availability Zones.
4. Review free practice assessments on Microsoft Learn before the exam.
