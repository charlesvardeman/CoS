# Evolution Records

This reference defines portable record contracts. Actual traces, outcome records, and the evolving personal wiki remain outside installed skill directories.

## Pattern Record

```yaml
schema: cos-pattern/v1
pattern_id: stable identifier
title: concise generalization
status: provisional | confirmed | superseded
origin: declared-policy | induced-lesson
scope: contexts where the pattern applies
guidance: procedural implication
evidence: []
counterexamples: []
confidence: low | medium | high
created_at: timestamp
updated_at: timestamp
```

Evidence entries point to protected run or outcome identifiers. Do not copy private source content into the record.

## Skill Proposal

```yaml
schema: cos-skill-proposal/v1
proposal_id: stable identifier
target_skill: skill name and version
patterns: []
change_summary: one coherent behavioral change
expected_effect: observable improvement
regression_risks: []
fixture_set: immutable identifier
status: proposed | accepted | rejected | rolled-back
human_decision: null or decision reference
```

Keep the proposed patch separately so it can be inspected and reverted.

## Evaluation Record

An evaluation identifies the candidate and baseline skill versions, fixture-set version, harness and model, observable measures, failures, safety results, and decision. Preserve qualitative examples through protected fixture identifiers rather than personal source excerpts.

Evaluation evidence must distinguish the runs used to induce a lesson from retained runs used to test the proposed change. When a representative validation split is not yet available, label the result exploratory rather than treating it as proof of improvement.

## Wiki Persistence

Rejected and rolled-back proposals remain in the evolution log. Update pattern confidence or scope only when the evidence warrants it; do not delete a supported lesson merely because one implementation of it failed.
