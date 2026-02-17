---
title: Source System
parent: Architecture
nav_order: 1
---

# Source System – Azure DevOps

## Overview

\<CUSTOMER\> currently uses **Azure DevOps** (`<ADO_ORG_URL>`) as its primary software development platform. The following services are in active use:

| Azure DevOps Service | Usage | Migration Target |
|---|---|---|
| Azure Repos (Git) | Source code management | GitHub Repositories |
| Azure Pipelines | CI/CD | GitHub Actions |
| Azure Boards | Work item tracking | GitHub Issues / Projects |
| Azure Artifacts | Package management | GitHub Packages / *TBD* |
| Azure Test Plans | Test management | *Out of scope / TBD* |
| Azure DevOps Wiki | Documentation | *Manual migration / TBD* |

## Organisation Structure

```
<ADO_ORG_URL>
├── Project A
│   ├── Repos
│   ├── Pipelines
│   └── Boards
├── Project B
│   ├── Repos
│   ├── Pipelines
│   └── Boards
└── ...
```

> **Note:** Document the actual Azure DevOps organisation structure, including project names, repository counts, and pipeline counts.

## Identity & Access

- **Authentication:** \<CUSTOMER\> users authenticate to Azure DevOps via **Microsoft Entra ID** (`<ENTRA_TENANT_NAME>`).
- **Authorisation:** Access is managed through Azure DevOps security groups, project-level permissions, and repository-level policies.
- **Service Connections:** Pipelines use service connections for deployments to Azure and other environments.

## Key Metrics

| Metric | Value |
|---|---|
| Number of Projects | *\<COUNT\>* |
| Number of Repositories | *\<COUNT\>* |
| Number of Pipelines (YAML + Classic) | *\<COUNT\>* |
| Number of Active Users | *\<COUNT\>* |
| Total Repository Size | *\<SIZE\>* |
| Largest Repository | *\<REPO_NAME\> (\<SIZE\>)* |

## Dependencies & Integrations

Document any integrations between Azure DevOps and other systems that need to be considered during migration:

- **Azure Key Vault** – secrets used in pipelines
- **Azure Container Registry** – container image builds and pushes
- **SonarQube / SonarCloud** – code quality gates
- **Slack / Teams** – notification integrations
- **Jira** – work item linking *(if applicable)*
- *\<ADD FURTHER INTEGRATIONS\>*
