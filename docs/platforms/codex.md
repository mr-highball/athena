# Optional ChatGPT and Codex hints

[Home](../../README.md) · [Platform-neutral stewardship](../agent-stewardship.md) · [Agent template](../../templates/AGENTS.template.md)

## Instruction discovery

Codex can discover root and directory-scoped `AGENTS.md` files, with
`AGENTS.override.md` taking precedence at a given scope. Deeper instructions
can override broader repository guidance. Keep the root entry short and link
to only the standards needed for the task. A linked document is not guaranteed
to be loaded automatically.
See [official instruction documentation](https://developers.openai.com/codex/guides/agents-md).

Other agents may use different discovery rules. In a chat interface, explicitly
provide the relevant files or attach the project profile. Do not assume settings
or file access transfer between products.

## Configuration hints

Checked against official documentation on 2026-09-13. Verify support in the
installed client before applying examples; do not silently rewrite a user's
configuration. No model name, subscription tier or price is prescribed here.

For clients supporting the documented fields, a local no-helper profile can use:

```toml
[agents]
enabled = false
```

If delegation is explicitly authorized, the documented
`agents.max_concurrent_threads_per_session` caps spawned threads, excluding the
primary. Set it to `1` for the Standard profile's one helper.
Documented defaults also include `default_subagent_model` and
`default_subagent_reasoning_effort`; choose supported values for the actual task.
See [official subagent controls](https://developers.openai.com/codex/subagents).

Model effort is configurable for supported models; available values depend on
the model/client. See the [configuration reference](https://developers.openai.com/codex/config-reference).
Prefer a narrow task and appropriate effort over a universal maximum.

## Usage stewardship

Concurrency settings are not a spending ceiling. Count parent and helper work
using exposed telemetry; do not infer weekly quota from elapsed time.
Keep the [work profile](../agent-stewardship.md#work-profiles) as the portable
policy and runner configuration as its product-specific implementation.

Use available usage indicators in ChatGPT/Codex when present. Do not assume an
API account's budgets or billing apply to a chat subscription. Do not promise
that an unavailable setting or a prompt alone can impose a hard quota.

No connector, plugin or additional account is needed for the native build path.
Use tools only when they materially help the authorized task. Store credentials
and personal overrides outside this shared standards collection.
