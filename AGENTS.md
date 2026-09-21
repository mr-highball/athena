# Working in Athena

Maintain this as a project-agnostic standards collection. Start at the
[standards map](README.md#standards-map); read only the relevant linked pages.

- Apply [Pascal coding standards](docs/coding-standards.md) to authored tools.
  Shell scripts may orchestrate builds; do not introduce Node, Python or a
  separate implementation of domain logic.
- Preserve the native FPC baseline. Put engine, browser and platform requirements
  behind explicit conditions using [build paths](docs/fpc-builds.md#choose-a-path).
- Before setup, [inspect existing tools](docs/local-environment.md#inspect-before-installing)
  and reuse verified capabilities; ask only for missing target or installation choices.
- Use [Lean stewardship](docs/agent-stewardship.md#work-profiles) by default.
  This file does not authorize delegation. Do not spawn agents unless the current
  task explicitly authorizes it or another applicable instruction requires it.
- Apply [Task flow](docs/task-flow.md) as core design governance: connect work
  to north-star outcomes, follow prerequisite tasks, record discovered gaps and
  update milestones from accepted evidence when tasks move to DONE.
- Do not copy private paths, accounts, forks, transcripts, usage history or
  personal configuration into examples. Preserve existing legal notices.
- Link requirements to their rationale and examples. Check local paths,
  section anchors and orphan documents using [documentation checks](docs/documentation.md#checks).
- Validate examples according to [their status](templates/README.md#verification).
  Do not claim that an illustrative workflow has run on GitHub.
- Change only this repository for its maintenance. No account changes, automatic
  dependency updates or publishing follow merely from editing documentation.
