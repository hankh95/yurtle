# Yurtle Specification v1.1 (December 2025)

Yurtle is minimal YAML front matter that turns any folder of Markdown files into a queryable knowledge graph.

## Rules (still only five)

1. Start with:
   ```yaml
   ---
   yurtle: v1.1
   id: unique/uri/like/this
   ---

### Evolution & Domain (optional – makes self-refactoring possible)

domain:               # the conceptual domain this asset belongs to
  - motivation        # exact string match of a TLP tech-name
  - tupugit
  - wonder
  # …or any custom domain you invent

evolves:              # explicit “this improves/replaces that” link
  - previous-id       # points to earlier version or weaker asset
  score: 0.84         # optional numeric confidence/impact (0–1)
  reason: Increased autonomy measurement granularity

version: 1.3.0        # optional – SimSemVer (simple semantic versioning) strongly recommended for anything in domain:*