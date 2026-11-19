# 🔍 KQL (Kusto Query Language) Cheat Sheet

KQL is the query language used to search and analyze large datasets in **Azure Log Analytics**, **Azure Monitor**, **Application Insights**, **Microsoft Sentinel**, and **Azure Resource Graph**.

---

## 🧱 1. Basic Operators & Syntax

```kql
// Filter rows
AzureActivity
| where TimeGenerated >= ago(24h)
| where ActivityStatusValue == "Success"

// Project specific columns
AzureActivity
| project TimeGenerated, Caller, OperationNameValue, ResourceGroup

// Rename and compute new columns
AzureActivity
| extend OperationHour = datetime_part("hour", TimeGenerated)

// Sort results
AzureActivity
| sort by TimeGenerated desc
| take 50
```

---

## 📈 2. Aggregations & Summarization

```kql
// Count events grouped by caller
AzureActivity
| where TimeGenerated > ago(7d)
| summarize EventCount = count() by Caller
| order by EventCount desc

// Timechart of failed operations over the past 24 hours (1-hour bins)
AzureActivity
| where TimeGenerated > ago(24h)
| where ActivityStatusValue == "Failed"
| summarize FailedCount = count() by bin(TimeGenerated, 1h)
| render timechart
```

---

## 🚨 3. Real-World Monitoring & Security Queries

### Detect Who Created or Deleted Azure Resources
```kql
AzureActivity
| where OperationNameValue has "write" or OperationNameValue has "delete"
| where ActivityStatusValue == "Success"
| project TimeGenerated, Caller, CallerIpAddress, OperationNameValue, Resource, ResourceGroup
| sort by TimeGenerated desc
```

### Virtual Machine High CPU Usage Alert (> 85%)
```kql
Perf
| where TimeGenerated > ago(15m)
| where ObjectName == "Processor" and CounterName == "% Processor Time" and InstanceName == "_Total"
| summarize AvgCPU = avg(CounterValue) by Computer, bin(TimeGenerated, 5m)
| where AvgCPU > 85
```

### Query Azure Resource Graph: Public Storage Accounts
```kql
Resources
| where type =~ "microsoft.storage/storageaccounts"
| extend allowBlobPublicAccess = properties.allowBlobPublicAccess
| where allowBlobPublicAccess == true
| project name, resourceGroup, subscriptionId, location
```
