# Configuration Contract

The package defines this contract but does not store the user's configured instance inside an installed skill directory.

## Suggested Shape

```yaml
schema: cos-config/v1
profile_id: user-selected stable identifier
task:
  thread_id: host-provided durable task identifier
  classification: dedicated-cos
review_modes:
  inbox-triage:
    enabled: true
    source_roles: []
  periodic-attention-review:
    enabled: true
    source_roles: []
  meeting-preparation:
    enabled: true
    source_roles: []
capabilities:
  vault_retrieval: provider binding or unavailable
  semantic_capture: provider binding or unavailable
  email_read: provider binding or unavailable
  calendar_read: provider binding or unavailable
  task_read: provider binding or unavailable
  drafting: provider binding or unavailable
  scheduler: provider binding or unavailable
  task_status: provider binding or unavailable
  trace_history: provider binding or unavailable
sources: []
attention_policy:
  interruption_posture: conservative | balanced | proactive
  quiet_hours: user-selected value
  user_overrides: []
authorization:
  read_scopes: []
  draft_scopes: []
  approval_required: []
storage:
  operational_state: external protected location
  trajectory_container: raw container binding or unavailable
  outcome_container: raw container binding or unavailable
  raw_containers: []
  evolution_wiki: governed location
trajectory_capture:
  enabled: true
  recorder: task-authored-receipt | host-adapter
  content_posture: privacy-minimized
scheduler:
  desired: true
  kind: thread-heartbeat
  cadence: user-selected value; recommend 30 minutes for initial Codex setup
  active_host: null
  automation_id: null
```

This is a semantic shape, not a mandate to use YAML. A host-native configuration system is acceptable if it preserves the distinctions.

Each entry in `raw_containers` follows [raw-container-policy.md](raw-container-policy.md). It declares evidence authority separately from physical location, Git treatment, backup, update semantics, discovery, retention, privacy, disclosure, and promotion. Do not assume that all raw containers are external, ignored, or unsearchable.

The trajectory and outcome fields bind CoS continual learning to configured containers; they do not authorize broad task-history capture. Setup must explicitly authorize the bounded operational task to append its own privacy-minimized episode receipts. A host adapter requires separate scope and policy.

## Source Entries

Each configured source should state:

- role, such as semantic context, email, calendar, tasks, literature, reading inbox, or task status;
- provider or capability binding;
- account or collection identifier when required, stored privately;
- allowed read, search, draft, and action scopes;
- authoritative claim types;
- expected freshness and unavailable-source behavior;
- retention or redaction constraints.

Do not interpret a connector's technical permission as user authorization for every action it supports.

## Initial Personal Profile

For the first implementation, the intended source set is:

- the existing personal knowledge vault and active project notes;
- the selected work calendar;
- the selected work task list;
- work Gmail;
- bounded status from specialist tasks and later Zotero or Readwise ingestion workflows.

These are configuration intentions, not embedded provider identifiers or permission grants. Resolve the actual bindings during approved setup.

The initial mutation policy is:

- read-only retrieval and draft generation are the starting capability envelope;
- no automatic semantic capture;
- sending, calendar changes, shared-document changes, task mutation, automation changes, and semantic-memory writes require explicit approval.

## Persistence

Before writing configuration, identify the proposed destination and whether it is machine-local, mounted, shared, or versioned. Never store credentials, tokens, raw source exports, or native task history in the portable package.

Changing configuration does not automatically update a live scheduler. If an existing automation prompt embeds old source scope or policy, propose a separate automation update and obtain authorization before applying it.
