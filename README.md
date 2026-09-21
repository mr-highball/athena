# Athena

Reusable standards for Pascal projects and the agents helping maintain them.
The baseline is a command-line Free Pascal Compiler (FPC) build with GitHub
Actions. Engines, browser targets, containers and agent products are optional.

This collection carries engineering lessons, not an application's architecture,
asset collection, account settings or release history. Public upstream identifiers
appear only where needed to identify tools. Existing license notices remain intact.

## Start here

1. Read [principles](docs/principles.md) and [coding standards](docs/coding-standards.md).
2. Choose the applicable [build path](docs/fpc-builds.md#choose-a-path).
3. Adopt a small [project profile](templates/PROJECT.md) and
   [agent entry point](templates/AGENTS.template.md).
4. [Inspect and prepare the local environment](docs/local-environment.md), reusing
   tools that pass the required probes.
5. Start with the [native example](templates/native-fpc.md) and
   [GitHub Actions template](templates/github-actions.md#native-job).
6. Select [validation by impact](docs/validation.md#validation-matrix) and a
   [work profile](docs/agent-stewardship.md#work-profiles).
7. Apply [Task flow](docs/task-flow.md) to connect north stars, milestones,
   prerequisite tasks and accepted progress throughout agentic design work.

Markdown examples are adoption templates, not installed workflows or active
agent configuration. Replace declared placeholders before use. Athena does not
install compilers, change account settings or enable deployment.

## Standards map

| Topic | Standard | Example or conditional path |
| --- | --- | --- |
| Language, naming and layout | [Coding standards](docs/coding-standards.md) | [Native FPC](templates/native-fpc.md) |
| Ownership and dependencies | [Dependencies](docs/dependencies.md) | [Optional CGE](docs/platforms/cge.md) |
| Local setup and reuse | [Environment bootstrap](docs/local-environment.md) | [Toolchain record](templates/TOOLCHAIN.md) |
| Reproducible builds | [FPC builds](docs/fpc-builds.md) | [CI templates](templates/github-actions.md) |
| Determinism and scoped edits | [State and constraints](docs/state-and-constraints.md) | [Work record](templates/WORK.md) |
| Tests and release evidence | [Validation](docs/validation.md) | [Browser checks](docs/platforms/browser.md) |
| Delivery and caches | [GitHub Actions](docs/platforms/github-actions.md) | [Optional Pages](templates/github-actions.md#pages-extension) |
| Agent effort and delegation | [Stewardship](docs/agent-stewardship.md) | [Optional Codex hints](docs/platforms/codex.md) |
| Agentic design and task flow | [Task flow](docs/task-flow.md) | [Milestones](templates/MILESTONES.md), [local flow](templates/TASKFLOW.MD), [tasks](templates/TASK.md) |
| Connected, reusable knowledge | [Documentation](docs/documentation.md) | [Lessons](docs/lessons.md) |

## Adoption and updates

Maintainers of this collection use the short [Athena agent entry point](AGENTS.md).

Copy the selected documents while preserving their relative layout, or vendor
Athena at a reviewed Git commit and point the project's root instructions at it.
Do not assume an agent automatically reads instructions inside a submodule.
Keep local decisions in the project profile instead of rewriting shared rules.
See [submodule adoption](docs/dependencies.md#submodule-workflow) and
[template portability](templates/README.md#copying-templates).

Mandatory requirements, defaults and conditional requirements have distinct
meanings in [principles](docs/principles.md#rule-strength). Read only the linked
pages needed for the current task; the map is navigation, not a requirement to
load the entire collection into every agent context.

External implementation details were checked on 2026-09-13. Versioned guidance
must be rechecked when adopting or upgrading a tool. Local example validation
and its limitations are recorded in [template verification](templates/README.md#verification).
