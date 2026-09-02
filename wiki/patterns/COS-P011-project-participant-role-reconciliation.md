---
schema: cos-pattern/v1
pattern_id: COS-P011
title: Reconcile project participation and role at the point of use
status: confirmed
origin: declared-policy
scope: Project-centered triage, meeting preparation, drafting, follow-up routing, and any operational inference that depends on who is involved or what authority they hold.
guidance: Retrieve the project's durable participant context from the semantic vault, compare it with current event- and message-level evidence, keep participation distinct from durable role or authority, and route material gaps through reviewed semantic capture instead of guessing or silently writing memory.
evidence:
  - cos-run-20260902T202352Z-manual-001
  - cos-outcome-20260902T205323Z-002
  - cos-outcome-20260902T205643Z-003
  - cos-outcome-20260902T210921Z-005
counterexamples: []
confidence: high
created_at: 2026-09-02T21:05:45Z
updated_at: 2026-09-02T21:05:45Z
---

# Reconcile Project Participation and Role at the Point of Use

## Problem

A project record may omit a participant, identify a participant without a role, or retain a relationship whose authority or current status has changed. Live email and calendar evidence can reveal current participation, but appearance in a recipient list or meeting roster does not establish a durable project role. Treating either source as complete can produce incorrect routing, framing, or follow-up advice.

## Memory Boundary

- The personal vault stores specific people, projects, participant relationships, role assertions, provenance, and current status.
- Live systems establish current message recipients, meeting attendees, task assignees, and other event-level participation within their source domain.
- This wiki stores only the reusable reconciliation procedure.
- The operational skill must not copy a current roster into procedural memory.

## Reconciliation Loop

1. **Trigger on consequence.** Run the loop when a draft, recommendation, meeting brief, delegation, or follow-up depends on who is involved or what authority a person has. Do not launch a generic completeness audit during every heartbeat.
2. **Retrieve durable context.** Read the project note and traverse its typed person relationships. Retrieve only the person notes needed to understand the active decision.
3. **Retrieve current participation.** Inspect the authoritative live artifacts relevant to the episode, such as message headers, calendar attendee lists, task ownership, or the originating request.
4. **Separate claim types.** Keep these claims distinct:
   - event participation: present on this message, meeting, or task;
   - durable project involvement: associated with the project across episodes;
   - role or authority: lead, sponsor, point of contact, reviewer, contributor, or another responsibility;
   - current responsibility: owns the immediate decision or next action.
5. **Classify the comparison.** Mark the evidence as consistent, missing-participant, missing-role, possibly-stale, conflicting, or ambiguous. Preserve source identity and observation time for mutable claims.
6. **Operate conservatively.** Use live sources for current event membership and the vault for curated durable context. Never infer durable role or decision authority merely from attendance, authorship, a carbon copy, or a single task assignment. If the distinction materially changes the output, verify it or use neutral language.
7. **Propose semantic closure.** When the episode exposes a reusable missing or stale fact, emit a bounded semantic-capture proposal containing the project, person, claimed relationship or role, evidence locator, observation time, confidence, and proposed change. Do not write it automatically.
8. **Route reviewed capture.** After explicit approval, use the vault's authoritative capture pathway to update the project/person representation and preserve provenance. A later operational episode retrieves the reviewed result normally.
9. **Learn from corrections.** Link user corrections and downstream outcomes to the originating run. Repeated or explicitly generalized procedural lessons return to this evolution workflow; specific roster facts return to the vault.

## Attention Policy

During a heartbeat, surface a participant-role gap only when it affects an imminent meeting, message, commitment, delegation, or decision. Otherwise retain it as a bounded capture candidate for the next relevant project review. The objective is use-on-contact improvement, not a noisy demand to complete every project roster at once.

## Required Vault Capability

The vault needs a governed representation that can distinguish project membership from role and authority while preserving provenance and freshness. Until that representation is accepted through ontology governance, the Chief of Staff should continue using the existing project-to-person relationship for known collaboration, avoid overloading it with inferred roles, and route role-bearing assertions as proposals rather than inventing new fields.

## Open Questions

- Should role-bearing project participation be represented by a reified participation record or by a small set of role-specific project-to-person edges?
- Which roles need controlled vocabulary, and which should remain project-local labels?
- What evidence and review threshold should retire a stale role assertion?
