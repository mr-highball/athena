# Optional browser target

[Home](../../README.md) · [Native core](../fpc-builds.md) · [CGE web](cge.md#web-target)

## Language and bridge cautions

If Pascal is compiled with pas2js, ship its matched runtime. Keep application
logic in Pascal; generated JavaScript does not justify npm tooling.
Use a Pascal HTTP server and Pascal browser driver, or direct browser inspection.

If a compiler's record iteration or dynamic-array construction behaves differently,
use explicit allocation and indexed record copies. Preserve baselines with detached
candidate data. Run the same numerical and state fixtures on native and browser
targets. Avoid depending on JavaScript's exactness beyond its safe integer range.

If WASM and JavaScript exchange lengths, offsets or handles, validate signedness,
overflow and lifetime on both sides. Bulk transfer can reduce call overhead, but
prove the boundary checks and output before relying on a performance improvement.
See [state contracts](../state-and-constraints.md).

## Hosting

Serve over HTTP rather than opening files directly. Use `compileserver` from
the matched Pascal toolchain or an admitted FPC HTTP server. Test a repository
subpath as well as the root; use relative resource URLs.

If a download fails, inspect status, content type, byte length and hash. Distinguish
an HTML error response, stale manifest and genuinely slow transfer. Network
proximity, adapter quality and cache state can affect observed speed independently
of application changes. Do not publish local addresses in shared documentation.

## Runtime readiness

Readiness means the required world/app state has initialized and rendered, not
only that the host script loaded. Preserve startup errors swallowed by host APIs.
Bound download/initialization work and expose actionable failure details.

For stateful applications, test cancellation, stale-result refusal and recovery
without losing the accepted world. If context-loss or background restoration
is supported, test it separately from a fresh-page startup.

## Representative checks

Exercise the changed interaction through real controls. Capture a desktop and
narrow viewport after UI changes. Verify actual optional resources reached the
renderer, rather than accepting a placeholder or successful network request alone.

Report software rendering, viewport emulation and physical-device testing distinctly.
Use focused regression journeys; avoid rerunning every visual style or every asset
for a change to one shared control. See [validation](../validation.md) and
[agent effort](../agent-stewardship.md#usage-and-waiting).
