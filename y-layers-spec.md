# Y-Layer Specification v2.0 (February 2026)

The Y-layer model defines **seven layers of knowledge** for AI beings. Each layer stores a different type of knowledge as Yurtle files with RDF/Turtle frontmatter.

---

## The 7-Layer Model

| Layer | Name | Content | Purpose |
|-------|------|---------|---------|
| **Y0** | Prose | Raw text chunks | Source documents, training corpus |
| **Y1** | Semantic | Entities, facts, K-blocks | Structured Wikipedia-like pages |
| **Y2** | Reasoning | Rules, ontology, constraints | Inference logic, class hierarchies |
| **Y3** | Experience | Conversations, actions | What the being did and said |
| **Y4** | Journal | Opinions, reflections | What the being thinks |
| **Y5** | Procedural | Workflows, skills | How to do things |
| **Y6** | Metacognitive | Calibration, patterns | Self-knowledge, error tracking |

### Definitional vs Experiential

```
DEFINITIONAL (What the being KNOWS)
├── Y0: Prose         — Raw source text
├── Y1: Semantic      — Entities, relationships
└── Y2: Reasoning     — Rules, ontology

EXPERIENTIAL (What the being DOES and THINKS)
├── Y3: Experience    — Actions, conversations
├── Y4: Journal       — Opinions, reflections
├── Y5: Procedural    — Workflows, skills
└── Y6: Metacognitive — Self-awareness, calibration
```

---

## Directory Structure

```
being/
└── memory/
    ├── Y0_prose/           # Raw text chunks with provenance
    │   └── {source}/
    │       └── *.md
    ├── Y1_semantic/        # Entity pages with K-blocks
    │   └── {source}/
    │       └── *.md
    ├── Y2_reasoning/       # Rules, ontology, constraints
    │   └── {domain}/
    │       └── *.md
    ├── Y3_experience/      # Conversations, learning events
    │   └── {date}/
    │       └── *.md
    ├── Y4_journal/         # Opinions, mental notes
    │   └── {date}/
    │       └── *.md
    ├── Y5_procedural/      # Workflows, skills
    │   └── *.md
    └── Y6_metacognitive/   # Calibration, error patterns
        └── *.md
```

---

## URI Prefixes

```turtle
@prefix y0: <https://nusy.dev/y0/> .  # Prose chunks
@prefix y1: <https://nusy.dev/y1/> .  # Semantic entities
@prefix y2: <https://nusy.dev/y2/> .  # Reasoning rules
@prefix y3: <https://nusy.dev/y3/> .  # Experience records
@prefix y4: <https://nusy.dev/y4/> .  # Journal entries
@prefix y5: <https://nusy.dev/y5/> .  # Procedural skills
@prefix y6: <https://nusy.dev/y6/> .  # Metacognitive records

# Common prefixes
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix owl: <http://www.w3.org/2002/07/owl#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix being: <https://nusy.dev/being/{id}/> .
```

---

## Layer Details

### Y0: Prose Layer

Raw text chunks with provenance tracking.

```markdown
---
@prefix y0: <https://nusy.dev/y0/> .
@prefix prov: <http://www.w3.org/ns/prov#> .

y0:chunk_001 a y0:ProseChunk ;
    y0:text "The three little pigs left home to seek their fortune..." ;
    prov:wasDerivedFrom <file:three_little_pigs.pdf> ;
    y0:page 1 ;
    y0:paragraph 1 .
---

# Three Little Pigs - Chunk 001

The three little pigs left home to seek their fortune...
```

**Types:** `y0:ProseChunk`, `y0:SourceDocument`

---

### Y1: Semantic Layer

Wikipedia-like entity pages with structured K-blocks.

```markdown
---
@prefix y1: <https://nusy.dev/y1/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

y1:Three_Little_Pigs a y1:Story ;
    rdfs:label "The Three Little Pigs" ;
    y1:genre "Fairy Tale" ;
    y1:theme "Hard work pays off" ;
    y1:characters y1:First_Pig, y1:Second_Pig, y1:Third_Pig, y1:Wolf ;
    y1:relatedTo y1:Goldilocks, y1:Little_Red_Riding_Hood .
---

# The Three Little Pigs

**Type:** Story
**Genre:** Fairy Tale

## Summary

A classic fairy tale about three pigs who build houses of straw, sticks,
and bricks, and a wolf who tries to blow them down.

## Knowledge Block

| Property | Value |
|----------|-------|
| Theme | Hard work pays off |
| Moral | Preparation prevents disaster |
| Origin | English folklore |

## Characters

- [[First_Pig]] — Built house of straw (lazy)
- [[Second_Pig]] — Built house of sticks (lazy)
- [[Third_Pig]] — Built house of bricks (industrious)
- [[Wolf]] — Antagonist who blows down houses

## Related

- [[Goldilocks]]
- [[Little_Red_Riding_Hood]]
```

**Types:** `y1:Entity`, `y1:Relationship`, `y1:KnowledgeBlock`, `y1:Story`, `y1:Character`, `y1:Concept`

---

### Y2: Reasoning Layer

Inference rules, ontology classes, and constraints.

```markdown
---
@prefix y2: <https://nusy.dev/y2/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix owl: <http://www.w3.org/2002/07/owl#> .

y2:FairyTale rdfs:subClassOf y2:Story .
y2:Story rdfs:subClassOf y2:Narrative .

y2:rule_moral_from_story a y2:InferenceRule ;
    y2:antecedent "?story a y2:FairyTale . ?story y1:moral ?moral ." ;
    y2:consequent "?moral a y2:LifeLesson ." ;
    y2:confidence 0.9 .
---

# Reasoning: Fairy Tale Ontology

## Class Hierarchy

- **FairyTale** ⊂ Story ⊂ Narrative

## Inference Rules

### Rule: Moral Extraction
```
IF ?story is a FairyTale
AND ?story has moral ?moral
THEN ?moral is a LifeLesson
```
**Confidence:** 0.9
```

**Types:** `y2:OntologyClass`, `y2:InferenceRule`, `y2:Constraint`

---

### Y3: Experience Layer

Conversations, actions, and learning events.

```markdown
---
@prefix y3: <https://nusy.dev/y3/> .
@prefix being: <https://nusy.dev/being/santiago/> .

being:conversation_001 a y3:Conversation ;
    y3:with "Teacher" ;
    y3:topic "fairy tales" ;
    y3:timestamp "2026-02-09T14:30:00Z" .

being:message_001 a y3:MessageReceived ;
    y3:inConversation being:conversation_001 ;
    y3:from "Teacher" ;
    y3:content "Tell me about the three little pigs" ;
    y3:timestamp "2026-02-09T14:30:05Z" .

being:learning_001 a y3:LearningEvent ;
    y3:inConversation being:conversation_001 ;
    y3:learnedFact y1:pigs_house_materials ;
    y3:from "Teacher" ;
    y3:timestamp "2026-02-09T14:31:00Z" .
---

# Conversation: Fairy Tales

**Date:** 2026-02-09 14:30
**With:** Teacher
**Topic:** fairy tales

## Transcript

**Teacher** (14:30:05): Tell me about the three little pigs.

**Me** (14:30:12): It's a story about three pigs who build houses...

## What I Learned

- **pigs_house_materials**: Straw, sticks, and bricks
- Source: Teacher (discussion)
```

**Types:** `y3:Conversation`, `y3:MessageReceived`, `y3:MessageSent`, `y3:LearningEvent`, `y3:Action`

---

### Y4: Journal Layer

Opinions, mental notes, and reflections.

```markdown
---
@prefix y4: <https://nusy.dev/y4/> .
@prefix being: <https://nusy.dev/being/santiago/> .

being:note_001 a y4:MentalNote ;
    y4:type y4:OBSERVATION ;
    y4:content "The wolf represents external threats" ;
    y4:trigger being:conversation_001 ;
    y4:timestamp "2026-02-09T14:35:00Z" .

being:evaluation_001 a y4:SourceEvaluation ;
    y4:source "Teacher" ;
    y4:trustLevel 0.95 ;
    y4:reason "Knowledgeable, consistent, patient" ;
    y4:timestamp "2026-02-09T14:40:00Z" .

being:reflection_001 a y4:SessionReflection ;
    y4:session being:conversation_001 ;
    y4:factsLearned 5 ;
    y4:keyInsight "Fairy tales encode cultural wisdom" ;
    y4:timestamp "2026-02-09T15:00:00Z" .
---

# Journal: 2026-02-09

## Mental Notes

### 14:35 - Observation
The wolf represents external threats and challenges.
*Triggered by: Fairy tale discussion*

## Source Evaluations

### Teacher
**Trust Level:** 0.95 (HIGH)
**Reason:** Knowledgeable, consistent, patient

## Session Summary

**Facts Learned:** 5
**Key Insight:** Fairy tales encode cultural wisdom through simple narratives.
```

**Types:** `y4:MentalNote`, `y4:SourceEvaluation`, `y4:SessionReflection`

**Note Types:** `y4:OBSERVATION`, `y4:QUESTION`, `y4:OPINION`, `y4:CONNECTION`, `y4:CONFUSION`

**Urgency Levels:** `y4:PURSUE_NOW`, `y4:DEFER`, `y4:LEAVE_ALONE`

---

### Y5: Procedural Layer

Workflows, skills, and how-to knowledge.

```markdown
---
@prefix y5: <https://nusy.dev/y5/> .
@prefix being: <https://nusy.dev/being/santiago/> .

being:skill_storytelling a y5:Skill ;
    y5:name "Story Recall" ;
    y5:description "Retrieve and narrate known stories" ;
    y5:requires y1:Story ;
    y5:proficiency 0.8 .

being:workflow_answer_question a y5:Workflow ;
    y5:name "Answer Story Question" ;
    y5:steps (
        y5:parse_question
        y5:retrieve_relevant_stories
        y5:extract_facts
        y5:compose_response
    ) .
---

# Skill: Story Recall

**Proficiency:** 0.8

## Description

Retrieve and narrate known stories from memory.

## Steps

1. Identify story being asked about
2. Retrieve Y1 entity page
3. Extract key facts and relationships
4. Compose narrative response

## Prerequisites

- Knowledge of story entities (Y1)
- Character relationships
```

**Types:** `y5:Skill`, `y5:Workflow`, `y5:Procedure`, `y5:Step`

---

### Y6: Metacognitive Layer

Self-awareness, calibration, and error patterns.

```markdown
---
@prefix y6: <https://nusy.dev/y6/> .
@prefix being: <https://nusy.dev/being/santiago/> .

being:calibration_001 a y6:CalibrationRecord ;
    y6:domain "fairy_tales" ;
    y6:confidence 0.85 ;
    y6:accuracy 0.82 ;
    y6:calibrationError 0.03 ;
    y6:timestamp "2026-02-09T16:00:00Z" .

being:pattern_001 a y6:ErrorPattern ;
    y6:type "overconfidence" ;
    y6:domain "character_details" ;
    y6:frequency 0.15 ;
    y6:mitigation "Verify character facts before stating" .
---

# Metacognition: Calibration Report

## Domain Calibration

| Domain | Confidence | Accuracy | Error |
|--------|------------|----------|-------|
| fairy_tales | 0.85 | 0.82 | 0.03 |
| characters | 0.80 | 0.65 | 0.15 |

## Error Patterns

### Overconfidence in Character Details
**Frequency:** 15% of responses
**Mitigation:** Verify character facts before stating with high confidence
```

**Types:** `y6:CalibrationRecord`, `y6:ErrorPattern`, `y6:KnowledgeBoundary`, `y6:ConfidenceThreshold`

---

## Design Principles

### TupuGit Principle

> "Files ARE the interface. Git IS the database. The LLM IS the query engine."

- Yurtle files are the canonical source of truth
- Git tracks all knowledge evolution
- Human-readable, LLM-consumable
- No external database required

### Graph Anywhere

Relationships declared where they make sense:
- **Frontmatter** — Document-level metadata (RDF/Turtle)
- **Wiki links** — Inline references (`[[entity]]`)
- **K-blocks** — Structured tables mid-document

### Layer Independence

Each layer can be:
- Loaded independently
- Queried by prefix (`y1:`, `y2:`, etc.)
- Persisted separately
- Evolved at different rates

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| **v2.0** | Feb 2026 | Y-layer specification (7 layers: Y0-Y6) |
| v1.3 | Dec 2025 | Yurtle blocks with code fence syntax |
| v1.2 | Dec 2025 | Three-layer model |
| v1.1 | Dec 2025 | Hierarchy (index, parent, children) |
| v1.0 | Nov 2025 | Core frontmatter |

---

MIT licensed · See [README.md](README.md)
