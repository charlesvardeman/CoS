# Codex Installation and First Run

## Package Shape

The root `plugin.json` is the portable Agent Plugins 1.0 manifest. `.codex-plugin/plugin.json` is the Codex installation wrapper and points to the same `skills/` directory. User configuration, scheduler state, trajectories, outcomes, credentials, and vault content remain outside the installed package.

## Installation-Ready Gate

Before installing a revision:

1. Validate the Codex wrapper and all three skills.
2. Ensure the source tree contains no trajectory, outcome, credential, or user-specific configuration instances.
3. Commit the intended plugin revision so episode receipts can identify the operational skill version.
4. Install or update the plugin through a local marketplace using the bundled Plugin Creator workflow rather than editing marketplace state by hand.
5. Start a new Codex task so the installed revision is loaded cleanly.

The public repository is the distributable source, not the deployment-state store. Installing from a public revision must not copy a user's private configuration or raw containers back into the repository.

## First-Run Contract

Create one durable task in the workspace that can retrieve from the vault. Invoke `configure-chief-of-staff` in that task. Configuration should:

- bind only the approved vault and live-source capabilities actually available in the harness;
- establish a private location for runtime state, trajectory receipts, and delayed outcomes;
- record the task as the dedicated Chief-of-Staff task;
- propose one thread heartbeat, recommending a 30-minute cadence initially;
- keep no-change heartbeats quiet while preserving a local checkpoint and trajectory receipt;
- obtain explicit approval before writing configuration or creating the heartbeat.

After approval, setup creates the native thread heartbeat. The heartbeat prompt should be short and durable: inspect the approved inbound and planning sources, prioritize what matters, research enough context to make the item useful, prepare drafts but do not send them, remain quiet when nothing changed, and append the configured episode receipt.

## Learning Cycle

Do not give the operational task access to the evolution wiki. When the user requests an evolution review—or enough meaningful episodes have accumulated—run `evolve-chief-of-staff` separately against selected receipts, outcomes, the wiki, and the current skill version.

The first learning cycle is complete when:

1. a real heartbeat or interactive CoS episode produced a usable receipt;
2. user feedback or an observable outcome was linked to it;
3. the wiki-memory adapter extracted a procedural generalization without copying instance facts;
4. any resulting skill proposal was reviewed explicitly; and
5. a later real episode provided evidence about the change.

A full Codex event exporter, automatic Maintainer cadence, and retained evaluation corpus are later improvements, not prerequisites for first use.
