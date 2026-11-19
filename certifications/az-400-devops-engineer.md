# 📘 AZ-400: Designing and Implementing Microsoft DevOps Solutions

The AZ-400 exam validates senior DevOps capabilities in designing and implementing strategies for collaboration, code, infrastructure, source control, security, compliance, continuous integration, testing, delivery, monitoring, and feedback.

---

## 🎯 Exam Domain Breakdown

1. **Configure Processes and Communications (10–15%)**
2. **Design and Implement Source Control (15–20%)**
3. **Design and Implement Build and Release Pipelines (40–45%)**
4. **Develop a Security and Compliance Plan (10–15%)**
5. **Implement an Instrumentation Strategy (10–15%)**

---

## 🚀 1. Continuous Integration & Continuous Delivery (CI/CD)

### Azure Pipelines & GitHub Actions
- **YAML Multi-stage Pipelines**: Stage -> Job -> Step -> Task hierarchy.
- **Runners & Agents**:
  - Microsoft-hosted agents: Clean VM for each job, zero maintenance.
  - Self-hosted agents: Inside private VNet to access internal resources/databases.
- **Environments & Approvals**:
  - Manual approval checks, business hours restrictions, branch protection rules.
  - Deployment Gates: Automated REST API checks and Azure Monitor alert evaluations before approving releases.
- **Deployment Strategies**:
  - **Blue/Green Deployment**: Two identical environments; swap router traffic instantaneously.
  - **Canary Deployment**: Route 5-10% of user traffic to new version to validate metrics before 100% rollout.
  - **Rolling Deployment**: Incrementally update instances in a fleet (default in Kubernetes).

---

## 🔐 2. DevSecOps & Shift-Left Security

- **Static Application Security Testing (SAST)**: SonarQube, GitHub CodeQL.
- **Software Composition Analysis (SCA)**: Dependabot, Snyk for vulnerable open-source dependencies.
- **Secret Scanning**: Prevent committing API keys, tokens, or passwords to Git.
- **Workload Identity Federation (OIDC)**: Eliminates long-lived service principal client secrets; uses short-lived tokens between GitHub Actions / Azure DevOps and Azure.

---

## 📦 3. Package Management & Artifacts

- **Azure Artifacts / GitHub Packages**:
  - Feeds: NuGet, npm, Maven, PyPI, and Universal Packages.
  - Upstream sources to cache public packages safely.
- **Container Registries (Azure Container Registry - ACR)**:
  - Geo-replication for global multi-region deployments.
  - ACR Tasks: Automated image builds triggered by base-image updates or git commits.
  - Microsoft Defender for Containers vulnerability scanning.

---

## ⚙️ 4. Infrastructure as Code (IaC)

- **Terraform vs. Bicep**:
  - Terraform: Multi-cloud, state file management, mature module ecosystem.
  - Bicep: Azure native, zero state management overhead, Day-0 resource provider support.
- **Automated Validation in PRs**:
  - `terraform fmt -check`, `terraform validate`, `tflint`.
  - Security scanning with `tfsec` or `checkov`.
  - `terraform plan` posted directly as a comment on GitHub Pull Requests.
