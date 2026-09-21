# Task template

[Home](../README.md) · [Task flow](../docs/task-flow.md#task-identity-and-template) ·
[Local adoption](TASKFLOW.MD) · [Copying](README.md#copying-templates)

Copy the following into `TODO/NS-<goal>_<feature>_<xx>.md`. Replace placeholders
with actual content and relative Markdown links. This is an illustrative task
definition, not an active task or a completion claim.

```markdown
# NS-N_feature_01 — Concrete outcome

<Relative links to the owning north-star anchor, task index and TASKFLOW.MD>

**Description:**

<High-level outcome, current gap, scope boundary and why it advances the goal>

North star: NS-N. Milestone outcome: <owner>.
Completion credit: <goal percentage points> (<overall points>).
Credit is earned only when every acceptance criterion and task-flow requirement passes.
Starting evidence: <current contracts, implementation and evidence links>.

**Acceptance Criteria:**

- <Observable delivered result and supported cases>.
- <Relevant failure, boundary, integration and invariant checks>.
- <Evidence and any actual user or independent-consumer verdict required>.

**Blockers**

- <Relative link to each prerequisite task; use None when there are none>.
- External input: <if applicable, what is needed and how it becomes satisfied>.
```

Add the dated acceptance evidence under Description when all criteria pass.
Move the same filename into `TODO/DONE/` and complete the
[linked completion updates](../docs/task-flow.md#acceptance-and-completion).
