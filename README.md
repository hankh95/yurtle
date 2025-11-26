Yes — **absolutely** do it.

The README is the front door.  
Right now most visitors only see the tiny example in the current README and never scroll to `yurtle-spec.md`. If we leave the new v1.1 fields (especially `path` and `index`) buried in the spec file, 90% of people will miss the whole reason we just shipped v1.1.

So: **replace the current README almost entirely** with this updated version below.  
It keeps the spirit ultra-light, but now instantly shows the full power (including hierarchy) in the very first screen.

### New `README.md` (copy-paste this exactly)

```markdown
# Yurtle — YAML front matter that turns Markdown into a living graph

**Yurtle** = the simplest way to make every `.md` file in a folder part of a real, queryable knowledge graph.

Just add a normal YAML block at the top of any Markdown file.  
That’s it.

```yaml
---
yurtle: v1.1
id: nautical/voyage
type: voyage
title: The Crossing of the Western Sea
path: nautical
index:
  discoverable: true
  parent: nautical
  children:
    - nautical/ship
    - nautical/crew
nugget: A three-month voyage to chart the uncharted archipelago
---
```

No plugins. No database. Works with Obsidian, Logseq, plain Git, or any future AI memory system...

### Core fields (recommended)
```yaml
yurtle: v1.1
id: unique/uri/like/this          # required
type: note | person | voyage | ship | ...
title: Human name
status: draft | active | sailing | docked
topics: [list, of, tags]
relates-to: [other/id, another/id]
nugget: One-sentence essence
created: 2025-12-01
```

### New in v1.1 — Hierarchy & Discovery
```yaml
path: folder/location             # e.g. expeditions/001 or crew
index:
  discoverable: true|false        # default true
  parent: id-or-path              # container
  children:                       # what lives inside this file
    - child-id-1
    - child-id-2
```

Your folder structure becomes part of the graph. Tools can now auto-generate wikis, sitemaps, or Mermaid diagrams from nothing but Markdown + Yurtle.

**See the full nautical demo** → `examples/nautical/`  
A tiny, complete, beautiful graph that feels alive (four files, fully connected).

MIT licensed · Fork, extend, build your own fleet.