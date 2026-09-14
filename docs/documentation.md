# Connected documentation

[Home](../README.md) · [Lessons](lessons.md) · [Templates](../templates/README.md)

## One source for each rule

Keep requirements in their owning standard, rationale in lessons and concrete
commands in templates. Link between them rather than copying the same rule
into multiple pages. Root instructions should route the reader, not embed the
entire handbook.

Every Markdown page must have an inbound path from the index and outbound links
to relevant standards or examples. Prefer a stable section anchor when the
relationship is specific. Changing a heading requires checking incoming links.

## Conditional guidance

State the condition first: “If CGE targets the browser, then…”.
Do not make a native CLI project install an engine, browser, container or agent
plugin merely because another project needed it.

Each recipe states prerequisites, placeholders, expected artifacts, verification
and what has not been run. Link CI commands to the relevant platform quirks.
See [build paths](fpc-builds.md#choose-a-path) and [template status](../templates/README.md#verification).

## Privacy and attribution

Use relative paths, role names and generic namespaces. Exclude personal account
names, local installation paths, private fork URLs, LAN addresses, screenshots,
conversation identifiers, usage percentages and customer data.

Public tool names, official upstream URLs and exact public registry identifiers
are technical references. Do not replace them with fabricated URLs to appear
generic. Preserve existing legal notices; source/script templates instruct
adopters to insert their own project's complete notice.

Cite upstream documentation next to version-sensitive claims. Record the check
date and recheck on upgrades. Do not present a mutable image tag as an immutable
pin or an example workflow as a successful deployment.

## Checks

Before delivering a documentation change:

- Resolve relative Markdown links and section anchors; detect orphan pages.
- Check references both from standards to examples and from examples to rationale.
- Search newly authored content for private paths/accounts and unfilled placeholders
  outside sections explicitly marked as templates.
- Compile executable Pascal examples and exercise the local commands available.
- State which runners, containers, browsers or external URLs were not tested.

A documentation check may be a small Pascal tool invoked by a build script.
It does not justify introducing a Node/Python documentation stack.
