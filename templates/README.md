# Adoption templates

[Home](../README.md) · [Documentation rules](../docs/documentation.md) · [Local setup](../docs/local-environment.md)

## Choose templates

| Template | Purpose |
| --- | --- |
| [Project profile](PROJECT.md) | Targets, namespace, pins and accepted exceptions |
| [Agent entry point](AGENTS.template.md) | Minimal instructions routed to shared standards |
| [Toolchain record](TOOLCHAIN.md) | Portable pins and separate local readiness evidence |
| [Work record](WORK.md) | Scope, checks, deferrals and handoff |
| [Native FPC example](native-fpc.md) | Compilable fixture and shell commands |
| [GitHub Actions](github-actions.md) | Native workflow and optional Pages extension |
| [CGE build](cge-build.md) | Pinned engine and target-aware commands |
| [Windows toolchain](toolchain-windows.md) | Native FPC and conditional web setup routes |
| [Linux web toolchain](toolchain-linux.md) | Pinned native/WASM/pas2js bootstrap |

## Copying templates

Templates here are documents, not an auto-installer. Copy the relevant fenced
content into the adopting project's files. Resolve placeholders and paths.
Keep the surrounding documentation linked from the resulting script/workflow.

If the entire Athena directory layout is retained, links in these templates
resolve as written. If a template becomes a root project file or Athena is
vendored under `vendor/athena/`, rewrite its relative links accordingly.
For example, a root project instruction can link to
`vendor/athena/docs/coding-standards.md`. This is a path example, not an existing
link in this repository.

Keep local environment evidence ignored. Commit only public pins, capabilities
and portable build instructions. Preserve the adopter's license notices.

## Verification

The native fixture is intended to be compiled with the local FPC command shown.
All Markdown documents and local section links are checked as a connected set.
The delivery record below distinguishes actual checks from illustrative recipes.

GitHub-hosted jobs, Linux package installation, container images, Windows
installation and a new CGE/WASM bootstrap are not executed merely by maintaining
this handbook. Check their prerequisites and record results when adopting them.
Public action refs were resolved to their pinned commits; image tags remain
explicit candidates until an adopter records and probes a digest.

## Delivery record

Checked on 2026-09-14:

- All 26 Markdown documents are reachable from the root README; all 239 local
  file and section links resolve.
- The native fixture compiled and passed with FPC 3.3.1 on Windows/i386, with
  assertions, range, overflow and I/O checks enabled. FPC 3.2.2 remains an
  illustrative CI baseline; this task did not execute that compiler.
- All 11 Bash examples and all PowerShell examples passed syntax parsing.
  Parsing does not establish installation or workflow success.
- No tool installation, Linux bootstrap, container build, CGE/browser execution
  or GitHub-hosted workflow was performed for this documentation change.

Recheck changed examples when adopting them and record target-specific results.
