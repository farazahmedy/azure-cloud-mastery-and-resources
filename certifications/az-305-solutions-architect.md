# 📘 AZ-305: Designing Microsoft Azure Infrastructure Solutions

The AZ-305 exam validates advanced architecture design capabilities across identity, governance, monitoring, data storage, business continuity, and infrastructure solutions.

---

## 🎯 Exam Domain Breakdown

1. **Design Identity, Governance, and Monitoring Solutions (25–30%)**
2. **Design Data Storage Solutions (25–30%)**
3. **Design Business Continuity Solutions (10–15%)**
4. **Design Infrastructure Solutions (25–30%)**

---

## 🏛️ Key Architectural Design Principles

### Microsoft Well-Architected Framework (WAF)
1. **Reliability**: Ability of a system to recover from failures and continue to function.
2. **Security**: Protecting data, applications, and networks from threats (Zero Trust model).
3. **Cost Optimization**: Managing and minimizing costs without sacrificing performance.
4. **Operational Excellence**: Automation, monitoring, and release management.
5. **Performance Efficiency**: Matching resource capacity to demand.

---

## 🛡️ 1. Identity, Governance & Monitoring Design

- **Zero Trust Architecture**: "Never trust, always verify".
  - Explicit verification of user, device, network context, and risk signals.
  - Principle of Least Privilege with Just-In-Time (JIT) access using **Microsoft Entra PIM (Privileged Identity Management)**.
- **Enterprise Landing Zones**:
  - Hierarchical structure: Root Management Group -> Platform (Identity, Management, Connectivity) + Landing Zones (Corp, Online) -> Sandbox.
- **Auditing & SIEM**:
  - Centralized logs exported to **Azure Log Analytics** and analyzed with **Microsoft Sentinel** (Cloud SIEM/SOAR).

---

## 💾 2. Data Storage Architecture Design

### Relational Data:
- **Azure SQL Database**: Hyperscale (up to 100 TB, instant storage scaling) vs. Business Critical (in-memory, high IOPS).
- **Azure SQL Managed Instance**: Near 100% on-premises SQL Server feature compatibility with native VNet peering.

### Non-Relational Data:
- **Azure Cosmos DB**: Multi-model (NoSQL, Mongo, Cassandra, Gremlin, Table), single-digit millisecond latency, turnkey global replication.
  - 5 Consistency Levels: *Strong -> Bounded Staleness -> Session (default, ideal balance) -> Consistent Prefix -> Eventual*.

---

## 🔄 3. Business Continuity & Disaster Recovery (BCDR)

- **RTO (Recovery Time Objective)**: Maximum acceptable time the system can be down after disaster.
- **RPO (Recovery Point Objective)**: Maximum acceptable period of data loss (e.g., last 15 minutes of transactions).
- **Cross-Region Replication**:
  - Geo-paired regions for active-passive or active-active configurations.
  - Azure Site Recovery (ASR) with automated failover runbooks.

---

## 🏗️ 4. Infrastructure & Migration Design

- **Compute Choices Decision Tree**:
  - Microservices / Containers: AKS (for fine-grained Kubernetes control) or Azure Container Apps (serverless microservices without K8s management overhead).
  - Web Apps: Azure App Service (PaaS, custom domains, built-in TLS, staging slots).
  - Event-Driven / Serverless: Azure Functions.
  - Legacy lift-and-shift: Azure Virtual Machines / Azure VMware Solution.
- **Network Security Architecture**:
  - Hub-and-Spoke with Azure Firewall Premium (IDPS, TLS Inspection, FQDN filtering).
  - Private Endpoints / Azure Private Link for all PaaS services (never expose storage or databases to the public internet).
