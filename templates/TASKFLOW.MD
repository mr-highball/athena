# Local task flow template

[Home](../README.md) · [Task flow standard](../docs/task-flow.md) ·
[Task template](TASK.md) · [Copying](README.md#copying-templates)

Copy this structure beside the milestone file as `TASKFLOW.MD`. Adopt the shared
standard by a real link rather than copying its rules into a competing handbook.
Replace the path placeholders for the project's chosen layout.

```markdown
# Task flow

<Relative links to the shared task-flow standard, milestones, task index and work record>

## Governing standard

Apply the linked shared Task flow standard for naming, acceptance templates,
prerequisite traversal, task-size checkpoints, scope-preserving splits, gap handling,
TODO-to-DONE moves and percentage accounting.

## Local records

- Canonical milestone file: <path>.
- Open tasks and index: <sibling TODO directory and README.md>.
- Accepted tasks: <TODO/DONE directory and README.md>.
- Current work and evidence: <work record and topic document paths>.
- Task template: <adopted template path or shared template link>.

## Project decisions

- Priority: <user-directed order; otherwise least-complete north star>.
- Scope and invariants: <project profile link>.
- Review boundary: <explicit planning-only stop, if requested; otherwise authorized execution>.
- Completion baseline and allocations: <milestone scorecard and task index links>.
- Meaningful milestone threshold: <agreed value or not specified>.
- Batch/checkpoint record: <work-record section tracking acceptance criteria,
  deliverable, stop condition, consecutive batches without closure and reassessment>.
- Exceptions: <none, or scope, reason, evidence and revisit condition>.
```

Create `TODO/README.md` with relative links to all open tasks, their goal credits
and derived overall contributions, the dependency order, and the DONE index.
Create `TODO/DONE/README.md` linking back to the catalog and listing accepted
tasks with dated evidence. It may initially state that no tasks are completed.
Keep this catalog as the allocation ledger; other records reference it. Each task
also states its own allocation, and both must agree when an allocation changes.
Use the shared [progress checkpoint](../docs/task-flow.md#task-size-and-progress-checkpoints)
to reassess stalled work; keep the actual count and decision in the project's
work record rather than copying a second policy into this local template.
