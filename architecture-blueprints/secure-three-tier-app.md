# 🛡️ Architecture Blueprint: Secure 3-Tier Enterprise Web Application

A resilient, defense-in-depth architecture for hosting critical enterprise web applications on Azure.

---

## 🏛️ Architectural Topology

```
[ Public Users ]
       |
       v (HTTPS / 443)
+-------------------------------------------------------------+
| TIER 1: WEB INGRESS & EDGE                                  |
|   Azure Application Gateway v2                              |
|   - Web Application Firewall (WAF v2, OWASP CRS 3.2)       |
|   - SSL / TLS Termination                                   |
|   - URL-based Routing & Cookie-based Affinity               |
+------------------------------+------------------------------+
                               |
                               v (Internal Private VNet)
+-------------------------------------------------------------+
| TIER 2: APPLICATION RUNTIME                                 |
|   Azure App Service / Azure Container Apps                  |
|   - VNet Integration (Inbound Private, Outbound VNet)       |
|   - Managed Identity for Passwordless Azure Access          |
|   - Auto-scaling based on HTTP requests & CPU               |
+------------------------------+------------------------------+
                               |
                               v (Private Endpoint / Private Link)
+-------------------------------------------------------------+
| TIER 3: DATA PERSISTENCE & SECRETS                          |
|   Azure SQL Database / Cosmos DB                            |
|   - Public Network Access: DISABLED                         |
|   - Entra ID (Azure AD) Only Authentication                 |
|   - Transparent Data Encryption (TDE) with Customer Key     |
|                                                             |
|   Azure Key Vault (Secrets & Encryption Keys)               |
|   - Private Endpoint enabled                                |
|   - RBAC-based access policies                              |
+-------------------------------------------------------------+
```

---

## 🔐 Key Defense-in-Depth Measures

1. **Zero Public Access to Data**: Storage Accounts, Key Vaults, and Azure SQL have public network access completely disabled (`publicNetworkAccess = false`).
2. **Private Endpoints**: Traffic between compute and data services travels exclusively across the Microsoft private backbone network.
3. **No Hardcoded Credentials**: The application uses Managed Identity to authenticate directly with Azure SQL and Key Vault.
4. **WAF Protection**: Detects and mitigates SQL injection, cross-site scripting (XSS), and common web exploits at the edge.
