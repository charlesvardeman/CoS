# Operating Policy

Read this reference for inbox triage and periodic attention reviews.

## Initial Review Modes

The first operational version supports three bounded modes:

1. **Inbox triage:** inspect approved inbound channels for unanswered asks, commitments, decisions, and information requiring routing.
2. **Periodic attention review:** reconcile the approved work calendar, task list, work email, and active project context to identify what may change the user's next move.
3. **Meeting preparation:** invoke the available meeting-preparation capability or retrieve the relevant project, people, previous meetings, open commitments, and current agenda context.

Do not assume that a named connector or specialist exists. Use the capabilities available in the current environment and identify unavailable sources that materially limit the result.

## Source Selection

Start from the requested mode and decision horizon. Retrieve the smallest set of sources needed to answer the operational question.

- Use the vault for curated identity, relationships, decisions, project context, and literature context.
- Use live systems for current messages, events, task status, and recently changed source state.
- Use specialist skills for their bounded workflow when available; do not restate their implementation inside Chief of Staff.
- Use task status to coordinate work, not as a substitute for the durable project record.

Record source identity and observation time for mutable claims. When a source is stale, unavailable, or outside the approved scope, say so without implying it was checked.

## What Deserves Attention

Investigate and potentially surface signals such as:

- a direct question or request that lacks a response;
- a commitment approaching its decision or preparation horizon;
- a blocker, dependency, or source conflict that changes what can happen next;
- a project or relationship drifting from an explicit expectation;
- an upcoming meeting with a meaningful preparation gap;
- a completed specialist task whose result requires review or routing;
- a genuinely useful synthesis from fresh evidence that may alter a decision.

Give greater weight to signals that are likely unseen, consequential, time-sensitive, externally dependent, or costly to recover from later.

Usually suppress:

- ordinary message churn;
- information already acknowledged or resolved;
- unchanged status copied from the previous run;
- weakly supported guesses;
- novelty without consequence;
- generic summaries with no decision or useful next step.

Do not force every signal into one numerical score. Explain prioritization using observable factors and appropriate uncertainty.

## Retrieval Depth

Retrieve enough context to make the item legible and the proposed next step useful. Stop when further retrieval is unlikely to change prioritization, factual confidence, or the recommended action.

If answering a detected request requires substantial research or delivery work, create or recommend a bounded specialist task according to the current harness and authorization policy. The Chief of Staff remains responsible for the handoff and later status interpretation, not for hiding a large project inside a recurring scan.
