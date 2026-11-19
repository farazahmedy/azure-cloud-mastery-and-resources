# 🚨 Azure Production Troubleshooting & Incident Response Runbook

Battle-tested procedures for triaging, diagnosing, and resolving the most common production incidents in Microsoft Azure environments.

---

## 📑 Quick Navigation

1. [502 / 504 Bad Gateway on Application Gateway](#1-502--504-bad-gateway-on-application-gateway)
2. [Virtual Machine High CPU & Out-Of-Memory (OOM)](#2-virtual-machine-high-cpu--out-of-memory)
3. [VNet Peering Traffic Drops & Routing Failures](#3-vnet-peering-traffic-drops--routing-failures)
4. [Azure Key Vault 403 Forbidden / Access Denied](#4-azure-key-vault-403-forbidden--access-denied)
5. [Managed Disk IOPS & Throughput Throttling](#5-managed-disk-iops--throughput-throttling)

---

## 1. 502 / 504 Bad Gateway on Application Gateway

### Root Causes:
- Backend target VM / Pod is down or not listening on the configured port.
- Custom health probe failed due to HTTP status code mismatch (expected 200, got 404/500).
- NSG on the backend subnet blocking probe traffic from `GatewayManager` service tag.

### Diagnostic Steps:
1. Check backend health status:
   ```bash
   az network application-gateway show-backend-health \
     --resource-group rg-prod-eastus \
     --name appgw-prod-eastus \
     --output table
   ```
2. Verify Backend Subnet NSG contains rule:
   - **Source**: `GatewayManager`
   - **Source Port**: `*`
   - **Destination**: `*`
   - **Destination Port**: `65200-65535` (for v2 SKU)
   - **Action**: `Allow`

---

## 2. Virtual Machine High CPU & Out-Of-Memory

### Diagnostic Steps:
1. Run diagnostic shell script remotely via Azure Run Command (no SSH required):
   ```bash
   az vm run-command invoke \
     --resource-group rg-prod-eastus \
     --name vm-prod-app01 \
     --command-id RunShellScript \
     --scripts "ps aux --sort=-%cpu | head -n 10 && free -h"
   ```
2. Check Azure Monitor Perf logs in Log Analytics:
   ```kql
   Perf
   | where Computer == "vm-prod-app01" and ObjectName == "Processor"
   | where TimeGenerated >= ago(2h)
   | summarize AvgCPU = avg(CounterValue) by bin(TimeGenerated, 5m)
   | render timechart
   ```

---

## 3. VNet Peering Traffic Drops & Routing Failures

### Diagnostic Steps:
1. Check Effective Routes on the VM Network Interface:
   ```bash
   az network nic show-effective-route-table \
     --resource-group rg-prod-eastus \
     --name nic-vm-prod-01 \
     --output table
   ```
2. Look for `VirtualAppliance` next hop: If default route `0.0.0.0/0` is routed to an Azure Firewall / NVA, verify that IP forwarding is enabled on the NVA NIC and the firewall rules permit inter-spoke traffic.
3. Test connectivity using Azure Network Watcher:
   ```bash
   az network watcher test-connectivity \
     --resource-group rg-network-hub \
     --source-resource vm-prod-01 \
     --dest-address 10.1.2.4 \
     --dest-port 80
   ```

---

## 4. Azure Key Vault 403 Forbidden / Access Denied

### Diagnostic Steps:
1. Check authorization model:
   - If `enableRbacAuthorization = true`: Ensure Managed Identity has `Key Vault Secrets User` (not just Reader or Contributor!).
   - If Access Policies model: Ensure Object ID has `Get` and `List` permissions.
2. Check Network Firewall:
   - If Key Vault firewall is enabled (`default_action = "Deny"`):
     - Ensure the requesting resource is in an allowed VNet subnet or uses a Private Endpoint.
     - Ensure "Allow trusted Microsoft services" is enabled if called by Azure Backup / App Service.

---

## 5. Managed Disk IOPS & Throughput Throttling

### Diagnostic Steps:
1. Check metrics in Azure Monitor:
   - `OS Disk IOPS Consumed Percentage` > 90%
   - `Data Disk Throughput Consumed Percentage` > 90%
2. Remediation:
   - Upgrade disk SKU: Standard HDD -> Standard SSD -> Premium SSD v2.
   - Enable Host Caching (Read-Only) for read-heavy database workloads.
   - Strip multiple disks using LVM / Storage Spaces for higher aggregate throughput.
