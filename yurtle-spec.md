# Yurtle Specification v2.1 (February 2026)

Yurtle is minimal YAML/RDF front matter + inline blocks that turn any folder of Markdown files into a queryable knowledge graph.

**New in v2.0:** Y-layer specification for AI beings — see [y-layers-spec.md](y-layers-spec.md)

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
yurtle: v2.0
id: unique/path/id
---
```

### Recommended

```yaml
---
yurtle: v2.0
id: unique/path/id
type: note | person | project | asset | log
title: Human Readable Name
status: draft | active | complete | archived
topics: [tag1, tag2]
relates-to: [other/id, another/id]
nugget: One-sentence summary
created: 2026-02-09
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

### Tabular Blocks (`yurtle-table`)

The core thesis is *one format, two audiences*. A plain `yurtle` block is
scannable for a single subject, but a **set of same-shaped subjects** (a
voyage's phases, a Y-layer summary, a hypothesis→experiment→measure matrix)
reads best as a **table** — yet a markdown table is not queryable, and writing
both a table and a `yurtle` block duplicates the data. The `yurtle-table` fenced
block removes the duplication: **it IS a markdown table, and it IS RDF.**

~~~markdown
```yurtle-table
@type Phase

| @id       | label                             | phase-order | phase-item        |
|-----------|-----------------------------------|-------------|-------------------|
| #phase-1  | Architect instruction (CLAUDE.md) | 1           | PR-187            |
| #phase-2  | Fleet voyage awareness            | 2           | EXP-1020, EXP-1021 |
| #phase-3  | Voyage CLI commands               | 3           | EXP-1022          |
| #phase-4  | Research interlinks               | 4           |                   |
```
~~~

Any markdown viewer renders the above as a table; a yurtle parser emits:

```yurtle
phase-1:
  a: Phase
  label: Architect instruction (CLAUDE.md)
  phase-order: 1
  phase-item: PR-187

phase-2:
  a: Phase
  label: Fleet voyage awareness
  phase-order: 2
  phase-item:
    - EXP-1020
    - EXP-1021
```

*(…and so on. In Turtle: `<#phase-1> a :Phase ; :label "…" ; :phase-order 1 ; :phase-item "PR-187" .`)*

**Rules**

1. **Header row = predicates.** Each column header is a property key resolved
   exactly like a `yurtle`-block key (bare key against the document vocabulary;
   a declared-prefix CURIE such as `rdfs:label` is also accepted).
2. **`@id` column = subject.** Required; each row's `@id` cell is that row's
   subject (resolved against `@base` like any other id).
3. **Type — declaration or column.** An `@type <Type>` line *before* the table
   sets `rdf:type` for **every** row. An optional **`@type` column** sets it
   **per row** and overrides the declaration. (Answers design Q1: both are
   supported; column wins.)
4. **Empty cell = no triple.** A blank cell emits nothing for that
   (subject, predicate) — it is absence, not an empty-string value.
5. **Multi-value cells.** A comma-separated cell emits **one triple per value**
   (identical to a `yurtle` list) — see `phase-item` above. (Answers design Q3.)
6. **Literals follow yurtle inference.** Values are typed the same way as
   elsewhere in yurtle — a bare number is a numeric literal, an id-shaped token
   (`#foo`) is a resource, everything else is a string. No `^^xsd:` annotation
   is needed; when explicit datatyping is required, use a plain `yurtle` block
   instead. (Answers design Q2.)
7. **Graceful fallback.** A viewer that does not recognize `yurtle-table`
   renders it as a fenced code block *containing a readable markdown table* —
   still fully human-scannable, never a parse error. (Answers design Q4.)

*(Parser support tracked separately in yurtle-rdflib.)*

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
| **v2.1** | `yurtle-table` block: tabular RDF — one markdown table, two audiences (human-scannable + machine-queryable) |
| v2.0 | Y-layer specification (7 layers: Y0-Y6) for AI beings |
| v1.3 | Yurtle blocks with ` ```yurtle ``` ` code fence |
| v1.2 | Three-layer model concept |
| v1.1 | Hierarchy (index, parent, children) |
| v1.0 | Core frontmatter |

---

MIT licensed · See [README.md](README.md)
