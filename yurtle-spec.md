# Yurtle Specification v1.2 (December 2025)

Yurtle is minimal YAML front matter that turns any folder of Markdown files into a queryable knowledge graph.

## The Three-Layer Semantic Model

Every Yurtle page can express relationships through three layers:

| Layer | Location | Purpose |
|-------|----------|---------|
| **Frontmatter** | YAML header at top | Explicit metadata |
| **Content** | Markdown body | Prose + wiki links |
| **Infoboxes** | Anywhere in content | Structured data blocks |

This enables **"graph anywhere"** — relationships declared where they make sense.

---

## Layer 1: Frontmatter

### Required Fields

```yaml
---
yurtle: v1.2
id: unique/uri/like/this
---
```

### Core Fields (recommended)

```yaml
---
yurtle: v1.2
id: unique/uri/like/this          # required - globally unique
type: note | person | project | asset | log | ...
title: Human Readable Name
status: draft | active | complete | archived
topics: [list, of, tags]
relates-to: [other/id, another/id]
nugget: One-sentence essence for search results
created: 2025-12-01
---
```

### Hierarchy & Discovery

```yaml
path: folder/location             # physical location hint
index:
  discoverable: true|false        # include in auto-indexes (default: true)
  parent: id-or-path              # container node
  children:                       # contained nodes
    - child-id-1
    - child-id-2
```

### Evolution & Domain

```yaml
domain:                           # conceptual domains
  - motivation
  - sustainability
  - your-custom-domain

evolves:                          # version tracking
  - previous-id                   # what this replaces
  score: 0.84                     # confidence (0-1)
  reason: Why this is better

version: 1.3.0                    # SemVer for versioned assets
```

---

## Layer 2: Content Body

The main Markdown content. Relationships can be expressed through:

### Wiki Links

```markdown
See [[nautical/voyage]] for the full journey.
The captain is [[nautical/crew-captain-reed]].
```

### Natural Language (LLM-parseable)

```markdown
The Windchaser **depends on** a full crew complement.
This voyage **builds upon** the 1851 expedition.
The manifest **is required by** the harbor master.
```

LLMs can extract typed relationships from prose:
- `depends_on: crew`
- `builds_upon: 1851-expedition`
- `required_by: harbor-master`

---

## Layer 3: Infoboxes

Structured data blocks that can appear **anywhere** in content.

### Syntax

```markdown
<!-- infobox:type-name -->
| Property | Value |
|----------|-------|
| Key1 | Value1 |
| Key2 | Value2 |
<!-- /infobox -->
```

### Common Types

**Asset/Thing:**
```markdown
<!-- infobox:ship -->
| Property | Value |
|----------|-------|
| Name | Windchaser |
| Type | Clipper |
| Built | 1852 |
| Length | 62m |
<!-- /infobox -->
```

**Person:**
```markdown
<!-- infobox:person -->
| Property | Value |
|----------|-------|
| Name | Captain Elias Reed |
| Role | Master & Commander |
| Born | 1809 |
<!-- /infobox -->
```

**Relationships:**
```markdown
<!-- infobox:relationships -->
| Relationship | Target | Notes |
|--------------|--------|-------|
| requires | crew.md | Minimum 20 |
| uses | manifest.md | Cargo tracking |
| part-of | voyage.md | Current expedition |
<!-- /infobox -->
```

**Status:**
```markdown
<!-- infobox:status -->
| Metric | Value |
|--------|-------|
| Progress | 60% |
| Days Remaining | 34 |
| Crew Health | Excellent |
<!-- /infobox -->
```

### Infobox Best Practices

1. Use semantic type names: `ship`, `person`, `relationships`, `status`
2. Keep tables focused — one concern per infobox
3. Place infoboxes near the content they describe
4. Use consistent column names across similar types

---

## Design Principles

### Files Are the Interface

- State lives in files, not databases
- Git tracks all changes automatically
- LLMs read files directly — no query language needed

### Graph Anywhere

Unlike databases where relationships are stored separately, Yurtle lets you declare relationships where they make sense:

- **Document-level** → Frontmatter
- **In prose** → Wiki links and natural language
- **Structured mid-page** → Infoboxes

### LLM-Native

```
User: What ships are in the fleet?

LLM: *reads voyage.md frontmatter*
     *finds relates-to: [ship.md]*
     *reads ship.md, finds infobox:ship*
     
     The Windchaser, a 62m clipper built in 1852.
```

No query language. Just markdown.

---

## Version History

| Version | Date | Key Changes |
|---------|------|-------------|
| v1.2 | Dec 2025 | Three-layer model, infoboxes, graph-anywhere |
| v1.1 | Dec 2025 | Hierarchy (index, parent, children) |
| v1.0 | Nov 2025 | Core frontmatter (id, type, relates-to) |

---

MIT licensed · See [README.md](README.md) for examples.
