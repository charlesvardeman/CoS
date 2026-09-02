# Recurring Checks

Read this reference when Chief of Staff is invoked by a scheduler or when the user asks to design recurring behavior.

## Separation of Concerns

The scheduler decides when to invoke a run. The Chief-of-Staff skill decides what to inspect and whether anything deserves attention.

Do not encode Codex heartbeat syntax in the portable procedure. In Codex, use a thread-local native heartbeat with the same minimal behavior as the installed `loop` skill. Other clients may supply a different scheduler.

Recurring operation is part of the default Chief-of-Staff experience. During first configuration, recommend one heartbeat attached to the durable Chief-of-Staff task. A 30-minute cadence is the initial Codex default when the user has not expressed another preference; adjust it when source latency, cost, quiet hours, or noise clearly justify a different interval.

## Check-In Contract

A recurring invocation should specify:

- bounded purpose and source scope;
- cadence and timezone;
- decision horizon or lookback window;
- quiet hours and notification policy;
- no-change behavior;
- completion or pause condition when the monitor is temporary;
- stable location of watermarks and pending action requests;
- active-host or duplicate-monitor protection when applicable.

Do not encode these user-specific values in this reference or in `SKILL.md`.

## Runtime Behavior

- Work first and notify only after deciding that a meaningful delta or useful next action exists.
- Use source watermarks to avoid repeatedly presenting the same unchanged item.
- Revisit prior pending items only when their status, urgency, evidence, or next action changed.
- Vary retrieval according to current risks rather than producing an identical generic digest each time.
- Report source failure when it materially weakens coverage; do not turn every transient failure into an interruption.
- Never wait for an interactive approval during an unattended run. Emit a persistent action request for later review.

## Creation and Mutation

Discussing or drafting a check-in does not authorize its creation. During setup, present the proposed scope, cadence, and quiet behavior and obtain explicit approval before creating it. Once activated, ordinary scheduled invocations do not require repeated approval; expanding source scope or enabling mutating actions does.

Prefer updating the one existing matching Chief-of-Staff schedule over creating a duplicate. The deployment system must prevent two hosts from scanning the same sources concurrently.

## Codex Heartbeat Profile

When configuration is approved in Codex:

- create a native heartbeat attached to the current durable task; do not create a detached cron task or a second Chief-of-Staff task;
- use a short name such as `Chief of Staff check-in`;
- put the approved sources and operational behavior in a self-contained prompt, while keeping cadence and task targeting in the automation fields;
- tell the heartbeat to retrieve intelligently, prioritize consequential unanswered or changing items, research enough context to prepare useful drafts, never send them without approval, stay quiet when nothing material changed, and append the configured trajectory receipt;
- persist the returned automation identifier in operational configuration;
- keep the task durable after each run rather than treating the recurrence as a temporary loop with a completion rename.

Do not expose raw scheduling syntax to the user. If the native automation capability is unavailable, report the capability gap instead of simulating recurrence.
