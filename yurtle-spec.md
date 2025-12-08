# Yurtle Specification v1.3 (December 2025)

Yurtle is minimal YAML front matter + inline blocks that turn any folder of Markdown files into a queryable knowledge graph.

## The Three-Layer Model

| Layer | Location | Syntax | Purpose |
|-------|----------|--------|---------|
| **Frontmatter** | Top of file | `---` YAML `---` | Document metadata |
| **Content** | Body | Markdown + `[[links]]` | Human prose |
| **Yurtle Blocks** | Anywhere | ` ```yurtle ``` ` | Inline structured data |

---

## Layer 1: Frontmatter

### Required

```yaml
---
yurtle: v1.3
id: unique/path/id
---
```

### Recommended

```yaml
---
yurtle: v1.3
id: unique/path/id
type: note | person | project | asset | log
title: Human Readable Name
status: draft | active | complete | archived
topics: [tag1, tag2]
relates-to: [other/id, another/id]
nugget: One-sentence summary
created: 2025-12-01
---
```

### Hierarchy

```yaml
path: folder/location
index:
  discoverable: true
  parent: parent-id
  children: [child-1, child-2]
```

### Evolution

```yaml
domain: [nautical, logistics]
evolves:
  - previous-id
  score: 0.91
  reason: Why this version is better
version: 1.3.0
```

---

## Layer 2: Content Body

Standard markdown with optional wiki links:

```markdown
The [[ship|Windchaser]] departed at dawn.
See [[crew-captain-reed]] for command structure.
```

Relationships can be implicit in prose:
- "X **depends on** Y" → `depends-on: Y`
- "X **part of** Y" → `part-of: Y`

---

## Layer 3: Yurtle Blocks

Inline structured data using code fence syntax:

~~~markdown
```yurtle
ship:
  title: Windchaser
  built: 1852
  part-of: voyage
  crewed-by: crew
```
~~~

### Syntax Rules

1. **Same as frontmatter** — `key: value` pairs
2. **Indentation** — 2 spaces for properties
3. **Subject** — Top-level key with colon (e.g., `ship:`)
4. **Values** — Strings, numbers, or IDs (no quotes needed)

### Multiple Subjects

```yurtle
captain:
  name: Elias Reed
  commands: ship

navigator:
  name: Mei-Xing Lee
  reports-to: captain
```

### Optional Base

```yurtle
@base nautical-project/

ship:
  part-of: voyage
```

All IDs resolve relative to `nautical-project/`.

### Lists

```yurtle
crew:
  members:
    - captain-reed
    - navigator-lee
    - bosun-chen
  size: 20
```

---

## Design Principles

### Files Are the Interface
- No database required
- Git tracks everything
- LLMs read markdown directly

### Graph Anywhere
- Frontmatter for document metadata
- Wiki links for inline references
- Yurtle blocks for structured data mid-document

### Consistent Syntax
- Frontmatter and blocks use identical `key: value` format
- Learn once, use everywhere

---

## Version History

| Version | Changes |
|---------|---------|
| **v1.3** | Yurtle blocks with ` ```yurtle ``` ` code fence |
| v1.2 | Three-layer model concept |
| v1.1 | Hierarchy (index, parent, children) |
| v1.0 | Core frontmatter |

---

MIT licensed · See [README.md](README.md)
