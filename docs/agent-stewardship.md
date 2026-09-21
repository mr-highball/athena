# Agent stewardship

[Home](../README.md) · [Work record](../templates/WORK.md) · [Optional Codex hints](platforms/codex.md)

## Work profiles

[Task flow](task-flow.md) owns goal alignment, prerequisite traversal and task
completion. Apply it with these staffing and effort rules; a larger task catalog
does not authorize additional agents.

These are platform-neutral project defaults, not executable account settings.

| Profile | Staffing | Validation and review |
| --- | --- | --- |
| Lean (default) | One primary agent | Narrow implementation and the [impact matrix](validation.md#validation-matrix); no automatic critic. |
| Standard | Primary; at most one explicitly authorized helper concurrently | Bounded independent task or review where useful. |
| Intensive | Explicit task-specific concurrency and effort budget | Cross-cutting invariants or migrations with named acceptance and stop points. |

Do not switch profiles merely because the task takes time. State the missing
evidence or parallel work that would justify the change. User-requested limits
persist across turns. Finish authorized work rather than stopping at a proposal.

## Delegation and review

Delegate only when permitted by the active task and platform. A shared standard
is not blanket authorization to spawn agents. Require a concrete independent
deliverable while the primary has useful work to do.

Default helper depth is one; a helper does not spawn further helpers.
Count running and idle retained sessions as the platform actually accounts for
them. Reuse a relevant helper when useful; close finished helpers. Do not keep
spawning replacements for an unresolved specification.

Choose the least expensive available model/effort that can reliably handle the
subtask. Use capability classes rather than hardcoded model names in shared policy.
Escalate for demonstrated reasoning needs, not as a universal quality setting.

Give helpers only the necessary context, file ownership, constraints, acceptance
checks and expected output. Prefer one implementer and a bounded review over
several agents solving the same problem. The integrator remains responsible
for checking results and resolving conflicts.

A review gets a defined scope and actionable findings. Re-review the changed
risk after a fix; do not rerun the whole critique without a reason.
Never lower correctness requirements to hide excessive usage.

## Usage and waiting

Account for the primary, helper inference, duplicated context, tool output,
browser/CI repeats and waiting behavior. Elapsed time and message count are not
reliable measures of quota or cost. Report measured usage only when the platform
exposes it; otherwise say it is unknown.

Read targeted files; batch independent searches; avoid dumping whole logs or
reloading the standards collection. Keep handoffs concise and reference evidence.
Do useful independent work while jobs run. Prefer completion notifications or
bounded waits over busy polling; report progress only when something changes.

Default escalation point: after two unsuccessful attempts on the same cause,
stop blind retries, summarize evidence and change the diagnostic approach.
This is a local policy choice, not proof that the task is impossible.

## Policy versus enforcement

Markdown can guide behavior; it cannot enforce a provider quota, concurrency
limit, model entitlement or spending ceiling. Configure supported runner controls
where available and verify their semantics. Do not change account settings,
disable sandbox protections or add connectors merely to save usage.

For ChatGPT-style interfaces without exposed controls, use a scoped task,
explicit no-delegation request where appropriate, checkpoints and available usage
indicators. For Codex, see the [dated configuration hints](platforms/codex.md).
Keep personal settings outside the shared repository.

## Handoff

Include the current task, originating north star and prerequisite return path
from [Task flow](task-flow.md#dependency-order-and-execution). Update the canonical
milestone assessment when a task is accepted; keep the handoff a concise pointer.

Capture objective, accepted scope, completed changes, current revision, commands
already run, blockers, next bounded action and remaining budget if known.
Do not copy a chat transcript, private machine paths or credentials.
Use [the work template](../templates/WORK.md#handoff) and resume from it rather
than rediscovering completed work.
