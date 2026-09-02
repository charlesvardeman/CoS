---
name: configure-chief-of-staff
description: Configure an existing Chief-of-Staff environment, including its durable task, vault and source capabilities, attention policy, trajectory storage, and recurring heartbeat. Use for first setup, partial setup, or deliberate reconfiguration; do not use for ordinary reviews or treat configuration as permission to scan unapproved sources.
---

# Configure Chief of Staff

Build or revise the smallest usable Chief-of-Staff operating contract for the current environment. Prefer discovering established context over replaying generic onboarding.

Read [references/configuration-contract.md](references/configuration-contract.md) before proposing or persisting configuration.

When configuration includes source evidence or CoS trajectory storage, also read [references/raw-container-policy.md](references/raw-container-policy.md).

## Determine Setup State

Classify the environment without ceremony:

- `new`: no usable vault, source map, attention policy, or approval boundary is known;
- `partial`: some elements exist, but material gaps prevent a reliable review;
- `established`: the vault and core workflows already exist; inspect them and ask only for missing or changed choices.

Do not create a new vault, duplicate an existing project system, or import another assistant's memory structure when established infrastructure is available.

## Configuration Workflow

1. Inspect the available vault instructions and capability inventory without scanning private source content more deeply than setup requires.
2. Identify the intended review modes and the source roles needed for each.
3. Propose least-privilege read, search, draft, and action scopes. Keep unavailable and denied actions explicit.
4. Calibrate what deserves interruption, what should remain quiet, and how uncertainty should be presented.
5. Propose output forms, the external location for configuration and operational state, and any required raw-container bindings with explicit per-container policies.
6. Propose one heartbeat attached to the durable Chief-of-Staff task, including scope, cadence, quiet behavior, and stop or pause conditions. Recommend 30 minutes for the initial Codex profile unless the available sources or user preference warrant another cadence.
7. Ask separately before writing configuration, creating the heartbeat, installing a capability, or scanning a newly approved source.
8. When approved and supported by the harness, create or update the one matching thread heartbeat rather than leaving the user to assemble it manually.

Configuration may point to the user's vault and installed capabilities. Do not copy current people, projects, messages, meetings, or account data into the skill package.

## Completion

Configuration is complete when the approved operating modes, durable-task binding, source roles and scopes, attention posture, output preferences, mutation boundary, state location, trajectory and outcome bindings, required raw-container policies, and scheduler state are recorded. The heartbeat may be explicitly disabled, but it is not silently deferred in a normal Chief-of-Staff deployment.

Return the resulting configuration summary, remaining capability gaps, and any separate actions awaiting approval.
