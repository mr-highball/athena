# Project profile template

[Home](../README.md) · [Adoption](README.md) · [Build paths](../docs/fpc-builds.md#choose-a-path)

Copy and fill only what applies. This is a decision record, not a reason to ask
again for choices already supplied by the current task.

## Decisions

| Decision | Project value |
| --- | --- |
| Public purpose and Pascal namespace | TO BE SET |
| Native targets and supported FPC version | TO BE SET |
| CGE used? | Yes / No / Not decided |
| Browser used? | Yes / No / Not decided |
| WASM required? | Yes / No / Not decided |
| Supported setup host | OS and CPU architecture |
| Setup method | Reuse / isolated install / container / existing WSL |
| Build and focused test commands | Relative paths and arguments |
| Public dependency URLs and commits | None or explicit pins |
| Toolchain profile | Link to adopted TOOLCHAIN record |
| Publishing | None / artifacts / Pages, with branch and stage path |
| Work profile | Lean unless overridden |
| Goal and task records | Canonical milestones, local TASKFLOW.MD, TODO/DONE and work record paths |
| Exceptions | Scope, reason, evidence and revisit condition |

## Setup questions

If the target choices are absent, ask one short combined question:
“What should this project build: native FPC only, browser Pascal, or CGE
(native, browser, or both), and may missing tools be installed locally?”

Inspect existing tools before proposing downloads. Ask separately about system
changes only if the selected recipe requires them and authority is not already
established. Follow [local bootstrap](../docs/local-environment.md#initial-decisions).

## Acceptance

Define the full intended end state and explicit scope boundaries in the
[north-star milestones](MILESTONES.md). Use [Task flow](../docs/task-flow.md) to
map remaining requirements to tasks and accepted evidence. The next small outcome
advances that destination; it does not replace the agreed full scope.

Name the smallest runnable outcome, required invariants and supported execution
targets. Use [validation](../docs/validation.md), not an inherited full-product
test list. Record work-specific evidence in [WORK](WORK.md).
