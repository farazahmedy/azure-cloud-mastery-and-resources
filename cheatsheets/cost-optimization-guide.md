# 💰 Azure Cloud Cost Optimization Playbook

A production-proven checklist to analyze, monitor, and eliminate waste in your Azure cloud infrastructure, delivering up to 30–60% monthly savings.

---

## 🎯 Top 10 High-Impact Cost Saving Levers

### 1. Identify & Delete Orphaned Managed Disks
When an Azure Virtual Machine is deleted, its OS disk and data disks remain attached to the subscription and continue to bill full storage costs indefinitely.
- **Action**: Run the automated PowerShell script in `azure-powershell-automation-toolkit` to identify unattached disks and purge or snapshot them.

### 2. Clean Up Unused Static Public IP Addresses
Static Public IPs that are allocated but not associated with a running NIC or Load Balancer still accrue hourly reservation fees.
- **Action**: Audit with Azure Resource Graph and delete orphan PIPs.

### 3. Reserved Instances (RIs) & Azure Savings Plans
- **1-Year or 3-Year Reservations**: Save up to 72% on predictable, 24/7 workloads (VMs, Azure SQL, Cosmos DB, Synapse).
- **Azure Savings Plan for Compute**: Flexible commitment across VM families, App Services, and Azure Container Apps.

### 4. Azure Hybrid Benefit (AHB)
- Apply existing on-premises Windows Server and SQL Server licenses with Software Assurance to Azure VMs and Azure SQL to save up to 40-55% on license costs.

### 5. Automated VM Scheduling (Dev / Test Workloads)
- Non-production environments only need to be online during business hours (e.g., 9 AM – 7 PM Monday to Friday).
- **Savings**: Running VMs 50 hours/week instead of 168 hours/week saves **~70%** on compute!
- **Action**: Use Azure Automation Runbooks or auto-shutdown policies in the portal.

### 6. Storage Lifecycle Management
- Transition blob data automatically:
  - Hot -> Cool (after 30 days)
  - Cool -> Archive (after 90 days)
  - Auto-delete (after retention period, e.g., 365 days)

### 7. Right-Size Over-Provisioned VMs & Databases
- Use **Azure Advisor** to find VMs with average CPU utilization < 5% and network utilization < 2% over a 14-day window.
- Downgrade to B-series (burstable) for dev/staging environments.

### 8. Use Azure Spot Virtual Machines
- Save up to 90% for fault-tolerant, interruptible workloads (batch processing, dev builds, test runners).

### 9. Optimize Log Analytics Ingestion & Retention
- Review high-volume ingestion tables (e.g., `W3CIISLog`, `ContainerLogV2`).
- Switch verbose tables to **Basic Logs** tier for up to 80% reduction in ingestion costs.
- Adjust default retention from 90 days to 30 days if not required by compliance.

### 10. Implement Budget Alerts & Anomaly Detection
- Configure Azure Cost Management budgets at the Subscription and Resource Group level with thresholds at 50%, 80%, and 100%.
- Enable Azure Cost Anomaly alerts to catch runaway resources within 24 hours.
