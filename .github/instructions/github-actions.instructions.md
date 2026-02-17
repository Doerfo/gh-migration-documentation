---
applyTo: ".github/workflows/*.yml"
---
# GitHub Actions Workflow Guidelines

## Workflow Patterns in This Repository

This project uses two workflows:

1. **CI (`ci.yml`)** — Validates Jekyll builds on every push/PR.
2. **Pages (`pages.yml`)** — Builds and deploys to GitHub Pages on push to `main`.

## Conventions

- **Ruby setup**: Always use `ruby/setup-ruby@v1` with `bundler-cache: true` and explicit `ruby-version: '3.3'`.
- **Action versions**: Pin to the latest major version tag (e.g., `@v6`, `@v5`). Dependabot handles minor/patch updates.
- **Build command**: Use `bundle exec jekyll build` (with `--baseurl` for Pages deployment only).
- **Permissions**: Apply least-privilege: set `permissions` at workflow level, not job level.
- **Concurrency**: Pages deployment uses `concurrency.group: "pages"` with `cancel-in-progress: true`.

## Adding New Workflows

- Place in `.github/workflows/` with a descriptive filename.
- Trigger on appropriate events (`push`, `pull_request`, `workflow_dispatch`).
- Keep workflows focused on a single concern (build, deploy, lint, etc.).
- Do not duplicate the Jekyll build logic — reference the existing patterns in `ci.yml`.
- Ensure any new workflow that modifies repository content or deploys has appropriate permission scopes.
