# Trajectory Capture

Read this reference after an operational episode when `trajectory_capture.enabled` is true.

## Purpose

Append enough temporally ordered, observable evidence for a later maintainer to understand what the Chief of Staff did and how the result arose. This is not semantic memory, a retrospective narrative, or hidden reasoning.

The first Codex profile uses a task-authored receipt. A future host adapter may enrich it with native event identifiers and failure boundaries. Record which method produced the evidence and do not claim task-authored capture is a complete native transcript.

## Minimal Receipt

Write one append-only `cos-run/v1` record to the configured trajectory container. Include:

- stable run, task, and turn identifiers when available;
- start and completion timestamps, invocation type, and review mode;
- skill version or package commit;
- ordered observable steps: source queries, retrievals, tool actions, material results, drafts, and approval events;
- source identity, observation time, freshness, and protected evidence locator;
- attention items produced or suppressed, with concise user-visible rationale tags;
- result state: `completed`, `partial`, `failed`, or `no-change`;
- source limitations, compaction boundaries known to the task, and capture method;
- privacy treatment applied to the record.

Prefer stable identifiers, hashes, redacted excerpts, and protected locators over copied message, document, or vault content. Never record credentials, hidden chain-of-thought, or unrelated conversation history.

Do not rewrite a completed record. Append later user reactions or downstream observations to the configured outcome stream, linked by `run_id` and labeled as explicit feedback, observable outcome, or maintainer inference.

## Failure Behavior

Trajectory capture must not replace the operational result. If the configured container is unavailable, preserve the user-facing result, report the capture gap when it affects learnability, and do not silently write the record somewhere else.
