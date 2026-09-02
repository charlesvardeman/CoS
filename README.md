# Chief of Staff

Chief of Staff is a design-stage Agent Plugin for maintaining a decision-ready view of personal work across a knowledge vault and approved connected sources. It is intended to notice what needs attention, retrieve the context needed to understand it, and produce concise briefs, drafts, and action requests.

The initial system is deliberately read-mostly. It does not treat installation as permission to send messages, modify calendars, update shared documents, create external automations, or write semantic memory.

> **Status:** pre-alpha design scaffold. No connector, scheduler, trace capture, or automatic evolution is active.

## What We Are Building

The project has three related skills:

- `chief-of-staff` performs bounded operational reviews such as inbox triage, periodic planning, meeting preparation, follow-up discovery, and cross-project coordination.
- `configure-chief-of-staff` discovers an existing environment, proposes source and attention policy, and produces a user-approved configuration without assuming a new vault or scheduler.
- `evolve-chief-of-staff` reviews normalized execution evidence, maintains a procedural evolution wiki, proposes narrow skill changes, and evaluates them before adoption.

The operational skill is the compiled behavior used during ordinary work. The evolution skill is a separate maintenance process and is not available to the operational agent during a run.

## Memory Model

The project keeps different kinds of memory separate:

| Layer | Contains | Does not contain |
|---|---|---|
| Personal vault | Specific people, projects, literature, decisions, commitments, and relationships | General CoS optimization history |
| Live systems | Current email, calendar, tasks, Zotero, Readwise, and other source state | Curated long-term interpretation |
| Raw CoS traces | Ordered, minimally sufficient evidence of runs and observable outcomes | Hidden reasoning or an unrestricted copy of private sources |
| CoS evolution wiki | Generalized workflows, decision strategies, failure patterns, and evidence-linked lessons | A duplicate inventory of people, projects, or messages |
| CoS skills | Concise, validated procedures compiled from accepted lessons | Raw traces or mutable personal facts |
| CoS configuration and runtime state | Source bindings, scopes, cadence, watermarks, pending actions, and active-host state | Portable procedure |
| Codex memory | Optional cross-task hints and summaries | Raw evidence or semantic authority |

The governing distinction is:

> The vault records what is true in the user's world. The CoS evolution wiki records how the Chief of Staff should operate in that world.

The evolution wiki teaches the skill how to locate and interpret specific information in the vault; it does not absorb that information.

## Package Boundary

This repository owns the portable CoS behavior and its evolution method. It may eventually include a Codex client extension for trace notification and normalization, but the portable core must remain usable without it.

The separate vault project **Chief-of-Staff Operating System** owns deployment concerns: source scopes, scheduler cadence, quiet hours, briefs and handoffs, Mac Studio operation, Android review, laptop takeover, and activation gates. Creating this package does not activate that operating system.

## Repository Map

```text
.
├── plugin.json
├── skills/
│   ├── chief-of-staff/SKILL.md
│   ├── configure-chief-of-staff/SKILL.md
│   └── evolve-chief-of-staff/SKILL.md
├── docs/
│   ├── architecture.md
│   ├── storage-model.md
│   └── continual-learning.md
├── wiki/
│   ├── index.md
│   ├── evolution-log.md
│   └── skill-impact.md
└── PLAN.md
```

Machine-local raw traces and delayed outcome records are intentionally ignored by Git.

## Design Principles

1. Retrieve specifics; do not compile them into procedural instructions.
2. Verify mutable facts against an authoritative live source when consequences justify it.
3. Surface decisions and changed conditions, not an exhaustive recap of available information.
4. Keep no-change runs quiet.
5. Separate observation, drafting, authorization, and mutation.
6. Separate operational inference from skill evolution.
7. Generalize only with explicit standing instructions or evidence from sufficiently independent outcomes.
8. Preserve provenance and reversibility for every proposed skill change.

## Documentation

- [Architecture](docs/architecture.md) defines responsibilities, authority, retrieval, and the two-wiki boundary.
- [Storage model](docs/storage-model.md) defines what belongs in a skill, elsewhere in the package, or outside the package entirely.
- [Continual learning](docs/continual-learning.md) adapts the WikiSkill methodology to ChatGPT Codex traces and personal workflows.
- [Plan](PLAN.md) defines the phased build and acceptance gates.
- [Evolution wiki](wiki/index.md) starts the procedural knowledge record with the design decisions accepted in the originating dialogue.

## Methodological Sources

- [Agent Plugins](https://agent-plugins.org/) supplies the portable package structure.
- [WikiSkill](https://arxiv.org/html/2608.27454v1) supplies the separation of immutable experience, persistent learning, and evolving skills, adapted here for personal workflows rather than benchmark tasks.
- [Codex App Server](https://learn.chatgpt.com/docs/app-server), [hooks](https://learn.chatgpt.com/docs/hooks), and [memories](https://learn.chatgpt.com/docs/customization/memories) describe the relevant Codex integration surfaces and their boundaries.
