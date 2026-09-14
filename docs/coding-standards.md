# Coding standards

[Home](../README.md) · [Builds](fpc-builds.md) · [State contracts](state-and-constraints.md)

## Pascal dialect and layout

Default to `{$mode delphi}` and `{$H+}` in authored units and programs.
Use two spaces, UTF-8 text and LF line endings. Aim for 100 columns.
Put each record field, class field and local variable on its own line.

Write `begin` and `end` on separate lines. Expand conditional and loop bodies;
avoid several assignments or case actions on one line. Separate declarations,
initialization and distinct operations. Spell built-in types consistently:
`String`, `Integer`, `Boolean`, `Single`, `Double`.

## Names

| Element | Convention |
| --- | --- |
| Unit and filename | Lowercase dotted project namespace: `sample.model.pas` |
| Type | `TDocument`, `TRequest` |
| Parameter | `ADocument`, `AReason` |
| Local | `LDocument`, `LIndex` |
| Stored field | `FRevision`, `FNodes` |
| Local constant | `CMaximumItems` |
| Shared constant | `MaximumItems` |
| Unavoidable global | `GApplication` |
| Routine and property | `ValidateDocument`, `Revision` |
| Exception binding | `LException` |

Use `I`, `J`, `K` only for short, obvious indexed loops. Match each unit's
declaration to its filename. Choose the namespace in the
[project profile](../templates/PROJECT.md), not in this shared standard.
Preserve external APIs, upstream unit names and established serialized keys.
Do not mass-rename a mature dependency to satisfy local naming preferences.

## Ownership and correctness

Initialize managed records deliberately. Pair ownership and release with
`try/finally`. Treat dynamic arrays and contained records as potentially shared:
copy before mutating a candidate that must preserve its baseline.

Keep numerical and state logic independent of rendering, global random state,
locale and wall-clock timing. Specify units, signedness, bounds and failure
semantics. Explain non-obvious constraint meanings and validation, not each line
of syntax. See [state and constraints](state-and-constraints.md).

If code also targets pas2js, follow the [browser language cautions](platforms/browser.md#language-and-bridge-cautions)
and run shared fixtures on both targets. A native pass does not prove browser
record/array ownership or numerical parity.

## Source and scripts

Use Pascal for product code and substantive tools. Keep scripts to the
[orchestration boundary](dependencies.md#dependency-boundary).
Use explicit compiler parameters, quote paths, propagate exit codes and write
generated files under `build/`. Examples are in [native FPC](../templates/native-fpc.md).

Required for authored source and scripts: retain the complete applicable project
license notice, including its actual copyright holder. Templates use placeholders;
adopters supply their own notice. Preserve third-party notices and record imported
asset licenses. Do not copy another project's identity into a reusable template.

Do not reformat or patch submodules in a consuming repository.
Use the [dependency change workflow](dependencies.md#submodule-workflow).
