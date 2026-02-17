# Azure DevOps to GitHub Migration – \<CUSTOMER\>

Documentation site for the migration of **\<CUSTOMER\>** from Azure DevOps to GitHub Enterprise Cloud. Built with [Jekyll] using the [Just the Docs] theme and published on [GitHub Pages].

## Placeholders

Replace the following placeholders throughout the documentation before publishing:

| Placeholder | Description | Example |
|---|---|---|
| `<CUSTOMER>` | Customer / organisation name | Contoso Ltd. |
| `<ENTERPRISE_SLUG>` | GitHub Enterprise slug (short code) | `contoso` |
| `<GITHUB_ORG>` | GitHub organisation name | `contoso-org` |
| `<GITHUB_PAGES_URL>` | URL where this docs site is published | `https://contoso.github.io/migration-docs` |
| `<MIGRATION_REPO_URL>` | URL of this repository on GitHub | `https://github.com/contoso-org/migration-docs` |
| `<ENTRA_TENANT_ID>` | Microsoft Entra ID (Azure AD) tenant ID | `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` |
| `<ENTRA_TENANT_NAME>` | Entra ID tenant display name | `contoso.onmicrosoft.com` |
| `<SETUP_USER>` | EMU setup user account | `<ENTERPRISE_SLUG>_admin` |
| `<OIDC_APP_NAME>` | Name of the OIDC enterprise app in Entra ID | `GitHub Enterprise Managed User (OIDC)` |
| `<SCIM_APP_NAME>` | Name of the SCIM provisioning app in Entra ID | `GitHub Enterprise Managed User (OIDC)` |
| `<ENTRA_ADMIN_ROLE>` | Entra ID role required for consent | Global Administrator |
| `<ADO_ORG_URL>` | Azure DevOps organisation URL | `https://dev.azure.com/contoso` |
| `<RESPONSIBLE_TEAM>` | Team / group responsible for the migration | Platform Engineering |
| `<MIGRATION_LEAD>` | Name or alias of the migration lead | `jdoe@contoso.com` |

## Documentation structure

| Page | Topic |
|---|---|
| `index.md` | User Synchronisation – Entra ID to GitHub (SCIM / OIDC) |
| *(future)* | Repository migration |
| *(future)* | Pipeline / Actions migration |
| *(future)* | Work‑item / project migration |
| *(future)* | Post‑migration validation |

## Building and previewing locally

Assuming [Jekyll] and [Bundler] are installed:

```bash
bundle install
bundle exec jekyll serve
```

Preview at `http://localhost:4000`.

## Publishing on GitHub Pages

1. Push to `main`.
2. Go to **Settings → Pages → Build and deployment → Source** and select **GitHub Actions**.

## License

This repository is licensed under the [MIT License].

[Jekyll]: https://jekyllrb.com
[Just the Docs]: https://just-the-docs.github.io/just-the-docs/
[GitHub Pages]: https://docs.github.com/en/pages
[Bundler]: https://bundler.io
[MIT License]: https://en.wikipedia.org/wiki/MIT_License
