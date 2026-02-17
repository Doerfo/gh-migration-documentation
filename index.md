---
title: Introduction
layout: home
nav_order: 1
---

# Azure DevOps to GitHub Migration – \<CUSTOMER\>

## Project Motivation

\<CUSTOMER\> is migrating its software development platform from **Azure DevOps** to **GitHub Enterprise Cloud** to modernise its development workflows, improve developer experience, and leverage GitHub's ecosystem for collaboration, security, and automation.

### Why Migrate?

| Driver | Description |
|---|---|
| **Developer Experience** | GitHub provides a modern, widely adopted platform that developers already know. Reducing context-switching and onboarding friction accelerates delivery. |
| **Inner Source & Collaboration** | GitHub's pull request model, Discussions, and organisation-wide visibility enable inner source practices across \<CUSTOMER\>. |
| **Security & Compliance** | GitHub Advanced Security (GHAS) offers integrated code scanning, secret scanning, and dependency review directly in the developer workflow. |
| **AI-Assisted Development** | GitHub Copilot and Copilot Chat provide AI-powered coding assistance, available natively on the platform. |
| **Ecosystem & Integrations** | GitHub Actions, Packages, and the GitHub Marketplace offer a rich ecosystem that reduces the need for third-party tooling. |
| **Identity & Access Management** | Enterprise Managed Users (EMU) with Entra ID integration provides centralised identity governance via OIDC and SCIM. |

### Migration Scope

This migration covers the following areas:

1. **Identity & Access** – User provisioning from Entra ID via SCIM/OIDC (Enterprise Managed Users)
2. **Repository Migration** – Source code, history, and branches from Azure DevOps Git repositories
3. **Pipeline Migration** – Azure Pipelines to GitHub Actions
4. **Work Item Migration** – Azure Boards to GitHub Issues / Projects *(if applicable)*
5. **Security Enablement** – GitHub Advanced Security (code scanning, secret scanning, dependency review)

### Out of Scope

- Migration of Azure DevOps Artifacts (NuGet, npm feeds) – *to be evaluated separately*
- Azure DevOps Test Plans – *no direct GitHub equivalent; alternative tooling to be assessed*
- Azure DevOps Wiki – *content to be migrated manually or via scripting if required*

---

## How to Use This Documentation

This site is structured into the following sections:

| Section | Description |
|---|---|
| **[Architecture](docs/architecture/)** | Overview of the source system (Azure DevOps) and the target architecture on GitHub |
| **[GitHub Configuration](docs/github-configuration/)** | Step-by-step configuration guides for the GitHub Enterprise, Entra ID integration, and Advanced Security |

Each section contains sub-pages with detailed instructions, prerequisites, and validation checklists.

---

## Key Contacts

| Role | Contact |
|---|---|
| Migration Lead | `<MIGRATION_LEAD>` |
| Responsible Team | `<RESPONSIBLE_TEAM>` |
| GitHub Enterprise Owner | `<SETUP_USER>` |
| Entra ID Administrator | *\<ENTRA_ID_ADMIN\>* |
