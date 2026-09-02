# Storage Model

## Purpose

The Chief of Staff needs stable instructions, conditional operating guidance, user-specific configuration, semantic knowledge, runtime state, raw evidence, and accumulated lessons. Placing all of these in `SKILL.md` would make the skill stale, private, difficult to transfer, and impossible to evolve safely.

This model distinguishes both **what an artifact means** and **when an agent may load it**.

## Storage Classes

| Artifact | Location | Loaded by | Examples |
|---|---|---|---|
| Skill entry point | `skills/<name>/SKILL.md` | The matching skill invocation | Stable purpose, routing, invariants, authorization boundaries |
| Skill-local reference | `skills/<name>/references/` | Only the matching mode that needs it | Attention policy, output contracts, recurring-check rules, record schemas |
| Package documentation | `docs/` and root files | Developers and reviewers | Architecture, rationale, build plan, packaging decisions |
| Development evolution wiki | repository-root `wiki/` | Evolution workflow only | Generalized patterns, proposal history, skill impact |
| Personal semantic knowledge | User's vault | Operational retrieval and approved capture workflows | People, projects, literature, decisions, commitments |
| User configuration | External governed configuration chosen during setup | Operational skill and scheduler | Source bindings, account choices, scopes, quiet hours, thresholds |
| Operational state | External host or shared control record | Scheduler and operational skill | Watermarks, last successful check, pending action IDs, active host |
| Raw runs and outcomes | Protected external trace store | Trace adapter and evolution workflow | Ordered run evidence and delayed feedback |
| Live source state | Connected systems | Authorized connector or specialist | Email, calendar, tasks, Zotero, Readwise |
| Codex memory | Codex-managed memory surface | Harness retrieval when available | Selective cross-task hints |

## What Belongs in `SKILL.md`

Place guidance in the entry point when it is:

- needed in nearly every invocation of that skill;
- stable across users, projects, and source systems;
- necessary to route to an optional reference;
- a non-negotiable safety, authority, or memory boundary;
- concise enough that loading it routinely improves rather than dilutes behavior.

Examples include the read-mostly default, the instruction to retrieve current specifics instead of embedding them, the separation of briefs from restricted action requests, and the prohibition on self-modification during an operational run.

Do not place current project lists, names, account identifiers, schedules, vault paths, attention thresholds, source watermarks, or learned trace instances in `SKILL.md`.

## What Belongs in Skill References

Place a procedure or contract in a skill-local reference when it is portable but only conditionally relevant. A scheduled review needs recurring-check behavior; an interactive meeting-preparation request does not need heartbeat setup guidance. Both may need the same source-authority and output contracts.

References define reusable shapes and decision criteria. They do not contain the user's configured values or current world state.

## What Belongs Outside Skills

User-specific configuration and mutable operational state must survive skill replacement without modifying the installed package. The configuration workflow may propose or validate these artifacts, but the deployed values live in a host configuration surface, private operational repository, or vault note explicitly selected by the user.

The package defines contracts such as `cos-config/v1`, `attention-item/v1`, and `cos-run/v1`. Instances of those contracts remain outside the skill directories.

This prevents:

- package updates from overwriting personal state;
- portable releases from containing private identifiers;
- source changes from requiring edits to procedural instructions;
- runtime checkpoints from appearing as skill evolution;
- operational inference from seeing rejected or experimental lessons.

## Status of the Repository-Root Wiki

The current `wiki/` directory is deliberately outside `skills/`. It is the development evolution wiki for this source repository and records only generalized procedural knowledge.

For the first personal implementation it may serve as the governed evolution authority because this repository is private. Before producing a reusable installation artifact, decide whether to:

1. ship only a read-only base wiki and keep the user's evolving wiki in external state; or
2. omit the wiki from the installation artifact and point the evolution skill to a separately versioned private wiki.

Either choice must preserve the invariant that the operational skill cannot read the evolution wiki and that skill rollback does not erase accumulated learning.

## Promotion Paths

Information moves between stores only through explicit transformations:

```text
Live source observation
    → operational attention item or draft
    → optional reviewed semantic-capture proposal
    → vault

Normalized run plus later outcome
    → Maintainer generalization
    → evolution wiki
    → evaluated skill proposal
    → accepted skill version
```

The first path preserves specific meaning in the semantic vault. The second compiles experience into general procedure. They must not be collapsed into one automatic memory write.

## First-Pass Rule

When placement is uncertain, keep the value outside the skill and put only the retrieval or validation instruction inside. It is easier to promote a stable, well-supported pattern later than to remove private or stale state from deployed procedural instructions.
