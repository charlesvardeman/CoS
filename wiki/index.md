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

### COS-P007 — Make recurrence part of the experience, not the portable implementation

**Status:** accepted declared policy
**Origin:** heartbeat correction dialogue, 2026-09-02

A usable Chief of Staff includes one durable task and a recurring heartbeat by default. The portable skill defines the recurring behavior while each harness supplies the scheduler implementation. In Codex, configuration should create one native thread heartbeat with minimal ceremony after explicit approval.

### COS-P008 — Give each raw container its own policy

**Status:** accepted declared policy
**Origin:** raw-container design dialogue, 2026-09-02

`raw` means source evidence that has not been promoted into asserted semantic knowledge. It does not impose one location, format, Git rule, search surface, retention period, or disclosure posture. Readwise Markdown, paper manifests, and CoS trajectories may all be raw while following different declared container policies.

### COS-P009 — Begin learning with observable episode receipts

**Status:** accepted declared policy
**Origin:** minimum viable learning dialogue, 2026-09-02

Do not delay real use until a full harness exporter or software-style evaluation suite exists. A configured operational task should append privacy-minimized, ordered receipts of its observable episodes. Native harness traces may later enrich capture fidelity without changing the learning boundary.

### COS-P010 — The wiki adapter learns generalities only

**Status:** accepted declared policy
**Origin:** wiki-memory adapter dialogue, 2026-09-02

The separate wiki-memory adapter generalizes how the Chief of Staff should retrieve, verify, prioritize, route, communicate, and seek authorization. Specific people, projects, messages, literature, and current facts remain in the vault or their source systems. The operational task cannot consult the evolution wiki directly.

### COS-P011 — Reconcile project participation and role at the point of use

**Status:** confirmed declared policy
**Origin:** first operational episode and explicit generalization instruction, 2026-09-02
**Record:** [Project participant and role reconciliation](patterns/COS-P011-project-participant-role-reconciliation.md)

When an operational output depends on who is involved or what authority they hold, retrieve durable project context from the vault, compare it with relevant live participation evidence, distinguish event membership from durable role, and route material gaps through reviewed semantic capture. Do not infer authority from mere attendance or turn heartbeats into generic roster audits.

The procedure was adopted in operational skill `0.2.1` through accepted proposal [COS-SP001](proposals/COS-SP001-project-participant-role-reconciliation.md).

## Open Questions

- What minimum evidence changes an induced lesson from provisional to confirmed?
- How long should protected raw traces and delayed outcomes be retained?
- Which attention and omission metrics best predict usefulness in ordinary work?
- Which aspects of a learned workflow transfer between Codex and other harnesses?
- Should a reusable installation ship a read-only base evolution wiki or keep every evolving wiki external?
- Which durable harness signals should identify dedicated Chief-of-Staff tasks and CoS episodes inside mixed-purpose tasks?

## Supporting Records

- [Evolution log](evolution-log.md)
- [Skill impact](skill-impact.md)
- [COS-P011 pattern record](patterns/COS-P011-project-participant-role-reconciliation.md)
- [COS-SP001 skill proposal](proposals/COS-SP001-project-participant-role-reconciliation.md)
