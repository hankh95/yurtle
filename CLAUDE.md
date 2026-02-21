# Yurtle — Claude Code Instructions

The Yurtle format specification: YAML/TTL frontmatter that turns Markdown into queryable RDF graphs. Dual audience: machines (RDF triples) and humans (readable Markdown).

## Project Overview

- **Type:** Specification / Documentation
- **Format:** Markdown with examples

## Development Practices

### Branch + PR Pattern (Required)

All changes go through feature branches and pull requests:

1. Create a feature branch: `git checkout -b feat-short-description`
2. Do all work on the branch — **never push directly to main**
3. Push and create PR: `gh pr create`
4. Get review from another developer/agent before merging

### Code Quality

- Prefer editing existing files over creating new ones
- Spec changes should include examples
- Keep the specification clear and concise

## Related Projects

- **yurtle-rdflib** — Python library for parsing Yurtle format
- **yurtle-kanban** — Kanban system built on Yurtle
- **nusy-product-team** — Primary consumer of the Yurtle format
