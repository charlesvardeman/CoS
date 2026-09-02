# Continual Learning for the Chief of Staff

## Adaptation Goal

This project adapts the [WikiSkill methodology](https://arxiv.org/html/2608.27454v1) to a long-lived personal Chief of Staff running in ChatGPT Codex and, eventually, other compatible harnesses.

The paper assumes benchmark-controlled tasks with homogeneous rollouts and immediate scoring. A personal Chief of Staff has different conditions:

- one conversational task may contain many distinct operational episodes;
- evidence arrives from private, heterogeneous systems;
- useful outcomes are often delayed and only partially observable;
- there is rarely a single ground-truth answer;
- semantic facts change independently of the skill;
- the harness compacts and summarizes conversations;
- authorization and privacy are part of correctness.

The adaptation preserves the paper's separation of raw experience, persistent learning, and executable skills while changing the episode model, trace ingestion, outcome labeling, privacy controls, and validation gate.

## Adapted Layers

### Raw layer

The raw layer stores append-only, temporally ordered evidence of individual CoS runs. It is not Codex memory and is not a copy of the entire surrounding conversation.

The canonical episode is one coherent CoS operation, such as a morning review, inbox triage, meeting preparation, project scan, or specialist-task follow-up. A long-lived Codex task may contain many episodes.

Raw traces remain machine-local by default and are excluded from Git. They should capture the minimum evidence needed to reconstruct observable behavior, with sensitive source content represented by stable identifiers, hashes, redacted excerpts, or protected snapshot references whenever possible.

### Wiki layer

The CoS evolution wiki accumulates procedural generalizations supported by trace evidence and user instruction. It records patterns, counterexamples, scope conditions, unresolved questions, and the effects of skill changes.

The wiki persists when a skill proposal is rejected or rolled back. Rejected changes are evidence about skill design; they do not invalidate the underlying observations.

### Skills layer

The skills layer contains concise operational instructions selected from the larger body of accumulated learning. Skill updates are reversible and versioned.

The inference agent receives the accepted skill but not the evolution wiki. The Maintainer and Proposer receive controlled access to traces and the wiki during a separate evolution workflow.

## Codex Trace Adapter

Codex memory is a delayed, selective consolidation layer. It may omit sessions and external-context work, and it lacks the ordered observations and actions needed for causal analysis. It can suggest a candidate pattern but cannot serve as WikiSkill's raw layer.

The preferred trace path is:

```text
Codex structured task history and item events
        │
        ├── lightweight hook notification
        └── versioned native-rollout fallback
        │
        ▼
Codex Trace Adapter
        │
        ▼
cos-run/v1 normalized episode
```

The [Codex App Server](https://learn.chatgpt.com/docs/app-server) is the preferred structured interface for task history and events. [Codex hooks](https://learn.chatgpt.com/docs/hooks) should only enqueue identifiers or notify an asynchronous normalizer; they should not perform heavy trace analysis. Native transcript or rollout files may be supported by a named parser version, but the adapter must contain the instability because their format is not a public portable interface.

Context compaction is recorded as a boundary in the event sequence. A generated compaction summary is not treated as a new episode or as equivalent to the original trace.

## Normalized Run Record

The first implementation artifact should be a `cos-run/v1` schema. At minimum, a record needs:

```yaml
schema: cos-run/v1
run_id: stable local identifier
thread_id: harness task identifier
turn_id: harness turn identifier
started_at: timestamp
invocation: interactive | heartbeat
mode: inbox-triage | daily-review | meeting-prep | project-scan | other
harness:
  name: codex
  version: recorded when available
model: recorded model identifier
skill_version: immutable version or commit
compaction_epoch: integer or boundary identifier
sources: []
observations: []
actions: []
attention_items: []
drafts: []
authorization_events: []
result: completed | partial | failed | no-change
native_provenance: []
privacy: {}
```

Each source observation should preserve identity, retrieval time, freshness, and a protected reference to the underlying evidence. Each tool action should record its action class, especially whether it was read-only, draft-only, approval-requesting, or mutating.

Hidden reasoning is not required. Explicit, user-visible rationale tags such as `deadline-within-48h`, `unanswered-request`, or `source-conflict` are more auditable and portable.

## Delayed Outcomes

A CoS response may only become evaluable hours or days later. Raw run records therefore remain immutable while outcome observations are appended separately:

```text
raw/runs/<run-id>.json
outcomes/<run-id>.jsonl
```

Possible outcomes include:

- accepted, dismissed, deferred, or corrected attention item;
- user-reported omission;
- draft used or substantially rewritten;
- action completed or abandoned;
- priority changed;
- later evidence showing that a source or inference was stale;
- explicit feedback about briefing length, timing, or framing.

Outcome annotations must identify whether they are explicit user judgments, observable downstream events, or Maintainer inferences.

## From Evidence to Generalization

There are two legitimate promotion paths:

1. **Declared policy:** the user explicitly gives a standing instruction intended to apply beyond the current instance.
2. **Induced lesson:** multiple materially independent outcomes support a scoped operational pattern.

An individual failure is normally recorded as evidence, not immediately converted into a universal rule. Before adding an induced lesson, the Maintainer should ask:

- Does the lesson survive substitution of the current people, projects, and documents?
- Does it change retrieval, verification, prioritization, routing, communication, or authorization behavior?
- Are there independent supporting cases or a strong explicit correction?
- Are there counterexamples or important scope conditions?
- Is the lesson already represented by a more general pattern?
- Would storing it duplicate a mutable fact available from the vault?

Every learned pattern should retain evidence identifiers and confidence or status. The wiki stores the generalization; the trace stores the instance.

## Maintainer and Proposer

The evolution workflow separates two jobs even if an early implementation performs them sequentially.

### Wiki Maintainer

The Maintainer reviews sampled traces and outcomes, reconciles them with existing patterns, records counterexamples, and updates the persistent wiki. It does not modify the operational skill.

### Skill Proposer

The Proposer reads the current skill, relevant wiki entries, selected evidence, prior proposals, and evaluation results. It proposes one coherent, reviewable change at a time and explains which evidence and wiki patterns it addresses.

Neither role may move specific personal facts into procedural memory. Neither role may use raw email, calendar, or document content beyond the protected local evaluation environment.

## Evaluation and Adoption

A candidate skill must be evaluated against frozen, redacted, or synthetic fixtures. It must not be tested by replaying mutating actions against live systems.

Evaluation should cover more than task completion:

- useful attention selection;
- false escalation and missed-item rates;
- source freshness and provenance;
- concision and decision readiness;
- quiet no-change behavior;
- compliance with approval and semantic-memory boundaries;
- performance across different projects and information objects;
- behavior across compaction and partial-source failures;
- portability across supported harnesses where applicable.

Adopt a proposal only when it improves the targeted behavior without material regression on retained fixtures. Record acceptance, rejection, or rollback in the evolution log and update the skill-impact record.

Initially, all proposals require human review. Automatic proposal generation does not imply automatic adoption.

## Codex Memory's Limited Role

[Codex memories](https://learn.chatgpt.com/docs/customization/memories) may eventually serve as low-confidence hints:

```text
Codex memory assertion
    → candidate question
    → locate supporting run evidence
    → confirm scope and counterexamples
    → evolution-wiki entry
    → possible evaluated skill proposal
```

Memory must never bypass evidence review and write directly to the wiki or skill. Stable requirements belong in project instructions or accepted skills; specific facts belong in the vault.

## Initial Non-Goals

- Autonomous online self-modification
- Capturing hidden chain-of-thought
- Committing raw personal traces to the plugin repository
- Replacing the vault with learned summaries
- Treating user engagement as the sole measure of quality
- Automatic semantic capture
- Automatic external mutation
- Assuming that a policy learned in Codex transfers unchanged to every harness
