---
schema: cos-skill-proposal/v1
proposal_id: COS-SP001
target_skill: chief-of-staff 0.2.0
patterns:
  - COS-P011
change_summary: Add one conditional project-participant reconciliation procedure for operational outputs whose correctness depends on participant identity, role, authority, or immediate responsibility.
expected_effect: Fewer incorrectly framed drafts and follow-ups caused by treating incomplete vault rosters or live attendee lists as complete role evidence; more bounded, reviewable proposals for closing semantic gaps.
regression_risks:
  - Excess retrieval latency when participant identity cannot affect the result.
  - Noisy semantic-capture proposals for harmless roster incompleteness.
  - Accidental inference of durable roles from current participation if the source boundary is weakened.
comparison_evidence: []
status: accepted
human_decision: Explicit user approval on 2026-09-02T21:57:28Z
---

# Proposal: Project Participant and Role Reconciliation

## Proposed Change

Add a conditional reference to the operational skill. Load it only when an output depends on who participates in a project, what role or authority they hold, or who owns the immediate next action.

The proposed reference implements the loop in [COS-P011](../patterns/COS-P011-project-participant-role-reconciliation.md) while retaining the existing read-mostly and reviewed-semantic-capture boundaries.

## Evaluation Plan

Treat initial evaluation as exploratory. Do not reuse the episode that induced this proposal as comparison evidence. Assess the candidate on later independent project-centered meeting preparations, drafts, and follow-up decisions using these measures:

- correct distinction between current participation and durable role;
- correct recipient and responsibility framing;
- absence of unsupported authority claims;
- useful, bounded capture proposals when the vault is materially incomplete;
- no generic roster-completeness noise during heartbeats;
- no semantic write without explicit approval.

The concrete candidate patch is stored separately in [COS-SP001.patch](COS-SP001.patch).

## Adoption Decision

Chuck explicitly approved adopting this proposal on 2026-09-02. The procedure was incorporated into Chief of Staff `0.2.1`. Evaluation remains exploratory until later independent project-centered episodes exercise the behavior.
