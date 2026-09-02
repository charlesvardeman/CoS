# Output Contracts

Read this reference before returning a structured operational result. These are semantic contracts; the user-facing rendering should remain concise and natural.

## Attention Item

Use an attention item when the user should know, decide, prepare, or follow up.

```yaml
schema: attention-item/v1
title: concise description
priority: now | soon | watch
what_changed: observable change or unresolved condition
why_now: consequence, timing, or decision relevance
evidence:
  - source: protected identifier or human-readable source
    observed_at: timestamp when material
    freshness: current | possibly-stale | stale | unknown
confidence: high | medium | low
next_step: smallest useful next move
action_class: inform | draft | approval-required | delegate
```

Do not surface schema fields mechanically when prose is clearer. Preserve the distinctions even in a short narrative.

## Draft

A draft is editable content prepared for the user. Identify its intended destination and the source context used. Clearly state that it has not been sent or applied.

Do not place unsupported claims in a draft merely because they would make the response more persuasive. Mark unresolved facts for review.

## Action Request

Use an action request when the next useful step is externally mutating or otherwise restricted.

```yaml
schema: action-request/v1
action_id: stable identifier supplied by the host when available
proposed_action: exact bounded action
target: recipient, event, document, automation, or memory destination
rationale: why it is useful now
preview: draft or proposed change
side_effects: expected external changes
expires_or_revalidate: condition requiring a fresh check
status: awaiting-approval
```

An approval request is not authorization. Revalidate time-sensitive state before executing a previously approved request when circumstances may have changed.

## No-Change Result

For an interactive request, say concisely that no meaningful change was found and identify important source limitations. For an unattended scheduled run, remain silent unless the host requires a local checkpoint.

A checkpoint may record the run time, source watermarks, skill version, and source failures. It is operational state, not a user notification and not semantic memory.

## Brief Shape

When multiple attention items exist, order them by likely effect on the user's next decisions. A useful default shape is:

1. What needs attention now
2. What is coming soon
3. Drafts or approval requests ready for review
4. Important source gaps or uncertainty

Omit empty sections. Avoid repeating unchanged background that is already available through the linked project or vault context.
