# Agent entry point template

[Home](../README.md) · [Stewardship](../docs/agent-stewardship.md) · [Copying](README.md#copying-templates)

The following is content to adapt into the consuming repository's root
`AGENTS.md`. Rewrite link paths for that location.

## Suggested instructions

- Read the project profile and only the relevant linked standards.
- Apply [Task flow](../docs/task-flow.md) as core design governance. Read the
  milestones, local TASKFLOW.MD, current task and work record; follow blockers,
  record gaps as tasks, and update goal completion when accepted tasks move to DONE.
- Implement core behavior and maintained tools in Pascal. Shell scripts
  orchestrate compilation and platform tools. No Node/Python infrastructure.
- Follow the shared [coding conventions](../docs/coding-standards.md).
- Before setup, inspect the [toolchain record](TOOLCHAIN.md) and existing tools.
  Use [bootstrap decisions](../docs/local-environment.md#initial-decisions);
  do not reinstall a working toolchain or research setup from scratch.
- Keep dependencies pinned as [submodules](../docs/dependencies.md#submodule-workflow)
  when a dependency is justified. Do not edit dependency source in place.
- Default to [Lean](../docs/agent-stewardship.md#work-profiles), one primary agent.
  Delegation requires explicit authorization and a bounded independent task.
- Use the [validation matrix](../docs/validation.md#validation-matrix).
  Do not repeat passed broad suites without a changed risk.
- Preserve scope, locks, saved state and deterministic behavior. Report partial
  results and failures accurately.
- Keep evidence and handoffs concise, with commands and artifact paths.
  Do not copy personal information into shared documentation.
- Apply CGE/browser requirements only if the project profile selects them.
