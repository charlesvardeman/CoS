# CoS Evolution Wiki

This wiki is the persistent procedural memory used to improve the Chief-of-Staff skills. It contains generalizations, counterexamples, open questions, and evidence references. It is not the user's semantic vault and must not contain an inventory of specific people, projects, documents, messages, or commitments.

Operational Chief-of-Staff runs do not read this wiki. It is maintained and consulted only during the separate evolution workflow.

## Accepted Design Patterns

### COS-P001 — Separate semantic facts from procedural learning

**Status:** accepted declared policy
**Origin:** design dialogue, 2026-09-02

Store specific information objects and their relationships in the personal vault. Store generalized retrieval, verification, prioritization, routing, and communication strategies in this wiki.

### COS-P002 — Learn how to retrieve, not what currently exists

**Status:** accepted declared policy
**Origin:** design dialogue, 2026-09-02

The skill should learn navigation strategies and source-selection rules. It should retrieve the current people, projects, literature, deadlines, and commitments when needed instead of copying them into procedural memory.

### COS-P003 — Keep operational inference separate from evolution

**Status:** accepted design decision
**Origin:** WikiSkill adaptation dialogue, 2026-09-02

The operational agent receives the accepted skill but not the evolution wiki. A separate Maintainer and Proposer workflow analyzes traces and proposes changes.

### COS-P004 — Codex memory is not the raw layer

**Status:** accepted design decision
**Origin:** Codex trace adaptation dialogue, 2026-09-02

Codex memory is selective and consolidated. Continual learning requires normalized, temporally ordered run evidence with observable actions and outcomes. Memory may suggest a question but cannot bypass trace-based review.

### COS-P005 — Begin read-mostly

**Status:** accepted declared policy
**Origin:** Chief-of-Staff scope dialogue, 2026-09-02

Begin with read-only retrieval and draft generation. External mutation and semantic-memory writes require explicit approval. Do not perform automatic semantic capture.

### COS-P006 — Store contracts in skills and instances outside them

**Status:** accepted provisional design
**Origin:** package-composition dialogue, 2026-09-02

Skills contain stable operating instructions and portable contracts. User-specific configuration, watermarks, pending actions, trace evidence, and outcome records remain outside installed skill directories so that skill replacement does not overwrite state or distribute private values.

### COS-P007 — Compose scheduling instead of bundling it

**Status:** accepted provisional design
**Origin:** Loop and package-composition dialogue, 2026-09-02

The Chief-of-Staff skill defines recurring-run behavior but does not own scheduling. A Codex profile may supply the separate `loop` skill; another harness may supply an equivalent scheduler.

## Open Questions

- What minimum evidence changes an induced lesson from provisional to confirmed?
- How long should protected raw traces and delayed outcomes be retained?
- Which attention and omission metrics best predict usefulness in ordinary work?
- Which aspects of a learned workflow transfer between Codex and other harnesses?
- Should a reusable installation ship a read-only base evolution wiki or keep every evolving wiki external?

## Supporting Records

- [Evolution log](evolution-log.md)
- [Skill impact](skill-impact.md)
