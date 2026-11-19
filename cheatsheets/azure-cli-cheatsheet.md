# 💻 Azure CLI (`az`) Production Cheat Sheet

A curated reference guide of essential Azure CLI commands for daily cloud operations, troubleshooting, and automation.

---

## 🔐 1. Authentication & Subscription Management

```bash
# Log in to Azure interactively
az login

# Log in using a Service Principal
az login --service-principal -u <app-id> -p <password-or-cert> --tenant <tenant-id>

# Log in with Managed Identity (from an Azure VM or Cloud Shell)
az login --identity

# List all available subscriptions
az account list --output table

# Set active subscription
az account set --subscription "<subscription-name-or-id>"

# Show currently active account and tenant
az account show --output json
```

---

## 📁 2. Resource Groups

```bash
# Create a resource group
az group create --name rg-prod-eastus --location eastus --tags Environment=Production Owner=DevOps

# List all resource groups
az group list --output table

# Delete a resource group without prompt (Deletes ALL resources inside!)
az group delete --name rg-prod-eastus --yes --no-wait
```

---

## 🌐 3. Virtual Networks & Networking

```bash
# Create a Virtual Network with a default subnet
az network vnet create \
  --resource-group rg-prod-eastus \
  --name vnet-hub-eastus \
  --address-prefixes 10.0.0.0/16 \
  --subnet-name snet-core \
  --subnet-prefixes 10.0.1.0/24

# Create an additional subnet
az network vnet subnet create \
  --resource-group rg-prod-eastus \
  --vnet-name vnet-hub-eastus \
  --name snet-database \
  --address-prefixes 10.0.2.0/24

# Peer two Virtual Networks (Bidirectional requirement)
az network vnet peering create \
  --name peer-hub-to-spoke \
  --resource-group rg-prod-eastus \
  --vnet-name vnet-hub-eastus \
  --remote-vnet <spoke-vnet-id> \
  --allow-vnet-access

# Create a Network Security Group (NSG) and allow HTTPS rule
az network nsg create --resource-group rg-prod-eastus --name nsg-web-subnet
az network nsg rule create \
  --resource-group rg-prod-eastus \
  --nsg-name nsg-web-subnet \
  --name Allow-HTTPS \
  --priority 100 \
  --direction Inbound \
  --access Allow \
  --protocol Tcp \
  --destination-port-ranges 443
```

---

## 🖥️ 4. Virtual Machines

```bash
# Deploy an Ubuntu Linux VM with SSH keys
az vm create \
  --resource-group rg-prod-eastus \
  --name vm-prod-linux-01 \
  --image Ubuntu2204 \
  --size Standard_B2s \
  --admin-username azureuser \
  --generate-ssh-keys \
  --vnet-name vnet-hub-eastus \
  --subnet snet-core

# List VM power status
az vm list -d --query "[].{Name:name, Status:powerState, ResourceGroup:resourceGroup}" --output table

# Stop and deallocate VM (Stops compute billing!)
az vm deallocate --resource-group rg-prod-eastus --name vm-prod-linux-01

# Start VM
az vm start --resource-group rg-prod-eastus --name vm-prod-linux-01

# Run shell command remotely inside an Azure VM
az vm run-command invoke \
  --resource-group rg-prod-eastus \
  --name vm-prod-linux-01 \
  --command-id RunShellScript \
  --scripts "uptime && df -h"
```

---

## ☸️ 5. Azure Kubernetes Service (AKS)

```bash
# Create an AKS cluster with system-assigned identity and Azure CNI
az aks create \
  --resource-group rg-prod-eastus \
  --name aks-prod-cluster \
  --node-count 3 \
  --node-vm-size Standard_D4s_v5 \
  --enable-managed-identity \
  --network-plugin azure \
  --generate-ssh-keys

# Get Kubernetes credentials to local kubeconfig
az aks get-credentials --resource-group rg-prod-eastus --name aks-prod-cluster --overwrite-existing

# Add a dedicated user node pool
az aks nodepool add \
  --resource-group rg-prod-eastus \
  --cluster-name aks-prod-cluster \
  --name userpool1 \
  --node-count 2 \
  --node-vm-size Standard_E4s_v5 \
  --mode User

# Scale an existing node pool
az aks nodepool scale \
  --resource-group rg-prod-eastus \
  --cluster-name aks-prod-cluster \
  --name userpool1 \
  --node-count 5
```

---

## 📦 6. Storage & Key Vault

```bash
# Create a storage account with TLS 1.2 and no public blob access
az storage account create \
  --name stprodeastus001 \
  --resource-group rg-prod-eastus \
  --location eastus \
  --sku Standard_GRS \
  --min-tls-version TLS1_2 \
  --allow-blob-public-access false

# Create Azure Key Vault with purge protection
az keyvault create \
  --name kv-prod-eastus-01 \
  --resource-group rg-prod-eastus \
  --location eastus \
  --enable-purge-protection true

# Store and retrieve a secret
az keyvault secret set --vault-name kv-prod-eastus-01 --name "DbPassword" --value "SuperSecretPassword123!"
az keyvault secret show --vault-name kv-prod-eastus-01 --name "DbPassword" --query "value" --output tsv
```

---

## 🔍 7. Azure Resource Graph Queries (ARG)

```bash
# List all unattached managed disks (great for cost optimization)
az graph query -q "Resources | where type =~ 'microsoft.compute/disks' and properties.diskState == 'Unattached' | project name, resourceGroup, properties.diskSizeGB" --output table

# List public IP addresses with no NIC attached
az graph query -q "Resources | where type =~ 'microsoft.network/publicipaddresses' and isnull(properties.ipConfiguration) | project name, resourceGroup, location" --output table
```
