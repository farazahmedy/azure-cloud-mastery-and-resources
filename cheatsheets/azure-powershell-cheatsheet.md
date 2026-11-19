# ⚡ Azure PowerShell (`Az`) Production Cheat Sheet

A comprehensive collection of practical Azure PowerShell cmdlets for enterprise management, bulk updates, and reporting.

---

## 🔌 1. Connect & Context

```powershell
# Interactive Sign-in
Connect-AzAccount

# Sign in with a specific Tenant
Connect-AzAccount -TenantId "your-tenant-id-guid"

# List and Select Subscription
Get-AzSubscription | Select-Object Name, Id, State
Set-AzContext -SubscriptionId "your-subscription-id-guid"

# View current context
Get-AzContext | Select-Object Subscription, Account, Tenant
```

---

## 🗂️ 2. Resource Groups & Tags

```powershell
# Create a new Resource Group with structured Tags
$tags = @{
    Environment = "Production"
    Owner       = "Faraz Ahmed"
    CostCenter  = "IT-Ops-101"
}
New-AzResourceGroup -Name "rg-network-prod" -Location "EastUS" -Tag $tags

# Apply tags to all resources in a resource group
$rg = Get-AzResourceGroup -Name "rg-network-prod"
Get-AzResource -ResourceGroupName $rg.ResourceGroupName | ForEach-Object {
    Update-AzTag -ResourceId $_.ResourceId -Tag $tags -Operation Merge
}
```

---

## 🖥️ 3. Virtual Machines & Scale Sets

```powershell
# Find all stopped but ALLOCATED VMs (still incurring compute costs!)
Get-AzVM -Status | Where-Object { 
    $_.PowerState -eq "VM stopped" 
} | Select-Object Name, ResourceGroupName, PowerState

# Find all properly DEALLOCATED VMs (compute cost stopped)
Get-AzVM -Status | Where-Object { 
    $_.PowerState -eq "VM deallocated" 
} | Select-Object Name, ResourceGroupName

# Safely stop and deallocate a VM
Stop-AzVM -ResourceGroupName "rg-network-prod" -Name "vm-prod-app01" -Force

# Start a VM
Start-AzVM -ResourceGroupName "rg-network-prod" -Name "vm-prod-app01"

# Restart all VMs in a resource group sequentially
Get-AzVM -ResourceGroupName "rg-network-prod" | Restart-AzVM
```

---

## 🛡️ 4. Role-Based Access Control (RBAC)

```powershell
# List all Owner assignments across subscription
Get-AzRoleAssignment -RoleDefinitionName "Owner" | Select-Object DisplayName, SignInName, Scope

# Assign 'Contributor' role to a user for a specific Resource Group
New-AzRoleAssignment -SignInName "user@domain.com" `
                     -RoleDefinitionName "Contributor" `
                     -ResourceGroupName "rg-network-prod"

# Remove a role assignment
Remove-AzRoleAssignment -SignInName "user@domain.com" `
                        -RoleDefinitionName "Contributor" `
                        -ResourceGroupName "rg-network-prod"
```

---

## 📊 5. Audit & Compliance One-Liners

```powershell
# Export all resources in subscription to CSV
Get-AzResource | Select-Object Name, ResourceType, ResourceGroupName, Location | 
    Export-Csv -Path "./azure-resources-inventory.csv" -NoTypeInformation

# Find public IP addresses not associated with any network interface
Get-AzPublicIpAddress | Where-Object { 
    $null -eq $_.IpConfiguration 
} | Select-Object Name, ResourceGroupName, Location

# Find unattached managed disks across all resource groups
Get-AzDisk | Where-Object { 
    $_.ManagedBy -eq $null 
} | Select-Object Name, ResourceGroupName, DiskSizeGB, Sku
```
