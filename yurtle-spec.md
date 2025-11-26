# Yurtle Specification v1 (November 2025)

Yurtle is YAML front matter designed to be instantly converted into clean RDF/Turtle triples.

## Rules (there are only five)

1. Every file that wants to be in the graph starts with exactly:
   ```yaml
   ---
   yurtle: v1
   id: unique/uri/like/this (relative or absolute)
   # ... rest of your keys
   ---
   ```

2. Required fields:
   - `yurtle: v1`
   - `id:` — unique identifier (becomes the subject URI)

3. Recommended common fields (use any or all):
   ```yaml
   type: note | person | project | recipe | idea | ...
   title: Human name
   status: draft | active | archived | seed | done
   topics:
     - list
     - of tags
   relates-to:
     - other/id/1
     - other/id/2
   nugget: One-sentence summary (optional but gold)
   created: 2025-11-26
   updated: 2025-11-26
   ```

4. You may add any custom keys you want — they all become predicates.

5. Nested data is allowed and encouraged:
   ```yaml
   author:
     name: Alice
     role: materials-lead
   location:
     city: Portland
     country: USA
   ```

## Auto-conversion to real Turtle (one-liner tools coming)

Your YAML:
```yaml
id: people/alice
type: person
name: Alice Chen
topics: [mycology, coffee]
relates-to: projects/mycofilter
```

→ becomes valid Turtle:
```turtle
<people/alice> a :Person ;
    :name "Alice Chen" ;
    :topics "mycology", "coffee" ;
    :relates-to <projects/mycofilter> .
```

Zero config. Works today with any folder of Markdown files.

Use it for personal notes, Zettelkasten, team wiki, AI memory, or just because.

Yurtle: because your thoughts deserve to be connected.
