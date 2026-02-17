---
title: General
parent: GitHub Configuration
nav_order: 1
---

# General Configuration

## Enterprise Settings

The following enterprise-level settings should be configured for the \<CUSTOMER\> enterprise (`<ENTERPRISE_SLUG>`).

### Enterprise Policies

| Policy | Recommended Setting | Notes |
|---|---|---|
| Base repository permission | `No permission` (or `Read`) | Repositories default to no access; teams grant explicit access |
| Repository creation | `Disabled` for members | Only organisation owners / admins can create repositories |
| Repository forking | `Disabled` | Prevent forks of internal/private repositories outside the enterprise |
| Repository visibility change | `Disabled` for members | Prevent accidental exposure of private repositories |
| Default repository visibility | `Internal` | Visible within the enterprise; not public |
| GitHub Pages creation | *\<POLICY\>* | Restrict or allow per organisational need |
| Copilot | *\<ENABLED / RESTRICTED\>* | Configure Copilot access at enterprise or organisation level |

> **Reference:** [Enforcing policies for your enterprise](https://docs.github.com/en/enterprise-cloud@latest/admin/policies/enforcing-policies-for-your-enterprise)

### Audit Log Configuration

- Enable **audit log streaming** to \<CUSTOMER\>'s SIEM or Azure Monitor workspace.
- Retain audit logs per compliance requirements.

> **Reference:** [Streaming the audit log](https://docs.github.com/en/enterprise-cloud@latest/admin/monitoring-activity-in-your-enterprise/reviewing-audit-logs-for-your-enterprise/streaming-the-audit-log-for-your-enterprise)

---

## Organisation Settings

Configure the following for each organisation within the enterprise (e.g. `<GITHUB_ORG>`).

### Member Privileges

| Setting | Recommended Value |
|---|---|
| Base permission | `No permission` |
| Allow members to create repositories | `No` |
| Allow forking of private/internal repos | `No` |
| Allow members to change visibility | `No` |
| Allow members to delete/transfer repos | `No` |
| Allow members to create teams | *\<YES / NO\>* |

### Branch Protection & Rulesets

Define default **repository rulesets** at the organisation level:

| Rule | Setting |
|---|---|
| Require pull request before merging | ✅ Enabled |
| Required approvals | *\<COUNT\>* (e.g. 1 or 2) |
| Dismiss stale reviews on new commits | ✅ Enabled |
| Require status checks to pass | ✅ Enabled |
| Require conversation resolution | ✅ Enabled |
| Require signed commits | *\<YES / NO\>* |
| Restrict force pushes | ✅ Enabled |
| Restrict deletions | ✅ Enabled |

> **Reference:** [Managing rulesets for an organisation](https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-organization-settings/managing-rulesets-for-repositories-in-your-organization)

---

## Repository Defaults

| Setting | Value |
|---|---|
| Default branch name | `main` |
| License | *\<LICENSE_TYPE\>* |
| `.gitignore` template | *Per technology stack* |
| README | Required |
| `CODEOWNERS` | Required – enforced via ruleset |

### Repository Topics & Naming Conventions

Define naming conventions for repositories to ensure consistency:

```
<team>-<service>-<component>
```

Example: `platform-auth-service`, `frontend-web-app`

> **Decision:** Define and agree on repository naming conventions with \<CUSTOMER\>.

---

## GitHub Actions Configuration

| Setting | Value |
|---|---|
| Actions permissions | Allow select actions (GitHub-authored + verified marketplace) |
| Default workflow permissions | `Read` |
| Required approvals for workflows from forks | *\<POLICY\>* |
| Self-hosted runner groups | *\<RUNNER_GROUP_NAME\>* |

### Reusable Workflows & Actions

- Maintain a **central repository** for shared GitHub Actions workflows (e.g. `<GITHUB_ORG>/.github`).
- Use organisation-level **action policies** to restrict which actions are allowed.

> **Reference:** [Managing GitHub Actions settings for an organisation](https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-organization-settings/disabling-or-limiting-github-actions-for-your-organization)
