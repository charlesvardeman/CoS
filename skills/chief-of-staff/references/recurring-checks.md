# Recurring Checks

Read this reference when Chief of Staff is invoked by a scheduler or when the user asks to design recurring behavior.

## Separation of Concerns

The scheduler decides when to invoke a run. The Chief-of-Staff skill decides what to inspect and whether anything deserves attention.

Do not assume Codex heartbeat semantics in the portable procedure. In Codex, an installation profile may supply the separate `loop` skill or native automation capability. Other clients may supply a different scheduler.

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

Discussing or drafting a check-in does not authorize its creation. Create, update, pause, resume, or delete an automation only when the user explicitly requests that action and the harness provides an appropriate scheduling capability.

Prefer updating the one existing matching Chief-of-Staff schedule over creating a duplicate. The deployment system must prevent two hosts from scanning the same sources concurrently.
