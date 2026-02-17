---
title: Advanced Security
parent: GitHub Configuration
nav_order: 3
---

# GitHub Advanced Security (GHAS)

## Overview

**GitHub Advanced Security** provides integrated security features directly within the developer workflow. For \<CUSTOMER\>, GHAS will replace or augment existing security tooling from the Azure DevOps environment.

GHAS includes three core capabilities:

| Feature | Description |
|---|---|
| **Code Scanning** | Static analysis (CodeQL) to find vulnerabilities in source code |
| **Secret Scanning** | Detects secrets (API keys, tokens, credentials) committed to repositories |
| **Dependency Review** | Identifies vulnerable dependencies before they are merged |

> **Reference:** [About GitHub Advanced Security](https://docs.github.com/en/enterprise-cloud@latest/get-started/learning-about-github/about-github-advanced-security)

---

## Enablement Strategy

### Phased Rollout

| Phase | Scope | Actions |
|---|---|---|
| **Phase 1** | Pilot repositories (*\<COUNT\>* repos) | Enable all GHAS features; tune alerts; establish triage process |
| **Phase 2** | Extend to critical / high-risk repositories | Onboard teams; refine code scanning queries |
| **Phase 3** | Enterprise-wide | Enable GHAS at organisation level for all repositories |

> **Decision:** Define the pilot repositories and rollout timeline with \<CUSTOMER\>.

---

## Code Scanning

Code scanning uses **CodeQL** (or third-party SARIF-compatible tools) to perform static application security testing (SAST).

### Configuration

1. **Default setup** (recommended for most repositories):
   - Enable *default setup* at the organisation level to automatically configure CodeQL for supported languages.
   - GitHub automatically detects languages and runs analysis on pull requests and pushes to the default branch.

2. **Advanced setup** (for custom configurations):
   - Define a `.github/workflows/codeql.yml` workflow in the repository.
   - Customise language matrix, query suites, and build steps.

### Organisation-Level Settings

| Setting | Recommended Value |
|---|---|
| Enable code scanning default setup | ✅ All repositories |
| Query suite | `security-and-quality` (or `security-extended`) |
| Alert severity threshold for PR checks | *\<SEVERITY\>* (e.g. `High` and `Critical`) |

> **Reference:** [Configuring default setup for code scanning at scale](https://docs.github.com/en/enterprise-cloud@latest/code-security/code-scanning/enabling-code-scanning/configuring-default-setup-for-code-scanning-at-scale)

---

## Secret Scanning

Secret scanning automatically detects tokens, keys, and other credentials committed to repositories.

### Configuration

| Setting | Recommended Value |
|---|---|
| Enable secret scanning | ✅ All repositories (organisation level) |
| Push protection | ✅ Enabled – blocks pushes containing detected secrets |
| Custom patterns | *\<ADD CUSTOMER-SPECIFIC PATTERNS IF NEEDED\>* |
| Alert notifications | Route to `<RESPONSIBLE_TEAM>` |

### Push Protection

When push protection is enabled, contributors are **blocked from pushing** commits that contain detected secrets. They can bypass the block with a documented reason, which is logged for audit.

> **Reference:** [About secret scanning](https://docs.github.com/en/enterprise-cloud@latest/code-security/secret-scanning/introduction/about-secret-scanning)

---

## Dependency Review

Dependency review helps identify vulnerable or unwanted dependencies before they are introduced via pull requests.

### Configuration

| Setting | Recommended Value |
|---|---|
| Dependency review enforcement | ✅ Enabled via repository ruleset or Actions workflow |
| Dependabot alerts | ✅ Enabled (organisation level) |
| Dependabot security updates | ✅ Enabled – auto-creates PRs for vulnerable dependencies |
| Dependabot version updates | *\<ENABLED / OPTIONAL\>* |

Add the dependency review GitHub Action to CI workflows:

```yaml
# .github/workflows/dependency-review.yml
name: Dependency Review
on: [pull_request]
permissions:
  contents: read
jobs:
  dependency-review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/dependency-review-action@v4
        with:
          fail-on-severity: high
```

> **Reference:** [Configuring dependency review](https://docs.github.com/en/enterprise-cloud@latest/code-security/supply-chain-security/understanding-your-software-supply-chain/configuring-dependency-review)

---

## Security Overview Dashboard

GitHub provides a **Security Overview** dashboard at the enterprise and organisation level. This gives \<CUSTOMER\> visibility into:

- Open code scanning alerts (by severity, repository, language)
- Secret scanning alerts and push protection bypasses
- Dependabot alerts across the organisation

> **Reference:** [About the security overview](https://docs.github.com/en/enterprise-cloud@latest/code-security/security-overview/about-security-overview)

---

## Validation Checklist

| # | Check | Status |
|---|---|---|
| 1 | GHAS licence enabled on enterprise | ☐ |
| 2 | Code scanning default setup enabled (org level) | ☐ |
| 3 | Secret scanning enabled (org level) | ☐ |
| 4 | Push protection enabled | ☐ |
| 5 | Dependabot alerts enabled | ☐ |
| 6 | Dependabot security updates enabled | ☐ |
| 7 | Dependency review action added to CI | ☐ |
| 8 | Security overview dashboard reviewed | ☐ |
| 9 | Alert triage process defined | ☐ |
| 10 | Custom secret scanning patterns added *(if applicable)* | ☐ |
