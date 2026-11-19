# ☸️ Architecture Blueprint: AKS Enterprise Baseline

A production-grade, secure reference architecture for running **Azure Kubernetes Service (AKS)** in an enterprise environment.

---

## 🏗️ Core Cluster Design Principles

1. **Private Cluster**: AKS API server is exposed only on a private IP address within a private subnet; inaccessible from the public internet.
2. **Separated Node Pools**:
   - **System Node Pool**: Dedicated to critical Kubernetes system pods (`coredns`, `metrics-server`, ingress controller).
   - **User Node Pool**: Hosts application workloads with auto-scaling (1 to 10 nodes).
3. **Azure CNI Networking**: Every pod receives a real IP address from the Azure Virtual Network subnet, allowing direct communication with Azure PaaS and on-prem services.
4. **Managed Identity**: Uses Entra ID Managed Identities instead of static service principal credentials with expiring secrets.
5. **Azure Key Vault Secrets Provider (CSI Driver)**: Mounts secrets, TLS certificates, and keys directly into pods as volumes without storing sensitive data in Git or ConfigMaps.

---

## 🔒 Security & Governance Baseline

- **Entra ID Integration & Azure RBAC**: Kubernetes RBAC mapped to Entra ID groups.
- **Azure Policy for Kubernetes**: Enforces Gatekeeper / OPA policies:
  - Disallow privileged containers.
  - Require resource limits (`cpu` and `memory` requests/limits).
  - Enforce pulling images exclusively from private Azure Container Registry (ACR).
- **Microsoft Defender for Containers**: Real-time vulnerability scanning of running images and cluster runtime threat detection.
