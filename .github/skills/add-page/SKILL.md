---
name: add-page
description: Guide for adding new documentation pages to this Jekyll site using Just the Docs theme. Use this when asked to add, create, or generate a new documentation page or section.
---

# Adding a New Documentation Page

This skill helps you add new pages to the Jekyll documentation site using the Just the Docs theme.

## Before You Start

1. **Check existing structure**: Review `docs/` directory to understand the current organization
2. **Identify parent section**: Determine where the new page fits in the navigation hierarchy
3. **Follow naming conventions**: Use lowercase filenames with hyphens (e.g., `my-new-page.md`)

## Page Structure Requirements

### Frontmatter Template

All pages must include YAML frontmatter at the top. Use this template:

```yaml
---
layout: default
title: Page Title
parent: Parent Section Title  # Required if page has a parent
grand_parent: Grandparent Title  # Only if nested 3 levels deep
nav_order: 1  # Controls position in navigation menu
has_children: false  # Set to true if this page will have child pages
has_toc: true  # Set to false to hide table of contents
---
```

### Key Frontmatter Fields

- **layout**: Always use `default` for content pages
- **title**: The page title displayed in navigation and as the H1
- **parent**: The title of the parent page (must match exactly)
- **nav_order**: Lower numbers appear first in navigation
- **has_children**: Set to `true` for section index pages (like `index.md` in a category folder)
- **has_toc**: Set to `false` for short pages or lists where TOC isn't helpful

## File Placement Rules

### Section Index Pages
- Location: `docs/<section-name>/index.md`
- Frontmatter: Must include `has_children: true`
- Example: `docs/architecture/index.md`

### Child Pages
- Location: `docs/<section-name>/<page-name>.md`
- Frontmatter: Must include `parent: Section Title`
- Example: `docs/architecture/source-system.md`

### Subsections (3-level hierarchy)
- Location: `docs/<section>/<subsection>/page.md`
- Frontmatter: Must include both `parent` and `grand_parent`

## Content Guidelines

### 1. Preserve Placeholders
Always preserve `<PLACEHOLDER>` tokens used throughout the site:
- `<CUSTOMER>`
- `<ENTERPRISE_SLUG>`
- `<GITHUB_ORG>`
- `<GITHUB_TEAM>`
- `<AZURE_TENANT_ID>`
- And others listed in README.md

**Never** replace placeholders with concrete values.

### 2. Use Just the Docs Components

**Callouts:**
```markdown
{: .warning }
> This is a warning callout

{: .note }
> This is a note callout

{: .highlight }
> This is a highlight callout
```

**Code blocks with titles:**
```markdown
```yaml
# filename: config.yml
key: value
\```
```

**Navigation links:**
Reference other pages using relative paths in standard markdown links.

### 3. Linking to GitHub Documentation

Use `enterprise-cloud@latest` path for GitHub Enterprise Cloud docs:
```markdown
[GitHub Enterprise Cloud documentation](https://docs.github.com/en/enterprise-cloud@latest/...)
```

### 4. Audience and Tone

- **Target audience**: Enterprise platform engineers and migration leads
- **Tone**: Professional, precise, and actionable
- **Style**: Use imperative mood for instructions ("Configure", "Set up", "Enable")

## Workflow Steps

When adding a new page:

1. **Determine location**: Identify the appropriate `docs/` subdirectory
2. **Check parent pages**: Ensure parent section exists and has `has_children: true`
3. **Create the file**: Use descriptive filename with `.md` extension
4. **Add frontmatter**: Include all required fields with correct parent references
5. **Write content**: Follow content guidelines and preserve placeholders
6. **Verify navigation**: Check that `nav_order` is appropriate
7. **Test locally** (if requested): Run `bundle exec jekyll serve` to preview

## Examples

### Adding a New Section

Create `docs/my-section/index.md`:

```markdown
---
layout: default
title: My Section
nav_order: 3
has_children: true
---

# My Section

Overview of this section...
```

### Adding a Page to Existing Section

Create `docs/github-configuration/api-access.md`:

```markdown
---
layout: default
title: API Access Configuration
parent: GitHub Configuration
nav_order: 4
---

# API Access Configuration

This guide covers configuring API access for `<GITHUB_ORG>`...

## Prerequisites

- GitHub Enterprise Cloud account
- Organization owner permissions

## Configuration Steps

1. Navigate to `<GITHUB_ORG>` organization settings
2. ...
```

### Adding a Subsection Page

Create `docs/architecture/security/authentication.md`:

```markdown
---
layout: default
title: Authentication
parent: Security
grand_parent: Architecture
nav_order: 1
---

# Authentication

Details about authentication architecture...
```

## Common Pitfalls to Avoid

❌ **Don't** use backticks around file references in display text - use markdown links
❌ **Don't** fill in placeholder values with real data
❌ **Don't** forget to set `has_children: true` on parent pages
❌ **Don't** mismatch parent titles (must match exactly)
❌ **Don't** skip the `layout: default` field

✅ **Do** check existing pages for pattern examples
✅ **Do** maintain consistent nav_order spacing (e.g., 1, 2, 3 or 10, 20, 30)
✅ **Do** use Just the Docs callouts for warnings and notes
✅ **Do** link to official GitHub documentation when appropriate

## Additional Resources

- Just the Docs documentation: https://just-the-docs.github.io/just-the-docs/
- UI Components: https://just-the-docs.github.io/just-the-docs/docs/ui-components/
- Navigation guide: https://just-the-docs.github.io/just-the-docs/docs/navigation-structure/

## Need More Examples?

Use GitHub MCP tools to search the Just the Docs repository:
```
mcp_github_search_code: repo:just-the-docs/just-the-docs path:docs extension:md [search term]
```
