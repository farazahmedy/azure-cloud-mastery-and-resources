# ☁️ Azure Cloud Engineering & Operations Mastery Hub

[![Microsoft Azure](https://img.shields.io/badge/Microsoft_Azure-0078D4?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge)](http://makeapullrequest.com)

Welcome to the **Azure Cloud Engineering & Operations Mastery Hub**! An enterprise-grade, battle-tested knowledge base and hands-on operational handbook for Microsoft Azure Cloud engineers, administrators, architects, and DevOps professionals.

---

## 📑 Repository Contents

1. [🏛️ Production Architecture Blueprints](#️-production-architecture-blueprints)
2. [🚨 Production Runbooks & Troubleshooting](#-production-runbooks--troubleshooting)
3. [🛡️ Security Hardening & CIS Benchmarks](#️-security-hardening--cis-benchmarks)
4. [💰 FinOps & Cost Optimization Strategies](#-finops--cost-optimization-strategies)
5. [🛠️ CLI, PowerShell & KQL Cheat Sheets](#️-cli-powershell--kql-cheat-sheets)
6. [📘 Core Engineering Deep-Dives](#-core-engineering-deep-dives)

---

## 🏛️ Production Architecture Blueprints

Real-world architectural patterns aligned with the **Microsoft Well-Architected Framework**:

- 🌐 [**Hub-and-Spoke Virtual Network Topology**](./architecture-blueprints/hub-and-spoke-network.md): Centralized firewall, VPN/ExpressRoute gateway transit, and isolated spoke networks with Private Endpoints.
- ☸️ [**AKS Enterprise Baseline Architecture**](./architecture-blueprints/aks-enterprise-baseline.md): Secure, multi-tenant Kubernetes cluster with Azure CNI, managed identities, Key Vault CSI secret driver, and Ingress Controller.
- 🛡️ [**Secure 3-Tier Web Application**](./architecture-blueprints/secure-three-tier-app.md): Application Gateway with WAF v2, Azure App Services/Containers, and Azure SQL Database with Private Link.

---

## 🚨 Production Runbooks & Troubleshooting

- 🩺 [**Incident Response & Troubleshooting Runbook**](./production-runbooks/incident-response-and-troubleshooting.md):
  - Diagnosing 502/504 Bad Gateway errors on Application Gateway
  - VM high CPU and OOM root cause analysis
  - VNet Peering packet drop and UDR route verification
  - Key Vault 403 Forbidden troubleshooting
  - Managed Disk IOPS and throughput throttling remediations

---

## 🛡️ Security Hardening & CIS Benchmarks

- 🔒 [**CIS Microsoft Azure Foundations Benchmark Checklist**](./security-and-compliance/cis-azure-benchmark-hardening.md): 25+ essential hardening controls across IAM, Storage, Networking, and Compute.
- 📜 [**Azure Policy & RBAC Governance Guide**](./governance/azure-policies-guide.md): Management Groups, tag enforcement, geographical deployment restrictions, and least-privilege role assignment matrix.

---

## 💰 FinOps & Cost Optimization Strategies

- 📉 [**Azure Cost Optimization Playbook**](./cheatsheets/cost-optimization-guide.md): Practical checklist covering Azure Reservations, Savings Plans, Unattached Managed Disks, Orphan Public IPs, Storage Lifecycle Management, and Auto-Shutdown policies.

---

## 🛠️ CLI, PowerShell & KQL Cheat Sheets

- 💻 [**Azure CLI (`az`) Cheat Sheet**](./cheatsheets/azure-cli-cheatsheet.md): Essential commands for VMs, Storage, Resource Groups, AKS, Networking, and RBAC.
- ⚡ [**Azure PowerShell (`Az`) Cheat Sheet**](./cheatsheets/azure-powershell-cheatsheet.md): Cmdlets for batch operations, reporting, and management.
- 🔍 [**KQL (Kusto Query Language) Cheat Sheet**](./cheatsheets/kql-kusto-cheatsheet.md): Log Analytics, Azure Monitor, and Resource Graph queries for alerts and diagnostics.

---

## 📘 Core Engineering Deep-Dives

- [**Cloud Core Concepts & Architectural Patterns**](./cloud-engineering-guides/azure-core-concepts-guide.md)
- [**Azure Infrastructure & Networking Administration**](./cloud-engineering-guides/azure-infrastructure-admin-guide.md)
- [**Enterprise Solutions Architecture Design**](./cloud-engineering-guides/enterprise-solutions-architecture.md)
- [**DevOps & SRE Production Practices**](./cloud-engineering-guides/devops-sre-production-guide.md)
- [**Awesome Azure Curated Tools & Frameworks**](./awesome-azure-resources.md)

---

## 👤 Author & Contribution

Maintained by **Faraz Ahmed** ([@farazahmedy](https://github.com/farazahmedy)).
Contributions, real-world incident postmortems, and new blueprints are welcome!
