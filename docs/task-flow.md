# Task flow

[Home](../README.md) · [Principles](principles.md) ·
[Stewardship](agent-stewardship.md) · [Templates](../templates/README.md)

## Core design governance

Required: agentic design work must connect the intended end state, current
evidence, remaining outcomes and the next authorized action. This standard owns
that connection. Small implementation tasks serve the full goal; task volume,
time spent and successful experiments do not establish completion.

For work spanning multiple milestones, maintain the files below. A bounded
one-off change may keep the same scope, acceptance and evidence in its
[work record](../templates/WORK.md) without creating an artificial backlog.
An explicit request for a task catalog takes precedence over that simplification.

| Record | Owns |
| --- | --- |
| `MILESTONES.md` | North stars, accepted baseline, completion assessment, remaining outcome-to-task mapping and next meaningful milestones |
| `TASKFLOW.MD` | Project adoption of this standard, local paths and explicit workflow decisions |
| `TODO/` beside `MILESTONES.md` | Open task definitions, acceptance criteria and prerequisite links |
| `TODO/DONE/` | Accepted tasks, retaining their filenames and completion evidence |
| `TODO/README.md` | Task navigation, north-star ownership, credit allocation and dependency order |
| Work record and topic documents | Current handoff and supporting evidence; links to tasks instead of competing backlogs |

Use an existing milestone filename if appropriate; record the canonical location
in the project profile. If several milestone files are needed, give each a clear
scope and one top-level index. Never maintain competing totals or task definitions.
See the [milestone](../templates/MILESTONES.md),
[local flow](../templates/TASKFLOW.MD) and [task](../templates/TASK.md) templates.

## Establish and reassess the destination

1. Give each north star a stable ID, an observable end state, scope boundaries
   and explicit conditions for 100%. Keep actual user outcomes visible alongside
   implementation capabilities. Preserve required foundations and invariants.
2. Assess current capability from evidence. Distinguish implemented, integrated,
   evaluated and accepted behavior. Summarize completed work in the goal scorecard
   with evidence links; remove it from the active backlog. Do not invent historical
   DONE files merely to fill the directory.
3. Map every unfinished requirement to task files, including integration,
   validation, quality, delivery and independent use where the goal requires them.
   Explain deliberate exclusions. Check the entire intended scope, rather than
   copying an old percentage or only extending the current implementation list.
4. Identify real prerequisites and external inputs. Keep one credit owner for
   shared work even when several north stars consume it.
5. Group tasks into milestones that deliver meaningful observable progress.
   State the expected contribution and evidence needed, not just a list of small
   convenient edits. Record any user-specified minimum progress threshold locally;
   if the proposed package falls short, reassess the package before proceeding.
   Never inflate task credits to meet that threshold.

A catalog is exhaustive for its declared scope when every remaining requirement
has an owner and acceptance path. It cannot predict every future discovery.
Reassess when new evidence changes scope, disproves accepted behavior, or repeated
activity fails to advance acceptance. Explain why percentages remain unchanged:
partial work, a failed gate, an external dependency or a revised assessment.

If the user requests planning followed by review, produce the complete catalog
and stop at that boundary. Otherwise continue authorized execution without adding
an approval gate solely because a plan or milestone file exists.

## Task identity and template

Use `NS-<goal>_<feature>_<xx>.md`, such as `NS-1_import_01.md` and
`NS-1_import_02.md`. The goal ID must match the scorecard. Feature names use
lowercase words separated by hyphens. Related tasks share the feature base and
increment the numeric suffix, starting at `01`; extend beyond two digits after
99. Never reuse a suffix or renumber files after completion. The suffix is an
identity, not a priority, prerequisite or file-format version.

Every task contains these three sections, as shown in the
[task template](../templates/TASK.md):

- **Description:** High-level outcome, current gap, scope boundary, north-star
  owner, starting evidence and allocated completion credit.
- **Acceptance Criteria:** Bulleted observable pass conditions, supported cases,
  relevant failure cases and evidence required to accept the intended result.
- **Blockers**: Bulleted relative links to task files that must be completed
  before this task can be accepted. Use `None` when there are no prerequisites.
  List external needs separately within this section, with their unblock condition.

Keep navigation links to the owning goal, task index and local task flow. Criteria
must be sufficient to distinguish a delivered result from an experiment or draft.
Do not weaken acceptance merely to close a task.

## Dependency order and execution

Follow the user's priority. In the absence of a different agreed order, start
with the least-complete north star, then choose a task that advances its next
meaningful milestone. Read the selected task, its evidence and the current work
record before implementation. Keep one current task and record the return path.

Follow unmet prerequisite links first, including tasks owned by another north
star; return to the originating task once they are accepted. A prerequisite is
satisfied by accepted evidence and DONE status, not by a draft or a passing
isolated check. Check that this evidence still applies. External input remains
unresolved until it is actually supplied; do not invent a verdict or authority.

Keep the dependency graph acyclic. Blockers are hard acceptance prerequisites;
related work belongs in the description. Split independently deliverable
preparation from later integration when that resolves a cycle. A suggested
dependency order is navigation, not authorization for concurrent agents.

Implement the smallest useful part of the selected outcome using existing
verified tools. Apply [impact-based validation](validation.md#validation-matrix)
to the changed boundary and intended consumer. For exploratory work, declare a
hypothesis, evidence policy, bounded experiment budget and stop/switch condition.
Follow [stewardship](agent-stewardship.md#usage-and-waiting) when attempts repeatedly
fail on the same cause. Keep successful baseline behavior available.

## Newly discovered work

When a gap requires a separate task, stop expanding the current scope, create
the task immediately, and return to the current task's agreed outcome.

- Give the gap a north-star owner, concrete acceptance, the next unused filename
  and an allocation from remaining scope. Add it to the index and milestone map.
- For independent follow-up work, retain the current scope and finish it.
- For a true prerequisite, add its task link to the current task's blockers,
  keep the current task open, finish independent current work where useful, then
  follow the prerequisite and return. Do not mark the current task DONE just to
  satisfy an instruction to finish it.
- If previously accepted criteria were not met, reopen the task and reassess
  affected completion. A distinct follow-up cannot conceal a failed original gate.

A possible enhancement outside the declared destination is not automatically a
missing requirement. Explain its connection to the goal before expanding scope.

## Acceptance and completion

A task is DONE only when all acceptance criteria pass and all blockers are
satisfied. Record a dated completion paragraph under Description with the
revision or artifact identities, commands and targets where applicable, actual
results, required review verdicts and limitations. Link detailed evidence.
Implementation tasks must reach maintained code and the intended consumer;
an isolated study alone is insufficient. Documentation or planning tasks earn
credit only for their own declared deliverable, never for future implementation.

In the same logical completion change:

1. Move the task from `TODO/` to `TODO/DONE/`, preserving its basename.
2. Repair incoming prerequisite/index/milestone links and the moved file's
   relative links. Preserve links to completed prerequisites as evidence.
3. Remove the task from the active queue, update its catalog status and the
   milestone assessment, including the owning north-star completion percentage.
4. Record the accepted result, unblocked work and next bounded action in the
   work record. Keep completed details out of the remaining-work list.
5. Check links, dependency consistency and completion arithmetic. Apply only
   validation warranted by the actual change.

If a task is reopened, move it back to TODO, repair links, revoke its earned
credit and reconsider dependent acceptance. Preserve historical evidence and
explain why it no longer establishes the claimed capability.

## Honest percentage accounting

For milestone-driven work, declare an evidence-backed percentage baseline for
each goal and allocate its remaining points to tasks before execution. Use goal
weights totaling 100 when reporting an overall percentage:

```text
Goal completion = accepted baseline + accepted DONE task credits for that goal
Overall completion = sum(goal completion * goal weight / 100)
Task overall contribution = task goal credit * goal weight / 100
```

Baseline plus all allocated task credits must total 100 for each goal. Count
each capability once. Consuming a prerequisite, closing a parent outcome or
moving an already credited task does not earn the same credit again. Update
percentages on every accepted completion, even inside a larger milestone.

Percentages are planning judgments about accepted scope, not measurements of
time, cost, test counts or adoption. Display precision accordingly. Writing a
catalog, collecting inputs, running experiments or partially implementing a task
does not automatically advance product completion. Report useful intermediate
evidence separately without crediting unfinished criteria.

When tasks split or new work is found within the same scope, redistribute only
unearned credit and record the previous and new allocation. Genuine scope changes
or disproved baseline capability require an explicit reassessment with rationale;
retain the old assessment as history. Do not manufacture points by adding files.
No 100% claim is valid while required outcomes or acceptance evidence remain open.
