# Chief of Staff Plugin — Build Plan

## Objective

Build a portable, read-mostly Chief-of-Staff Agent Plugin that can retrieve specific context from the user's vault and approved live systems, produce decision-ready attention briefs and drafts, and improve through a governed WikiSkill-inspired process without turning its procedural memory into a duplicate personal knowledge base.

## Definition of Done

The first complete release should:

1. Package valid operational, configuration, and evolution Agent Skills under an Agent Plugins 1.0 manifest.
2. Run at least three bounded workflows interactively using approved read-only sources.
3. Produce useful attention items with provenance and freshness.
4. Stay quiet when a periodic review finds no meaningful change.
5. Require explicit approval for external mutation and semantic-memory writes.
6. Normalize Codex executions into privacy-minimized, append-only run records.
7. Maintain a procedural evolution wiki without storing specific personal information objects.
8. Propose and evaluate reversible skill changes against retained fixtures.
9. Remain separable from Codex-specific scheduling and trace capture.

## Phase 0 — Contract and Design Scaffold

**Goal:** make the system boundary reviewable before implementing connectors or automation.

- [x] Establish the Agent Plugins 1.0 package root and manifest.
- [x] Draft the operational and evolution skill entry points.
- [x] Add a configuration skill that recognizes established environments and keeps configured values outside the package.
- [x] Define the semantic-vault versus procedural-wiki boundary.
- [x] Define the skill, package-documentation, configuration, runtime-state, trace, and vault storage boundaries.
- [x] Document the Codex-specific continual-learning adaptation.
- [x] Seed the evolution wiki with accepted design principles.
- [x] Reconcile ownership with the vault's Chief-of-Staff Operating System project: this repository owns the portable capability; the vault project owns deployment and operations.
- [x] Select the first three provisional workflows: inbox triage, periodic attention review, and meeting preparation.
- [x] Define first-pass attention-item, draft, action-request, and no-change contracts.
- [ ] Decide the local retention and redaction policy for raw traces.

**Gate P0:** the user accepts the responsibility model, initial workflows, output contracts, and trace privacy policy. No live connector or recurring monitor is active.

## Phase 1 — Operational Skill MVP

**Goal:** prove the skill interactively with read-only retrieval and draft output.

Initial workflows:

- inbox triage across approved inbound channels;
- daily or weekly attention review using work calendar, task list, work Gmail, and project notes;
- meeting preparation using the relevant project, people, prior meetings, and open commitments.

Work:

- [x] Define a first-pass source and configuration capability contract independent of connector implementation.
- [x] Specify first-pass source authority, freshness, failure, and conflict behavior.
- [ ] Implement vault navigation through existing retrieval capabilities rather than embedding personal paths or note inventories.
- [x] Define attention selection as explainable factors, not a hidden universal number.
- [x] Specify concise brief, draft, no-change, and approval-request outputs.
- [ ] Create redacted or synthetic fixtures for useful change, no change, stale source, source conflict, and partial source failure.
- [ ] Verify that the skill never writes semantic memory or mutates an external source without explicit authorization.

**Gate P1:** the three workflows produce reviewable results on fixtures and manual read-only runs, with no unauthorized mutation or semantic capture.

## Phase 2 — Codex Trace Adapter

**Goal:** create reliable evidence for learning without coupling the portable skill to Codex internals.

- [ ] Define and validate the `cos-run/v1` normalized schema.
- [ ] Define the append-only delayed-outcome schema.
- [ ] Prototype extraction from structured Codex task history and item events.
- [ ] Add a lightweight notification hook only if required for dependable ingestion.
- [ ] Isolate any native rollout parser behind an explicit adapter version.
- [ ] Preserve temporal order, turn boundaries, compaction markers, source provenance, skill version, and authorization events.
- [ ] Redact or replace sensitive source content before persistence.
- [ ] Verify several long-task episodes, including compaction, failure, no-change, and delayed feedback.

**Gate P2:** normalized records can reconstruct observable CoS behavior without depending on Codex memory summaries or exposing unnecessary private content.

## Phase 3 — Evolution Wiki Maintainer

**Goal:** turn evidence into durable procedural knowledge while preserving the semantic boundary.

- [ ] Define pattern, counterexample, open-question, and evidence-reference formats.
- [ ] Implement declared-policy and induced-lesson promotion paths.
- [ ] Require scope conditions and counterexample checks for induced lessons.
- [ ] Prevent person-, project-, message-, and document-specific facts from entering the wiki.
- [ ] Maintain an append-only evolution log and a skill-impact record.
- [ ] Test the Maintainer on a curated batch of successful, failed, and ambiguous runs.
- [ ] Review all initial wiki changes manually.

**Gate P3:** the Maintainer produces useful generalizations with trace provenance and no semantic-memory leakage.

## Phase 4 — Skill Proposal, Evaluation, and Rollback

**Goal:** convert selected wiki lessons into demonstrably better operational behavior.

- [ ] Define the candidate-patch format and one-coherent-change rule.
- [ ] Build a retained validation set distinct from the evidence used to propose a change.
- [ ] Evaluate usefulness, omissions, false escalation, concision, provenance, quiet behavior, and safety boundaries.
- [ ] Record accepted, rejected, and rolled-back proposals.
- [ ] Preserve the wiki when a skill change is rejected.
- [ ] Require explicit human approval before adopting candidate skill versions.
- [ ] Test the accepted skill with more than one supported model or harness when portability becomes relevant.

**Gate P4:** at least one evidence-linked skill improvement passes retained fixtures, receives human approval, and can be rolled back cleanly.

## Phase 5 — Heartbeat and Specialist Coordination

**Goal:** connect the proven operational skill to one conservative scheduler without embedding scheduling into the portable package.

- [ ] Define cadence, quiet hours, lookback windows, and no-change notification behavior in the operating-system project.
- [ ] Invoke bounded specialist workflows for Zotero, Readwise, inbox ingestion, or project monitoring rather than duplicating their procedures.
- [ ] Define stable status and handoff contracts for specialist tasks monitored by the Chief of Staff.
- [ ] Ensure there is one active scheduler and no duplicate source scans.
- [ ] Run manually, then in dry-run recurrence, before activation.
- [ ] Review the first three live runs for usefulness and policy compliance.

**Gate P5:** one active monitor produces useful change notifications or quiet checkpoints without duplicate scheduling, unauthorized mutation, or automatic semantic capture.

## Phase 6 — Portability and Distribution

**Goal:** preserve the portable core while supporting harness-specific advantages.

- [ ] Validate `plugin.json` and all three Agent Skills against their specifications.
- [ ] Document the capability contract expected from a host client.
- [ ] Keep Codex-only files in a reverse-domain client extension or separate adapter package.
- [ ] Build at least one non-Codex fixture runner before claiming cross-harness portability.
- [ ] Decide private installation and immutable pinning through the separate marketplace project.

**Gate P6:** the same operational skill and fixtures can run through a second compatible harness without importing Codex trace semantics into the portable core.

## Cross-Cutting Evaluation Dimensions

| Dimension | Required evidence |
|---|---|
| Usefulness | Surfaced item supports a real decision or next step |
| Selectivity | Unchanged and low-value material is suppressed |
| Recall | Important fixture items are not missed |
| Freshness | Mutable claims identify retrieval time and source |
| Provenance | Attention items can be traced to protected evidence |
| Safety | Restricted actions remain drafts or action requests until approved |
| Memory discipline | Specific information remains in the vault or source system |
| Learnability | Outcomes can be joined to the run that produced them |
| Reversibility | Skill versions and accepted changes can be rolled back |
| Portability | Core procedure does not depend on one harness's transcript format |

## Decisions Still Needed

These are intentional design decisions, not prerequisites for beginning fixture work:

- Raw-trace retention duration and protected storage location.
- Whether the initial Maintainer runs only on explicit request or on a low-frequency review cadence.
- The minimum evidence required before an induced lesson becomes confirmed.
- Which output and outcome measures matter enough to gate skill adoption.
