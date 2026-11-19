# ☁️ Azure Cloud Mastery & Resources Hub

[![Microsoft Azure](https://img.shields.io/badge/Microsoft_Azure-0078D4?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge)](http://makeapullrequest.com)

Welcome to the **Azure Cloud Mastery & Resources Hub**! This repository is an all-in-one, battle-tested knowledge base and practical reference guide for Microsoft Azure Cloud engineers, administrators, architects, and DevOps professionals.

---

## 📑 Table of Contents

1. [🎯 Certification Study Guides](#-azure-certification-study-guides)
2. [🏛️ Architecture Blueprints](#️-architecture-blueprints)
3. [🛠️ Daily CLI & PowerShell Cheat Sheets](#️-cli--powershell-cheat-sheets)
4. [💰 Cost Optimization Strategies](#-cost-optimization-strategies)
5. [🔐 Governance, Policy & Security](#-governance-policy--security)
6. [🌟 Curated Awesome Azure Repos & Tools](#-curated-awesome-azure-repos--tools)

---

## 🎯 Azure Certification Study Guides

Comprehensive notes, exam outlines, key concepts, and practical tips:

| Certification | Level | Role | Study Guide Link |
| :--- | :--- | :--- | :--- |
| **AZ-900** | Fundamental | Cloud Fundamentals | [AZ-900 Study Guide](./certifications/az-900-fundamentals.md) |
| **AZ-104** | Associate | Azure Administrator | [AZ-104 Study Guide](./certifications/az-104-administrator.md) |
| **AZ-305** | Expert | Azure Solutions Architect | [AZ-305 Study Guide](./certifications/az-305-solutions-architect.md) |
| **AZ-400** | Expert | Azure DevOps Engineer | [AZ-400 Study Guide](./certifications/az-400-devops-engineer.md) |

---

## 🏛️ Architecture Blueprints

Real-world architectural patterns aligned with the **Microsoft Well-Architected Framework**:

- 🌐 [**Hub-and-Spoke Virtual Network Topology**](./architecture-blueprints/hub-and-spoke-network.md): Centralized firewall, VPN/ExpressRoute gateway transit, and isolated spoke networks with Private Endpoints.
- ☸️ [**AKS Enterprise Baseline Architecture**](./architecture-blueprints/aks-enterprise-baseline.md): Secure, multi-tenant Kubernetes cluster with Azure CNI, managed identities, Key Vault CSI secret driver, and Ingress Controller.
- 🛡️ [**Secure 3-Tier Web Application**](./architecture-blueprints/secure-three-tier-app.md): Application Gateway with WAF v2, Azure App Services/Containers, and Azure SQL Database with Private Link.

---

## 🛠️ CLI & PowerShell Cheat Sheets

Quick commands for day-to-day administration and scripting:

- 💻 [**Azure CLI (`az`) Cheat Sheet**](./cheatsheets/azure-cli-cheatsheet.md): Essential commands for VMs, Storage, Resource Groups, AKS, Networking, and RBAC.
- ⚡ [**Azure PowerShell (`Az`) Cheat Sheet**](./cheatsheets/azure-powershell-cheatsheet.md): Cmdlets for batch operations, reporting, and management.
- 🔍 [**KQL (Kusto Query Language) Cheat Sheet**](./cheatsheets/kql-kusto-cheatsheet.md): Log Analytics, Azure Monitor, and Resource Graph queries for alerts and diagnostics.

---

## 💰 Cost Optimization Strategies

Practical checklist to cut your Azure monthly cloud bill:
- [**Azure Cost Optimization Guide**](./cheatsheets/cost-optimization-guide.md): Covers Azure Reservations, Savings Plans, Unattached Managed Disks, Orphan Public IPs, Storage Lifecycle Management, and Auto-Shutdown policies.

---

## 🔐 Governance, Policy & Security

Enterprise governance and compliance:
- [**Azure Policies & RBAC Guide**](./governance/azure-policies-guide.md): Management Group hierarchies, custom Azure Policy definitions (allowed regions, tag enforcement, deny public IP), and Principle of Least Privilege RBAC roles.

---

## 🌟 Curated Awesome Azure Repos & Tools

- [**Awesome Azure Resources List**](./awesome-azure-resources.md): Links to official Microsoft GitHub repos, open-source utilities, YouTube channels, and blogs.

---

## 👤 Author & Contribution

Maintained by **Faraz Ahmed** ([@farazahmedy](https://github.com/farazahmedy)).
Contributions, corrections, and new blueprints are always welcome! Feel free to fork and open a Pull Request.
