# Repository-Wide Copilot Instructions

## Project Overview

This is a **Jekyll documentation site** for an Azure DevOps to GitHub Enterprise Cloud migration project. It uses the **Just the Docs** theme and is deployed to **GitHub Pages** via GitHub Actions.

## Tech Stack

- **Static site generator:** Jekyll 4.4.x (Ruby)
- **Theme:** Just the Docs 0.12.x
- **Hosting:** GitHub Pages (via GitHub Actions workflow)
- **CI:** GitHub Actions (`ci.yml` for build checks, `pages.yml` for deployment)
- **Dependency management:** Bundler (Gemfile), Dependabot for automated updates

## Project Structure

```
index.md                        ← Site homepage (Introduction & migration scope)
_config.yml                     ← Jekyll configuration
Gemfile                         ← Ruby dependencies
docs/
├── architecture/               ← Source system & target architecture docs
│   ├── index.md
│   ├── source-system.md
│   └── target-architecture.md
└── github-configuration/       ← GitHub config guides (enterprise, Entra ID, GHAS)
    ├── index.md
    ├── general.md
    ├── entra-id-integration.md
    └── advanced-security.md
.github/
├── workflows/                  ← CI and Pages deployment workflows
└── dependabot.yml              ← Automated dependency updates
```

## Key Conventions

- **Placeholders**: The documentation uses `<PLACEHOLDER>` tokens (e.g., `<CUSTOMER>`, `<ENTERPRISE_SLUG>`, `<GITHUB_ORG>`) that must be replaced before publishing. See `README.md` for the full list. Never invent concrete values for these placeholders — always preserve them as-is.
- **Audience**: Enterprise platform engineers and migration leads. Content should be professional, precise, and actionable.
- **References**: Link to official GitHub Enterprise Cloud documentation where appropriate using the `enterprise-cloud@latest` URL path.

## Just the Docs Theme

This site uses the [Just the Docs](https://just-the-docs.github.io/just-the-docs/) Jekyll theme (v0.12.0). Key resources:

- **Documentation:** [https://just-the-docs.github.io/just-the-docs/](https://just-the-docs.github.io/just-the-docs/)
- **GitHub Repository:** [https://github.com/just-the-docs/just-the-docs](https://github.com/just-the-docs/just-the-docs)
- **Configuration Guide:** [https://just-the-docs.github.io/just-the-docs/docs/configuration/](https://just-the-docs.github.io/just-the-docs/docs/configuration/)
- **UI Components:** [https://just-the-docs.github.io/just-the-docs/docs/ui-components/](https://just-the-docs.github.io/just-the-docs/docs/ui-components/)

### Finding Examples

When working with Just the Docs features (navigation, callouts, layouts, etc.), use **GitHub MCP tools** to search the theme repository for implementation examples:

```
mcp_github_search_code: repo:just-the-docs/just-the-docs [your search query]
mcp_github_get_file_contents: owner:just-the-docs, repo:just-the-docs, path:[file path]
```

Examples:
- Search for callout usage: `repo:just-the-docs/just-the-docs path:docs extension:md "{: .warning }"`
- Get navigation examples: `owner:just-the-docs, repo:just-the-docs, path:docs/navigation/main/`
- Find frontmatter patterns: `repo:just-the-docs/just-the-docs path:docs extension:md has_toc`

## Development Workflow

- **Local preview**: `bundle install && bundle exec jekyll serve` → `http://localhost:4000`
- **CI**: Every push/PR triggers `ci.yml` (Jekyll build check)
- **Deployment**: Pushing to `main` triggers `pages.yml` which builds and deploys to GitHub Pages
- **Dependencies**: Managed via Dependabot (daily checks for Bundler gems and GitHub Actions)
