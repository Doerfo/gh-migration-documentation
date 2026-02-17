---
title: Resources
nav_order: 4
has_toc: true
---

# Resources

This page provides a curated list of official documentation and resources to support the Azure DevOps to GitHub Enterprise Cloud migration for \<CUSTOMER\>.

---

## Core Migration Tools & Guides

### GitHub Enterprise Importer

GitHub Enterprise Importer (GEI) is the recommended tool for migrating repositories to GitHub Enterprise Cloud.

- **[Using GitHub Enterprise Importer](https://docs.github.com/en/migrations/using-github-enterprise-importer){:target="_blank" rel="noopener noreferrer"}** – Main documentation hub for GEI
- **[About GitHub Enterprise Importer](https://docs.github.com/en/migrations/using-github-enterprise-importer/understanding-github-enterprise-importer/about-github-enterprise-importer){:target="_blank" rel="noopener noreferrer"}** – Overview of capabilities and supported source systems
- **[Migrating from Azure DevOps to GitHub Enterprise Cloud](https://docs.github.com/en/migrations/using-github-enterprise-importer/migrating-from-azure-devops-with-github-enterprise-importer){:target="_blank" rel="noopener noreferrer"}** – Specific guide for Azure DevOps migrations

{: .note }
> GitHub Enterprise Importer supports migrating Git repositories, including history, branches, and commit metadata. It does **not** migrate Azure Pipelines, work items, or wiki content.

---

## Identity & Access Management

### Enterprise Managed Users (EMU) with Entra ID

Enterprise Managed Users provide centralized identity and access control via Microsoft Entra ID (formerly Azure AD).

- **[Tutorial: Provision users into GitHub Enterprise Managed User (OIDC)](https://learn.microsoft.com/entra/identity/saas-apps/github-enterprise-managed-user-oidc-provisioning-tutorial){:target="_blank" rel="noopener noreferrer"}** – Microsoft Entra ID provisioning setup guide
- **[Configuring OIDC for Enterprise Managed Users](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-iam/configuring-authentication-for-enterprise-managed-users/configuring-oidc-for-enterprise-managed-users){:target="_blank" rel="noopener noreferrer"}** – GitHub OIDC authentication configuration
- **[About Enterprise Managed Users](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-iam/understanding-iam-for-enterprises/about-enterprise-managed-users){:target="_blank" rel="noopener noreferrer"}** – Overview of EMU features and constraints
- **[Configuring SCIM provisioning for Enterprise Managed Users with Entra ID](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-iam/provisioning-user-accounts-with-scim/configuring-scim-provisioning-for-enterprise-managed-users-with-entra-id){:target="_blank" rel="noopener noreferrer"}** – User lifecycle management via SCIM

---

## GitHub Enterprise Cloud Administration

### General Administration

- **[GitHub Enterprise Cloud Admin Documentation](https://docs.github.com/en/enterprise-cloud@latest/admin){:target="_blank" rel="noopener noreferrer"}** – Complete admin guide
- **[Managing organizations in your enterprise](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-accounts-and-repositories/managing-organizations-in-your-enterprise){:target="_blank" rel="noopener noreferrer"}** – Organization structure and governance
- **[Setting policies for your enterprise](https://docs.github.com/en/enterprise-cloud@latest/admin/policies){:target="_blank" rel="noopener noreferrer"}** – Enterprise-level policy configuration
- **[Managing GitHub Actions for your enterprise](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-github-actions-for-your-enterprise){:target="_blank" rel="noopener noreferrer"}** – Actions policies, runners, and usage controls

### Security & Compliance

- **[GitHub Advanced Security documentation](https://docs.github.com/en/enterprise-cloud@latest/code-security){:target="_blank" rel="noopener noreferrer"}** – Code scanning, secret scanning, and dependency review
- **[Enabling GitHub Advanced Security for your enterprise](https://docs.github.com/en/enterprise-cloud@latest/admin/code-security/managing-github-advanced-security-for-your-enterprise/enabling-github-advanced-security-for-your-enterprise){:target="_blank" rel="noopener noreferrer"}** – GHAS activation and licensing
- **[Managing security and analysis settings for your organization](https://docs.github.com/en/enterprise-cloud@latest/organizations/keeping-your-organization-secure/managing-security-settings-for-your-organization/managing-security-and-analysis-settings-for-your-organization){:target="_blank" rel="noopener noreferrer"}** – Organization-level security controls

---

## GitHub Actions

### Migration & Security

- **[Migrating from Azure Pipelines to GitHub Actions](https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/manual-migrations/migrate-from-azure-pipelines){:target="_blank" rel="noopener noreferrer"}** – Manual migration guide
- **[Understanding the differences between Azure Pipelines and GitHub Actions](https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-azure-pipelines-to-github-actions){:target="_blank" rel="noopener noreferrer"}** – Conceptual mapping between platforms
- **[Security hardening for GitHub Actions](https://docs.github.com/en/actions/security-for-github-actions/security-guides/security-hardening-for-github-actions){:target="_blank" rel="noopener noreferrer"}** – Best practices for secure workflows
- **[Using OpenID Connect with Azure](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-azure){:target="_blank" rel="noopener noreferrer"}** – Keyless authentication to Azure resources from GitHub Actions

### GitHub Actions Runners

- **[About self-hosted runners](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/about-self-hosted-runners){:target="_blank" rel="noopener noreferrer"}** – On-premises or cloud-based runner configuration
- **[Using larger runners](https://docs.github.com/en/enterprise-cloud@latest/actions/using-github-hosted-runners/using-larger-runners){:target="_blank" rel="noopener noreferrer"}** – GitHub-hosted runners with more resources

---

## GitHub Packages (Artifact Management)

- **[Introduction to GitHub Packages](https://docs.github.com/en/packages/learn-github-packages/introduction-to-github-packages){:target="_blank" rel="noopener noreferrer"}** – GitHub's integrated artifact registry (NuGet, npm, Maven, Docker, etc.)
- **[Working with the NuGet registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-nuget-registry){:target="_blank" rel="noopener noreferrer"}** – Publishing and consuming NuGet packages
- **[Working with the npm registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-npm-registry){:target="_blank" rel="noopener noreferrer"}** – Publishing and consuming npm packages

---

## Work Item & Project Management

- **[About GitHub Issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues){:target="_blank" rel="noopener noreferrer"}** – GitHub's work item system
- **[About GitHub Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects){:target="_blank" rel="noopener noreferrer"}** – GitHub's project management tool
- **[Quickstart for Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/quickstart-for-projects){:target="_blank" rel="noopener noreferrer"}** – Getting started with GitHub Projects

{: .note }
> There is no automated migration path for Azure Boards work items to GitHub Issues. Work items can be migrated via the GitHub CLI or custom scripting. Evaluate whether historical work items need to be migrated or if only active items should be transferred.

---

## Additional Resources

### Training & Learning Paths

- **[Introduction to GitHub](https://learn.microsoft.com/training/modules/introduction-to-github/){:target="_blank" rel="noopener noreferrer"}** – Microsoft Learn module for GitHub fundamentals
- **[Introduction to version control with Git](https://learn.microsoft.com/training/paths/intro-to-vc-git/){:target="_blank" rel="noopener noreferrer"}** – Git fundamentals training path
- **[GitHub Actions learning path](https://learn.microsoft.com/training/paths/automate-workflow-github-actions/){:target="_blank" rel="noopener noreferrer"}** – Automating workflows with GitHub Actions

### API & Extensibility

- **[GitHub REST API documentation](https://docs.github.com/en/rest){:target="_blank" rel="noopener noreferrer"}** – Complete REST API reference
- **[GitHub GraphQL API documentation](https://docs.github.com/en/graphql){:target="_blank" rel="noopener noreferrer"}** – GraphQL API for advanced queries
- **[GitHub CLI (gh)](https://cli.github.com/){:target="_blank" rel="noopener noreferrer"}** – Command-line interface for GitHub

### Support & Community

- **[GitHub Support](https://support.github.com/){:target="_blank" rel="noopener noreferrer"}** – Official GitHub support portal
- **[GitHub Community Discussions](https://github.com/orgs/community/discussions){:target="_blank" rel="noopener noreferrer"}** – Community-driven Q&A and discussions
- **[GitHub Changelog](https://github.blog/changelog/){:target="_blank" rel="noopener noreferrer"}** – Latest feature announcements and updates

---

## Related Documentation Sections

| Section | Description |
|---|---|
| **[Architecture](../architecture/)** | Overview of source and target systems |
| **[GitHub Configuration](../github-configuration/)** | Step-by-step configuration guides |
