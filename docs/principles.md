# Principles

[Home](../README.md) · [Coding](coding-standards.md) · [Lessons](lessons.md)

## Rule strength

**Required** means a compatibility or safety invariant. **Default** means the
starting choice, with a documented reason for a different choice. **If** introduces
a requirement only when that scenario applies. Record exceptions with scope,
rationale, evidence and a revisit condition in the [project profile](../templates/PROJECT.md).
Do not silently turn a preference into a release gate.

Project-specific user direction can narrow scope or replace local defaults.
It does not authorize misrepresenting evidence or overriding the execution
platform's higher-priority constraints. Resolve routine choices within the task;
ask only when information or authority is actually missing.

## Native baseline

Required: core behavior, validators, codecs, importers and maintained development
tools are Pascal. Build and test the portable core with FPC from a clean checkout.
Prefer the compiler's standard libraries and project-owned units.

Shell, PowerShell, Make, Git and CI YAML may acquire verified toolchains, invoke
compilers, manage build artifacts and report process failures. They must not
become parallel implementations of parsing, generation or validation.
No authored Node, Python, npm or pip infrastructure belongs in this baseline.
See [dependency boundaries](dependencies.md#dependency-boundary).

## Optional edges

If a project uses an engine, isolate engine types in adapters and retain native
core tests. If it uses a browser, generated JavaScript and its matched Pascal
runtime are target artifacts, not permission to add a JavaScript tool stack.
If it needs Docker, the container is a build environment, not an application
dependency. Follow the [decision table](fpc-builds.md#choose-a-path).

OS libraries, linkers, browsers and compiler build prerequisites still exist.
“Pure Pascal” describes owned implementations; it does not claim every tool
or platform underneath them is written in Pascal.

## Proportional effort

Deliver a small end-to-end result early. Protect determinism, data integrity,
scope, permissions and recovery; avoid elaborate gates that do not address the
change's risks. Prefer measurable acceptance over subjective grade loops.
Connect each lesson to a [focused check](validation.md), and each agent
assignment to a [bounded work record](../templates/WORK.md).

## Goal-directed design

Required: apply [Task flow](task-flow.md#core-design-governance) to keep agentic
design tied to the intended end state. North stars define accepted outcomes;
milestones connect them to dependency-linked tasks and evidence. Reassess scope
when evidence changes, and update completion from accepted results.
