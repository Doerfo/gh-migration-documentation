---
applyTo: "**/*.md"
---
# Markdown Documentation Guidelines

> **Reference:** [Just the Docs Documentation](https://just-the-docs.github.io/just-the-docs/)

## Just the Docs Frontmatter

Every documentation page must include YAML frontmatter with these fields:

```yaml
---
title: Page Title
parent: Parent Section Title    # required for child pages
nav_order: 1                    # controls sidebar ordering
has_toc: true                   # optional, for section index pages
layout: default                 # usually inherited from _config.yml defaults
---
```

### Navigation Structure Requirements

- **Top-level pages** must have unique titles.
- **Pages with the same parent** must have unique titles.
- **Section index pages** (e.g., `docs/architecture/index.md`) use `has_toc: true` and omit `parent`.
- **Child pages** must set `parent` to match the exact `title` of their section index.
- `nav_order` values are integers starting at 1 within each section.
- The theme supports **unlimited navigation depth** (v0.10.0+).

### Advanced Navigation (Edge Cases)

If your site has pages with the same title in different sections, use `grand_parent` or `ancestor` for disambiguation:

```yaml
---
title: Configuration
parent: Azure DevOps
grand_parent: Source Systems
---
```

> **Reference:** [Navigation Structure](https://just-the-docs.github.io/just-the-docs/docs/navigation/)

### Hiding Auto-Generated Child Lists

By default, parent pages display a table of contents linking to child pages. Disable with:

```yaml
---
title: Section Index
has_toc: false
---
```

> **Reference:** See [`has_toc` documentation](https://github.com/just-the-docs/just-the-docs/blob/main/docs/navigation/children.md)

## Content Structure

- Start each page with an H1 heading (`#`) matching the `title` in frontmatter.
- Use H2 (`##`) for major sections, H3 (`###`) for subsections.
- Use Markdown tables for structured data (settings, metrics, comparisons).

## Callouts

Just the Docs provides styled callouts using kramdown block IALs (Inline Attribute Lists). Configure callout types in `_config.yml`:

```yaml
callouts:
  note:
    title: Note
    color: purple
  warning:
    title: Warning
    color: red
  important:
    title: Important
    color: blue
```

### Single-Paragraph Callouts

```markdown
{: .note }
A single paragraph callout.
```

{: .note }
A single paragraph callout.

### Multi-Paragraph Callouts

Use blockquote syntax for multi-paragraph callouts:

```markdown
{: .warning }
> First paragraph of the warning.
>
> Second paragraph with more details.
```

{: .warning }
> First paragraph of the warning.
>
> Second paragraph with more details.

### Custom Callout Titles

```markdown
{: .important-title }
> Custom Title Here
>
> Content of the callout with a custom title.
```

> **Reference:** [Callouts Documentation](https://just-the-docs.github.io/just-the-docs/docs/ui-components/callouts/)

### This Project's Callout Patterns

- `{: .note }` or `> **Note:**` — Informational callouts
- `{: .warning }` — Warnings and cautions  
- `> **Reference:**` — Links to official GitHub Enterprise Cloud docs
- `> **Decision:**` — Items requiring customer input during migration

## Placeholder System

This project uses angle-bracket placeholders that must be preserved:

- `<CUSTOMER>`, `<ENTERPRISE_SLUG>`, `<GITHUB_ORG>`, `<ENTRA_TENANT_ID>`, etc.
- In Markdown body text, escape angle brackets: `\<CUSTOMER\>` to prevent HTML parsing.
- In code blocks and table cells, use unescaped: `<CUSTOMER>`.
- Never substitute placeholder values with example data unless explicitly instructed.
- Refer to `README.md` for the complete placeholder reference table.

## Writing Style

- Write for an enterprise audience: platform engineers, migration leads, and IT administrators.
- Be concise and actionable — use numbered steps for procedures, tables for settings.
- Use **bold** for product names, UI elements, and setting names.
- Use `backticks` for slugs, URLs, CLI commands, and configuration values.
- Link to official GitHub docs using the `enterprise-cloud@latest` path variant.
- Maintain consistency with existing page patterns — review sibling pages before adding new content.

## Code Blocks

Use fenced code blocks with language identifiers:

````markdown
```yaml
key: value
```
````

Supported languages include `yaml`, `bash`, `ruby`, `markdown`, `json`, `powershell`, etc.

## Tables

Use GitHub Flavored Markdown table syntax:

```markdown
| Column 1 | Column 2 | Column 3 |
|---|---|---|
| Value A | Value B | Value C |
```

## Links

- **Internal pages:** Use relative paths: `[Target Architecture](target-architecture)` or `[Architecture Overview](../architecture/)`
- **External docs:** Use full URLs with descriptive text: `[GitHub Enterprise Cloud Documentation](https://docs.github.com/en/enterprise-cloud@latest)`
- **Anchor links:** `[Configuration Section](#configuration)` (auto-generated from headings)

## File Naming

- Use lowercase, hyphen-separated names: `entra-id-integration.md`, `source-system.md`.
- Section index pages are always named `index.md`.
- Place new pages in the appropriate `docs/` subdirectory.

## Additional Resources

- **Just the Docs Theme:** [https://just-the-docs.github.io/just-the-docs/](https://just-the-docs.github.io/just-the-docs/)
- **GitHub Repository:** [https://github.com/just-the-docs/just-the-docs](https://github.com/just-the-docs/just-the-docs)
- **UI Components:** [https://just-the-docs.github.io/just-the-docs/docs/ui-components/](https://just-the-docs.github.io/just-the-docs/docs/ui-components/)
- **Configuration:** [https://just-the-docs.github.io/just-the-docs/docs/configuration/](https://just-the-docs.github.io/just-the-docs/docs/configuration/)

For implementation examples, use GitHub MCP tools to search the [just-the-docs/just-the-docs](https://github.com/just-the-docs/just-the-docs) repository.
