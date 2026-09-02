# Chief-of-Staff Architecture

## Purpose

The Chief of Staff maintains a bounded operational view across projects and information channels. It should bring actionable changes to the user's attention, recover the specific context required for a decision, and prepare useful drafts without becoming another source of truth.

The architecture separates portable procedure, personal knowledge, live source state, operational scheduling, and continual learning. That separation is the main defense against stale instructions, uncontrolled semantic capture, and harness lock-in.

## Responsibility Model

| Component | Responsibility | Authority |
|---|---|---|
| `chief-of-staff` skill | Retrieve, reconcile, prioritize, brief, and draft | Procedural runtime behavior |
| `configure-chief-of-staff` skill | Discover capabilities and propose user-specific source, attention, and authorization policy | Configuration workflow, not configuration storage |
| Personal vault | People, projects, literature, decisions, commitments, and curated context | Specific semantic knowledge |
| Connected systems | Current email, calendar, task, reference, and reading state | Current source state within approved scopes |
| Specialist tasks | Perform bounded work such as literature import or Readwise processing | Their explicitly delegated task |
| Scheduler or heartbeat | Invoke the durable CoS task on its configured cadence | Host-specific recurrence only |
| Episode recorder | Append privacy-minimized `cos-run/v1` receipts after operational episodes | Observation and provenance, not interpretation |
| Optional Codex trace adapter | Enrich receipts from structured harness events | Capture fidelity, not interpretation |
| Configured raw containers | Retain source evidence under per-container storage, search, and disclosure policy | Evidence, not asserted semantic knowledge |
| CoS evolution wiki | Accumulate generalized procedural lessons | Evidence-linked learning record |
| `evolve-chief-of-staff` skill | Maintain the wiki and propose evaluated changes | Development workflow, not runtime authority |
| User | Set policy, authorize restricted actions, and accept consequential behavior changes | Final authority |

## Two Wikis, Different Jobs

### Personal vault wiki

The vault contains specific information objects and their relationships:

- people and organizations;
- active and historical projects;
- meetings, decisions, and commitments;
- papers, books, annotations, and research synthesis;
- areas of focus, goals, and project context;
- explicit preferences and policies whose current values may change.

The vault is the durable semantic representation of the user's world. The Chief of Staff should retrieve from it through its published navigation and typed-relationship contracts.

### CoS evolution wiki

The evolution wiki contains generalizations about effective operation:

- how to assemble context for a meeting or project review;
- which kinds of changes deserve attention;
- how to distinguish urgency, importance, and mere novelty;
- which source should resolve a given kind of conflict;
- how to recognize stale, incomplete, or ambiguous evidence;
- when to draft, ask, defer, suppress, or route work;
- recurrent failure modes and successful recovery strategies;
- effects of prior skill changes.

It may cite trace identifiers as evidence. It must not copy the personal objects found in those traces.

The relationship is directional:

```text
CoS evolution wiki
    teaches how and where to retrieve
                │
                ▼
Personal vault wiki
    supplies the current specific context
```

These are not interchangeable stores. The evolution wiki is procedural and compact; the vault is semantic and richly specific.

## Classification Test

A candidate belongs in the evolution wiki when it remains useful after replacing every current person, project, paper, and deadline, and when it changes how the agent retrieves, decides, verifies, routes, or communicates.

A candidate belongs in the vault when it identifies a particular object or records a state of the user's world.

Examples:

| Candidate | Destination | Reason |
|---|---|---|
| “The proposal is due September 18.” | Vault or authoritative source | Specific mutable fact |
| “Verify consequential deadlines against the originating source.” | Evolution wiki | General verification strategy |
| “Alice leads Project X.” | Vault | Person-project relationship |
| “Meeting preparation should traverse project, people, recent meetings, and open commitments.” | Evolution wiki | Reusable retrieval procedure |
| “Project X reports are sent on Thursday.” | Project note | Project-specific operating fact |
| “Consult project-specific operating instructions before applying defaults.” | Evolution wiki | General routing rule |

Some concerns have both representations. A scheduling preference's current value belongs in the vault; the procedural rule to consult the scheduling profile belongs in the evolution wiki. This avoids duplicating changeable values in skill instructions.

## Operational Flow

The initial runtime flow is:

```text
Interactive request or heartbeat
        │
        ▼
Classify review mode and decision horizon
        │
        ▼
Select only the approved sources needed
        │
        ├── retrieve semantic context from the vault
        ├── retrieve current state from live systems
        └── inspect relevant specialist-task status
        │
        ▼
Reconcile freshness, provenance, and conflicts
        │
        ▼
Produce bounded attention items
        │
        ├── brief or draft
        ├── action request requiring approval
        └── quiet checkpoint when nothing changed
        │
        ▼
Append a normalized episode receipt when capture is configured
```

An attention item should answer:

- What changed or requires a decision?
- Why does it matter now?
- What evidence and freshness support it?
- What is the smallest useful next step?
- Is that next step informational, a draft, or a restricted mutation?

## Authority and Freshness

The skill uses different authorities for different questions:

- Explicit current user direction controls policy and intent.
- Live systems are authoritative for rapidly changing operational state within their domain.
- The vault is authoritative for curated context, relationships, decisions, and interpretation.
- The evolution wiki is authoritative only for learned procedural guidance.
- The deployed skill is the currently accepted executable procedure.
- Codex memory is an optional retrieval hint, never raw evidence or final authority.

When authorities conflict, the skill should expose the conflict and its timestamps rather than silently merge incompatible claims.

## Raw Evidence Boundary

Raw containers preserve source evidence before promotion. `raw` is an authority and lifecycle classification, not a promise that every item is local, ignored by Git, unsearchable, or confidential. A Readwise Markdown mirror, a manifest for externally stored papers, and an ignored CoS trajectory stream may all be raw while using different container policies.

Each deployment declares a container's origin, physical binding, versioning, update semantics, discovery, retention, privacy, disclosure, and promotion behavior. A retrieval-capable agent may be able to find content whose disclosure posture says not to introduce it outside a relevant context. That is an answer-scope rule; stronger confidentiality requires an enforced access boundary.

See [storage-model.md](storage-model.md) for the container policy contract.

## Mutation Boundary

The initial capability envelope is read-only retrieval and draft generation. The following require explicit approval at the time they are performed:

- sending or forwarding communications;
- creating, editing, or canceling calendar events;
- changing external tasks, shared documents, or automations;
- writing or promoting semantic memory;
- installing or activating recurring monitoring, or materially expanding an existing monitor's scope;
- adopting an evolved skill version for operational use.

An unattended run emits a stable action request instead of waiting on an interactive approval or assuming permission.

## Operational Skill and Evolution Skill

The operational skill receives the current accepted instructions and the information needed for its present task. It must not inspect the evolution wiki or modify itself during ordinary execution.

The evolution workflow receives normalized traces, outcome annotations, the evolution wiki, the current skill, and any available comparison evidence. It can update the wiki and propose a narrow skill patch, but adoption remains gated. Early evolution passes may be exploratory and human-reviewed; retained fixtures are added when real failures or stable cases justify them.

This separation prevents exploratory lessons, rejected ideas, and detailed optimization history from leaking into everyday reasoning.

## Portability Boundary

The portable package contains Agent Skills and future portable MCP declarations. Harness-specific behavior belongs behind adapters or reverse-domain client extensions.

For ChatGPT Codex, the minimum profile lets the operational task write a normalized receipt from its observable episode context. Structured task history through the App Server and lightweight lifecycle hooks can later enrich or verify those receipts. Direct parsing of native rollout files must remain behind a versioned adapter because it is not a stable portable contract.

The scheduler implementation is external to the portable procedure, but recurring operation is part of the product contract. A configured Codex deployment creates one thread heartbeat using the native automation surface. Another client's scheduler and an interactive request invoke the same operational contract.

The portable package does not reimplement a scheduler. A Codex installation follows the same minimal thread-heartbeat behavior as the existing `loop` skill through the native automation surface. Other harnesses may supply a different scheduler without changing Chief-of-Staff behavior.

See [storage-model.md](storage-model.md) for the source-versus-instance boundary used by each artifact.
