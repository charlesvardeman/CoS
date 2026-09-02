# CoS Project Instructions

This repository develops a portable Chief-of-Staff Agent Plugin and its governed continual-learning method.

## Read First

Before changing behavior, read:

1. `README.md`
2. `docs/architecture.md`
3. `docs/storage-model.md`
4. `docs/continual-learning.md`
5. `PLAN.md`

## Authority Boundaries

- Use the Agent Plugins 1.0 structure as the portable packaging authority: root `plugin.json`, immediate skill children under `skills/`, and reverse-domain directories for client-specific extensions.
- Keep Codex hooks, task-history adapters, scheduler wiring, credentials, and host paths out of the portable skill core.
- Treat the user's vault as semantic authority for people, projects, literature, decisions, and other specific information objects.
- Treat the CoS evolution wiki as procedural memory: generalized workflows, decision strategies, failure patterns, and evidence-linked lessons.
- Do not copy personal facts from the vault or raw source content into the evolution wiki.
- Do not treat Codex memory summaries as raw execution traces or authoritative evidence.
- Keep user-specific configuration, scheduler state, watermarks, pending actions, traces, and outcomes outside installed skill directories. Skills may define their contracts, not store their instances.

## Safety and Scope

- Default to read-only retrieval and draft generation.
- Sending messages, changing calendars, modifying shared documents, changing external automations, and writing semantic memory require explicit user authorization at the time of action.
- Operational runs must not read or edit the evolution wiki. Evolution is a separate workflow.
- Raw artifacts are evidence, not asserted semantic knowledge. Their physical location, Git treatment, indexing, retention, and disclosure posture are declared per container; a `raw/` path does not itself provide confidentiality.
- CoS trajectory containers may contain private information. Minimize captured content and follow the configured container policy. Never commit traces to this portable plugin repository.
- Do not install or activate a recurring monitor merely because plugin or skill code exists.

## Development Practice

- Keep `SKILL.md` entry points concise. Put conditional detail in focused references only when implementation requires it.
- Preserve observable provenance, source freshness, and authorization boundaries in fixtures and evaluations.
- Validate each skill with the bundled Codex `skill-creator` validator after substantive changes.
- Prefer narrow, reversible changes supported by explicit instructions or multiple independent outcomes.
