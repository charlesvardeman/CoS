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

The adaptation preserves the paper's separation of raw experience, persistent learning, and executable skills while changing the episode model, trace ingestion, outcome labeling, privacy controls, and adoption gate. The minimum viable system learns between real episodes; it does not wait for a software-style test harness or modify itself inside an active run.

## Adapted Layers

### Raw layer

The raw layer is the evidence substrate shared by heterogeneous source containers. For continual learning, a configured CoS trajectory container stores append-only, temporally ordered evidence of individual CoS runs. It is not Codex memory and is not a copy of the entire surrounding conversation.

The canonical episode is one coherent CoS operation, such as a morning review, inbox triage, meeting preparation, project scan, or specialist-task follow-up. A long-lived Codex task may contain many episodes.

The trajectory container should capture the minimum evidence needed to reconstruct observable behavior, with sensitive source content represented by stable identifiers, hashes, redacted excerpts, or protected snapshot references whenever possible. Its physical location, Git treatment, backup, indexing, retention, and disclosure posture come from its `raw-container-policy/v1` binding. The likely first personal policy is machine-local and Git-ignored, but that is not inherited by other raw containers such as Readwise or papers.

The first usable capture profile is an agent-authored episode receipt. At the end of an operational invocation, the Chief-of-Staff task appends the ordered observations, actions, material results, approval events, and output classifications available in its current context. The receipt declares its capture method and limitations. It is less complete than a native harness trace but sufficient to begin evidence-grounded learning when the Maintainer can reconstruct the relevant behavior from it.

### Wiki layer

The CoS evolution wiki accumulates procedural generalizations supported by trace evidence and user instruction. It records patterns, counterexamples, scope conditions, unresolved questions, and the effects of skill changes.

The wiki persists when a skill proposal is rejected or rolled back. Rejected changes are evidence about skill design; they do not invalidate the underlying observations.

### Skills layer

The skills layer contains concise operational instructions selected from the larger body of accumulated learning. Skill updates are reversible and versioned.

The inference agent receives the accepted skill but not the evolution wiki. The Maintainer and Proposer receive controlled access to traces and the wiki during a separate evolution workflow.

## Minimum Capture and Codex Trace Adapter

Codex memory is a delayed, selective consolidation layer. It may omit sessions and external-context work, and it lacks the ordered observations and actions needed for causal analysis. It can suggest a candidate pattern but cannot serve as WikiSkill's raw layer.

The installation-ready trace path is:

```text
Operational CoS episode
        │
        ▼
Task-authored observable receipt
        │
        ▼
cos-run/v1 in the configured trajectory container
```

This path avoids making a native exporter a prerequisite for using the Chief of Staff. It must not be described as a complete transcript, and capture failure must remain visible.

The later higher-fidelity path is:

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

The [Codex App Server](https://learn.chatgpt.com/docs/app-server) is the preferred future structured interface for task history and events. [Codex hooks](https://learn.chatgpt.com/docs/hooks) should only enqueue identifiers or notify an asynchronous normalizer; they should not perform heavy trace analysis. Native transcript or rollout files may be supported by a named parser version, but the adapter must contain the instability because their format is not a public portable interface.

Context compaction is recorded as a boundary in the event sequence. A generated compaction summary is not treated as a new episode or as equivalent to the original trace.

## Identifying Chief-of-Staff Tasks and Episodes

A Codex task is a conversation envelope, not necessarily one CoS run. A dedicated Chief-of-Staff task may contain many CoS episodes, while a mixed-purpose task may contain one bounded CoS episode among unrelated work. The trace adapter therefore needs both task-level classification and episode-level boundaries.

Once classified, normalized episodes in the trajectory container become the raw evidence for understanding how Chief-of-Staff tasks actually operate and for later procedural learning. Raw history supports that analysis, but the mere presence of task events in raw storage does not by itself establish that they are CoS episodes.

Prefer explicit, durable signals over title matching or content inference:

1. an explicit Chief-of-Staff skill invocation or router event;
2. a configured scheduler or automation binding;
3. an explicit task binding in the CoS deployment configuration;
4. a normalized marker emitted when a CoS episode begins;
5. a conservative heuristic only as a fallback, recorded with its confidence and reasons.

Do not classify every task that mentions email, projects, or meetings as a Chief-of-Staff task. Until the harness exposes a dependable invocation marker, identification remains an adapter decision to test rather than a convention hidden in the skill.

## Normalized Run Record

The first implementation artifact should be a `cos-run/v1` schema. At minimum, a record needs:

```yaml
schema: cos-run/v1
run_id: stable local identifier
thread_id: harness task identifier
turn_id: harness turn identifier
task_classification: dedicated-cos | mixed | other | unknown
identification:
  method: skill-invocation | scheduler-binding | configured-task | episode-marker | heuristic
  confidence: high | medium | low
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
capture:
  method: task-authored-receipt | codex-structured-history | native-rollout-adapter
  limitations: []
privacy: {}
```

Each source observation should preserve identity, retrieval time, freshness, and a protected reference to the underlying evidence. Each tool action should record its action class, especially whether it was read-only, draft-only, approval-requesting, or mutating.

Hidden reasoning is not required. Explicit, user-visible rationale tags such as `deadline-within-48h`, `unanswered-request`, or `source-conflict` are more auditable and portable.

## Wiki Memory Adapter

The wiki-memory adapter is a governed procedure, not a memory store embedded in the operational task:

```text
selected trajectories + outcomes
        │
        ▼
Wiki Maintainer
        │
        ├── instance facts remain in vault or source
        └── procedural generalities enter evolution wiki
        │
        ▼
optional narrow skill proposal
        │
        ▼
human adoption decision
```

The adapter learns how the Chief of Staff should retrieve, prioritize, verify, route, and communicate. It does not learn a shadow database of current people, projects, messages, papers, or deadlines. Operational runs never read the evolution wiki; only an accepted skill revision changes their behavior.

## Delayed Outcomes

A CoS response may only become evaluable hours or days later. Raw run records therefore remain immutable while outcome observations are appended separately:

```text
<trajectory-container>/runs/<run-id>.json
<outcome-container>/<run-id>.jsonl
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

A candidate skill must be assessed against evidence independent of the examples that induced the proposed change. During early use, that evidence can be subsequent real episodes reviewed by the user. Frozen, redacted, or synthetic fixtures should be retained when representative cases emerge and repeatable comparison becomes useful. Mutating behavior must never be replayed against live systems merely for evaluation.

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

Adopt a proposal only when the available evidence and human review justify the targeted change without an apparent material regression. Label early decisions exploratory when no representative comparison set exists. Record acceptance, rejection, or rollback in the evolution log and update the skill-impact record.

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
- Treating one Git or storage policy as intrinsic to every raw container
- Committing raw personal traces to the portable plugin repository
- Replacing the vault with learned summaries
- Treating user engagement as the sole measure of quality
- Automatic semantic capture
- Automatic external mutation
- Assuming that a policy learned in Codex transfers unchanged to every harness
