# 🌐 Architecture Blueprint: Hub-and-Spoke Virtual Network

The **Hub-and-Spoke** topology is the foundational networking pattern recommended by Microsoft's Cloud Adoption Framework (CAF) for enterprise Azure architectures.

---

## 🏛️ Architecture Overview

```
                      +---------------------------------------+
                      |               ON-PREMISES             |
                      |   Datacenter / Corporate Headquarters |
                      +-------------------+-------------------+
                                          |
                      ExpressRoute / S2S VPN Tunnel
                                          |
                                          v
+----------------------------------------------------------------------------------+
|                                HUB VIRTUAL NETWORK                               |
|                                                                                  |
|   +--------------------------+          +-----------------------------------+    |
|   | GatewaySubnet            |          | AzureFirewallSubnet               |    |
|   | [Virtual Network Gateway]|          | [Azure Firewall / NVA]            |    |
|   +--------------------------+          +-----------------+-----------------+    |
|                                                           ^                      |
|   +--------------------------+                            |                      |
|   | AzureBastionSubnet       |                            |                      |
|   | [Azure Bastion Host]     |                            |                      |
|   +--------------------------+                            |                      |
+-----------------------------------------------------------+----------------------+
                      |                                     |
               VNet Peering                          VNet Peering
                      |                                     |
                      v                                     v
+------------------------------------+   +------------------------------------+
|         SPOKE 1: WORKLOAD A        |   |         SPOKE 2: WORKLOAD B        |
|                                    |   |                                    |
|   +----------------------------+   |   |   +----------------------------+   |
|   | App Subnet (VMs / App Serv)|   |   |   | AKS Subnet                 |   |
|   +----------------------------+   |   |   | (Azure Kubernetes Service) |   |
|   +----------------------------+   |   |   +----------------------------+   |
|   | Data Subnet                |   |   |   +----------------------------+   |
|   | (Private Endpoints / SQL)  |   |   |   | Private Endpoint Subnet    |   |
|   +----------------------------+   |   |   +----------------------------+   |
+------------------------------------+   +------------------------------------+
```

---

## 🎯 Key Architectural Components

### 1. Hub Virtual Network
- Acts as the central point of connectivity to on-premises networks and the internet.
- **GatewaySubnet**: Hosts the Azure Virtual Network Gateway (VPN or ExpressRoute).
- **AzureFirewallSubnet**: Hosts Azure Firewall Premium for centralized inspection, Threat Intelligence filtering, and Layer 7 egress control.
- **AzureBastionSubnet**: Provides secure browser-based RDP/SSH access to VMs without public IP exposure.

### 2. Spoke Virtual Networks
- Dedicated to isolated workloads, applications, or business units.
- Non-overlapping IP address spaces.
- Contain application subnets, database subnets, and private endpoint subnets.

### 3. VNet Peering & Routing
- Spoke VNets peer directly with the Hub VNet.
- Hub peering enables `Allow gateway transit`.
- Spoke peering enables `Use remote gateways`.
- **User-Defined Routes (UDRs)**: Applied to Spoke subnets with default route (`0.0.0.0/0`) pointed to the private IP of the Azure Firewall as the `VirtualAppliance` next hop.

---

## 🛡️ Security Best Practices
- **No Direct Internet Ingress/Egress**: All inbound traffic flows through Application Gateway WAF; all outbound internet traffic routes through Azure Firewall.
- **Private DNS Zones**: Linked to Hub and Spoke VNets to resolve private endpoints (e.g., `privatelink.blob.core.windows.net`, `privatelink.database.windows.net`).
- **Network Security Groups (NSGs)**: Applied on every subnet for micro-segmentation.
