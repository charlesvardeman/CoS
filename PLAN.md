# Chief of Staff Plugin — Build Plan

## Objective

Build a portable, read-mostly Chief-of-Staff Agent Plugin that can retrieve specific context from the user's vault and approved live systems, produce decision-ready attention briefs and drafts, and improve through a governed WikiSkill-inspired process without turning its procedural memory into a duplicate personal knowledge base.

## Definition of Done

The first complete release should:

1. Package valid operational, configuration, and evolution Agent Skills under an Agent Plugins 1.0 manifest.
2. Run one durable Chief-of-Staff task interactively and through a native heartbeat using approved read-only sources.
3. Produce useful attention items with provenance and freshness.
4. Stay quiet when a periodic review finds no meaningful change.
5. Require explicit approval for external mutation and semantic-memory writes.
6. Normalize Codex executions into privacy-minimized, append-only run records.
7. Maintain a procedural evolution wiki without storing specific personal information objects.
8. Propose and assess reversible skill changes against independent real episodes or retained fixtures.
9. Keep the portable behavior separable from Codex-specific scheduling and trace capture implementations.

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
- [x] Define `raw` as an evidence authority class with per-container storage, versioning, discovery, retention, disclosure, and promotion policy.
- [ ] Decide the deployed `raw/trajectories` binding, backup, retention, redaction, and Git policy during first configuration.

**Gate P0:** the user accepts the responsibility model, initial workflows, output contracts, and trace policy contract. No live connector or recurring monitor is active merely because the source package exists.

## Phase 1 — Operational Skill MVP

**Goal:** establish the minimum real Chief-of-Staff loop: durable task, read-mostly operational judgment, native heartbeat, observable episode receipts, and quiet no-change behavior.

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
- [x] Define task-authored `cos-run/v1` receipts as the minimum capture profile.
- [x] Define the Codex installation wrapper and first-run sequence.
- [x] Make one native thread heartbeat part of the default configured deployment.
- [ ] Bind the durable task, approved sources, trajectory containers, and heartbeat in the first deployed configuration.
- [ ] Complete one real heartbeat episode and verify that its receipt reconstructs the observable behavior.
- [ ] Verify that the skill never writes semantic memory or mutates an external source without explicit authorization.

**Gate P1:** one durable task produces useful interactive and heartbeat results, quiet no-change runs, and usable episode receipts with no unauthorized mutation or semantic capture.

## Phase 2 — Codex Trace Adapter

**Goal:** improve capture completeness and failure recovery without coupling the portable skill to Codex internals.

- [x] Define the minimum `cos-run/v1` normalized schema and task-authored capture profile.
- [ ] Define and test how dedicated and mixed-purpose Codex tasks are identified and divided into CoS episodes.
- [x] Define the append-only delayed-outcome relationship.
- [ ] Prototype extraction from structured Codex task history and item events.
- [ ] Add a lightweight notification hook only if required for dependable ingestion.
- [ ] Isolate any native rollout parser behind an explicit adapter version.
- [ ] Preserve temporal order, turn boundaries, compaction markers, source provenance, skill version, and authorization events.
- [ ] Redact or replace sensitive source content before persistence.
- [ ] Verify several long-task episodes, including compaction, failure, no-change, and delayed feedback.

**Gate P2:** host-enriched records improve on the minimum receipts and reliably reconstruct interrupted, compacted, failed, and long-running CoS behavior without depending on Codex memory summaries or exposing unnecessary private content.

## Phase 3 — Evolution Wiki Maintainer

**Goal:** turn evidence into durable procedural knowledge while preserving the semantic boundary.

- [ ] Define pattern, counterexample, open-question, and evidence-reference formats.
- [ ] Implement declared-policy and induced-lesson promotion paths.
- [ ] Require scope conditions and counterexample checks for induced lessons.
- [ ] Prevent person-, project-, message-, and document-specific facts from entering the wiki.
- [ ] Maintain an append-only evolution log and a skill-impact record.
- [ ] Run the Maintainer on selected successful, failed, and ambiguous real episodes.
- [ ] Review all initial wiki changes manually and confirm that the operational task cannot read them.

**Gate P3:** the Maintainer produces useful generalizations with trace provenance and no semantic-memory leakage.

## Phase 4 — Skill Proposal, Evaluation, and Rollback

**Goal:** convert selected wiki lessons into reviewable improvements and learn from their effect in later episodes.

- [ ] Define the candidate-patch format and one-coherent-change rule.
- [ ] Assess the first candidate against subsequent independent real episodes.
- [ ] Retain redacted or synthetic fixtures when recurring cases justify a reusable comparison set.
- [ ] Evaluate usefulness, omissions, false escalation, concision, provenance, quiet behavior, and safety boundaries using the best independent evidence available.
- [ ] Record accepted, rejected, and rolled-back proposals.
- [ ] Preserve the wiki when a skill change is rejected.
- [ ] Require explicit human approval before adopting candidate skill versions.
- [ ] Test the accepted skill with more than one supported model or harness when portability becomes relevant.

**Gate P4:** at least one evidence-linked skill improvement receives human approval, affects a later real episode as intended, and can be rolled back cleanly. Record the result as exploratory unless representative retained comparisons also support it.

## Phase 5 — Specialist Coordination and Operational Hardening

**Goal:** expand the established heartbeat safely across specialist workflows and operating environments.

- [ ] Refine cadence, quiet hours, lookback windows, and no-change behavior from real use.
- [ ] Invoke bounded specialist workflows for Zotero, Readwise, inbox ingestion, or project monitoring rather than duplicating their procedures.
- [ ] Define stable status and handoff contracts for specialist tasks monitored by the Chief of Staff.
- [ ] Ensure there is one active scheduler and no duplicate source scans.
- [ ] Review cross-source and specialist behavior for duplicate work, latency, and policy compliance.

**Gate P5:** the active monitor coordinates specialist work without duplicate scheduling, unauthorized mutation, or automatic semantic capture.

## Phase 6 — Portability and Distribution

**Goal:** preserve the portable core while supporting harness-specific advantages.

- [ ] Revalidate both manifests and all three Agent Skills before each distributed release.
- [ ] Document the capability contract expected from a host client.
- [ ] Keep Codex-only files in a reverse-domain client extension or separate adapter package.
- [ ] Build at least one non-Codex fixture runner before claiming cross-harness portability.
- [ ] Decide immutable release pinning and any shared marketplace distribution.

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

- Initial CoS trajectory-container location, Git treatment, backup, retention, redaction, search, and disclosure settings.
- Reliable signals for identifying dedicated CoS tasks and bounded CoS episodes in mixed-purpose tasks.
- Whether the initial Maintainer runs only on explicit request or on a low-frequency review cadence.
- The minimum evidence required before an induced lesson becomes confirmed.
- Which output and outcome measures matter enough to move proposals from exploratory to confirmed.
