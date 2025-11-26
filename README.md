# Yurtle — YAML front matter that thinks like a graph

**Yurtle** = YAML + Turtle spirit.  
A dead-simple, human-first way to make every Markdown file part of a living knowledge graph — without writing any Turtle, RDF, or prefixes.

Just add a normal YAML block at the top of any `.md` file.  
That’s it. Tools can now turn your entire folder of notes into a searchable, queryable graph.

No dependencies. No config. Works with Obsidian, Logseq, plain Git, or any future AI memory system.

```yaml
---
yurtle: v1
id: notes/2025/11/26-my-idea
type: idea
title: Reusable coffee filters made from mushroom leather
status: seed
topics:
  - sustainability
  - materials
  - coffee
relates-to:
  - notes/people/alice
  - notes/projects/mycofilter-v1
nugget: One sentence essence
created: 2025-11-26
---
