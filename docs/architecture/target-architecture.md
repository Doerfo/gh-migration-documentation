---
title: Target Architecture
parent: Architecture
nav_order: 2
---

# Target Architecture – GitHub Enterprise Cloud

## Overview

The target platform is **GitHub Enterprise Cloud** with **Enterprise Managed Users (EMU)**. This provides \<CUSTOMER\> with a fully managed, cloud-hosted development platform where user lifecycle is governed from **Microsoft Entra ID**.

## Enterprise Structure

```
GitHub Enterprise Cloud
└── Enterprise: <ENTERPRISE_SLUG>
    ├── Organisation: <GITHUB_ORG>
    │   ├── Team A  ←  mapped from Entra ID group
    │   │   ├── repo-service-a
    │   │   ├── repo-service-b
    │   │   └── ...
    │   ├── Team B  ←  mapped from Entra ID group
    │   │   ├── repo-frontend
    │   │   └── ...
    │   └── ...
    ├── Organisation: <GITHUB_ORG_2> (if applicable)
    │   └── ...
    └── ...
```

> **Decision:** Document whether \<CUSTOMER\> will use a single organisation or multiple organisations within the enterprise, and the rationale.

## Platform Capabilities Mapping

| Capability | Azure DevOps | GitHub Enterprise Cloud |
|---|---|---|
| Source Control | Azure Repos (Git) | GitHub Repositories |
| CI/CD | Azure Pipelines | GitHub Actions |
| Package Management | Azure Artifacts | GitHub Packages |
| Work Tracking | Azure Boards | GitHub Issues & Projects |
| Code Security | *3rd party / manual* | GitHub Advanced Security (GHAS) |
| Secret Management | Azure Key Vault (pipeline integration) | GitHub Actions Secrets + Azure Key Vault |
| Identity | Entra ID → Azure DevOps | Entra ID → GitHub EMU (OIDC + SCIM) |
| AI Assistance | *N/A* | GitHub Copilot |
| Documentation | Azure DevOps Wiki | GitHub Wikis / Markdown in repo / GitHub Pages |

## Identity & Access Architecture

```
┌──────────────┐       OIDC SSO       ┌──────────────────────┐
│  Microsoft   │ ──────────────────── │  GitHub Enterprise   │
│  Entra ID    │                      │  Cloud (EMU)         │
│              │       SCIM           │                      │
│  Users &     │ ──────────────────── │  Managed User        │
│  Groups      │   provisioning      │  Accounts            │
└──────────────┘                      └──────────────────────┘
       │                                       │
       │  Conditional Access                   │  Organisation &
       │  Policies (CAP)                       │  Team membership
       ▼                                       ▼
  IP restrictions,                       Repository access,
  MFA, device compliance                 role-based permissions
```

- **Authentication:** OIDC single sign-on via Entra ID
- **Provisioning:** SCIM automatic user lifecycle management
- **Authorisation:** Entra ID groups → GitHub teams → repository permissions
- **Conditional Access:** Entra ID CAP policies enforced on every GitHub session and API call

For detailed configuration steps, see [Entra ID Integration](../github-configuration/entra-id-integration).

## Network & Security

| Aspect | Detail |
|---|---|
| Data Residency | GitHub Enterprise Cloud (hosted by GitHub; see [GitHub data residency options](https://docs.github.com/en/enterprise-cloud@latest/admin/data-residency/about-github-enterprise-cloud-with-data-residency)) |
| IP Allow Lists | *\<CONFIGURE IF REQUIRED\>* |
| Private Networking | GitHub-hosted runners / self-hosted runners with Azure VNet integration |
| Audit Logging | GitHub Audit Log → *\<SIEM / Log Analytics target\>* |

## GitHub Actions – Runner Strategy

| Runner Type | Use Case |
|---|---|
| GitHub-hosted runners | Standard CI/CD workloads (Linux, Windows, macOS) |
| Larger GitHub-hosted runners | Performance-intensive builds |
| Self-hosted runners (Azure VNet) | Workloads requiring private network access to Azure resources |

> **Decision:** Document the runner strategy, including whether self-hosted runners are needed and where they will be hosted.

## Licensing

| Product | Licence Type | Quantity |
|---|---|---|
| GitHub Enterprise Cloud | EMU | *\<COUNT\>* |
| GitHub Advanced Security | Per committer | *\<COUNT\>* |
| GitHub Copilot Business / Enterprise | Per seat | *\<COUNT\>* |
