---
title: User Synchronisation – Entra ID to GitHub
layout: home
nav_order: 1
---

# Azure DevOps to GitHub Migration – \<CUSTOMER\>

This documentation covers the migration of **\<CUSTOMER\>** from **Azure DevOps** to **GitHub Enterprise Cloud** using **Enterprise Managed Users (EMU)**.

The first phase of the migration focuses on **identity and access management**: synchronising users from **Microsoft Entra ID** (formerly Azure AD) to GitHub via **OIDC** single sign-on and **SCIM** provisioning.

---

## User Synchronisation Overview

With Enterprise Managed Users, \<CUSTOMER\> manages the full lifecycle of GitHub user accounts from Entra ID:

- **Provisioning** – User accounts are automatically created on GitHub when assigned in Entra ID.
- **Profile sync** – Username, display name, and email are kept in sync from Entra ID.
- **De-provisioning** – Removing or disabling a user in Entra ID automatically disables the corresponding GitHub account.
- **Group mapping** – Entra ID groups can be mapped to GitHub teams for automatic organisation and repository access.

> **Note:** Managed user accounts cannot create public content or collaborate outside the \<CUSTOMER\> enterprise on GitHub.

---

## Authentication – OIDC Single Sign-On

\<CUSTOMER\> will use **OpenID Connect (OIDC)** for SSO authentication. OIDC is only supported with Microsoft Entra ID and provides the following advantages over SAML:

- **Conditional Access Policy (CAP) support** – GitHub validates every session and token-based interaction against Entra ID's CAP IP conditions.
- **Managed certificates** – Certificates are managed by GitHub and Entra ID; no manual certificate rotation required.
- **Session lifetime control** – Token lifetime can be configured via Entra ID policies.

### Prerequisites

| # | Prerequisite | Details |
|---|---|---|
| 1 | GitHub Enterprise Cloud account with EMU | Enterprise slug: `<ENTERPRISE_SLUG>` |
| 2 | Setup user access | Sign in as `<SETUP_USER>` (`<ENTERPRISE_SLUG>_admin`) |
| 3 | Entra ID tenant | Tenant: `<ENTRA_TENANT_NAME>` (`<ENTRA_TENANT_ID>`) |
| 4 | Entra ID admin rights | A user with **`<ENTRA_ADMIN_ROLE>`** is required to consent to the OIDC app |
| 5 | Recovery codes downloaded | Store securely before enabling SSO |

### Configuration Steps

1. Sign in to GitHub as the setup user **`<SETUP_USER>`**.
2. Navigate to **Your enterprises → \<CUSTOMER\> enterprise → Identity provider → Single sign-on configuration**.
3. Under *OIDC single sign-on*, select **Enable OIDC configuration** and click **Save**.
4. GitHub redirects to Entra ID. Sign in with an account that has **`<ENTRA_ADMIN_ROLE>`** rights.
5. Review permissions for the **`<OIDC_APP_NAME>`** application and select *Consent on behalf of your organization*, then click **Accept**.
6. Back on GitHub, **download recovery codes** and store them securely.
7. Click **Enable OIDC Authentication**.

> **Important:** Each Entra ID tenant supports only **one** OIDC integration with Enterprise Managed Users. If multiple enterprises need to connect to the same tenant, use SAML for the additional enterprises.

### Reference

- [Configuring OIDC for Enterprise Managed Users](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-iam/configuring-authentication-for-enterprise-managed-users/configuring-oidc-for-enterprise-managed-users)
- [About support for your IdP's Conditional Access Policy](https://docs.github.com/en/enterprise-cloud@latest/admin/identity-and-access-management/using-enterprise-managed-users-for-iam/about-support-for-your-idps-conditional-access-policy)

---

## Provisioning – SCIM with Entra ID

After OIDC SSO is enabled, **SCIM** (System for Cross-domain Identity Management) provisioning must be configured so that Entra ID can manage user lifecycle on GitHub.

### User Lifecycle with SCIM

| Event in Entra ID | Effect on GitHub |
|---|---|
| User assigned to the GitHub EMU app | Account provisioned; user added to the enterprise |
| User profile updated | Profile (name, email) updated on GitHub |
| User unassigned / disabled | GitHub account disabled; sessions invalidated; username hashed |
| User re-assigned / re-enabled | Account reactivated; original username restored |

### Prerequisites

| # | Prerequisite | Details |
|---|---|---|
| 1 | OIDC SSO enabled | Completed in the previous section |
| 2 | Entra ID admin access | To configure the provisioning app |
| 3 | Entra ID groups | Groups that map to GitHub organisations / teams (created or identified) |

### Configuration Steps

1. In Entra ID, open the **`<SCIM_APP_NAME>`** enterprise application (created during OIDC setup).
2. Go to **Provisioning → Get started**.
3. Set *Provisioning Mode* to **Automatic**.
4. In the *Admin Credentials* section, enter:
   - **Tenant URL:** `https://api.github.com/scim/v2/enterprises/<ENTERPRISE_SLUG>`
   - **Secret Token:** Generate a **Personal Access Token (classic)** from the `<SETUP_USER>` account with the `admin:enterprise` scope, or use the token provided during OIDC setup.
5. Click **Test Connection** to verify.
6. Configure **Mappings** (user attributes and group mappings) per the [Microsoft tutorial](https://learn.microsoft.com/en-us/entra/identity/saas-apps/github-enterprise-managed-user-oidc-provisioning-tutorial).
7. Set the **Scope** to *Sync only assigned users and groups* (recommended).
8. Turn provisioning **On** and click **Save**.

> **Note:** Entra ID does **not** support provisioning nested groups. Ensure all user assignments are in flat groups.

### Assigning Users and Groups

- Assign individual users or Entra ID groups to the **`<SCIM_APP_NAME>`** app.
- Use the **Roles** attribute in Entra ID to set the user's enterprise role on GitHub:
  - `Enterprise Owner`
  - `Enterprise Member` (default)
  - `Guest Collaborator`
- Map Entra ID groups to GitHub **teams** for automatic organisation membership and repository access. See [Managing team memberships with identity provider groups](https://docs.github.com/en/enterprise-cloud@latest/admin/identity-and-access-management/using-enterprise-managed-users-for-iam/managing-team-memberships-with-identity-provider-groups).

### Reference

- [Configuring SCIM provisioning for Enterprise Managed Users](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-iam/provisioning-user-accounts-with-scim/configuring-scim-provisioning-for-users)
- [Tutorial: Configure GitHub EMU (OIDC) for automatic user provisioning (Microsoft Learn)](https://learn.microsoft.com/en-us/entra/identity/saas-apps/github-enterprise-managed-user-oidc-provisioning-tutorial)

---

## Username Conventions

GitHub automatically generates usernames for managed users by normalising an identifier from Entra ID. The format is:

```
<normalised-idp-username>_<ENTERPRISE_SLUG>
```

For example, if the Entra ID UPN is `jdoe@contoso.com` and the enterprise slug is `contoso`, the GitHub username will be `jdoe_contoso`.

> See [Username considerations for external authentication](https://docs.github.com/en/enterprise-cloud@latest/admin/identity-and-access-management/managing-iam-for-your-enterprise/username-considerations-for-external-authentication) for normalisation rules and conflict resolution.

---

## Guest Collaborators

To grant vendors or contractors limited access, \<CUSTOMER\> can use the **Guest Collaborator** role. Guest collaborators:

- Only have access to **internal** repositories in organisations where they are a member.
- Must be assigned the guest collaborator role via Entra ID.

Additional Entra ID configuration may be required. See [Enabling guest collaborators](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-accounts-and-repositories/managing-users-in-your-enterprise/enabling-guest-collaborators).

---

## Validation Checklist

| # | Check | Status |
|---|---|---|
| 1 | OIDC SSO enabled on GitHub Enterprise | ☐ |
| 2 | Recovery codes downloaded and stored securely | ☐ |
| 3 | SCIM provisioning app configured in Entra ID | ☐ |
| 4 | Test connection successful | ☐ |
| 5 | Pilot users provisioned and can sign in | ☐ |
| 6 | Group → Team mapping verified | ☐ |
| 7 | User de-provisioning tested (disable in Entra ID → account disabled on GitHub) | ☐ |
| 8 | CAP / Conditional Access policies validated | ☐ |

---

## Responsible Contacts

| Role | Contact |
|---|---|
| Migration Lead | `<MIGRATION_LEAD>` |
| Responsible Team | `<RESPONSIBLE_TEAM>` |
| GitHub Enterprise Owner | `<SETUP_USER>` |
| Entra ID Administrator | `<ENTRA_ADMIN_ROLE>` holder |
