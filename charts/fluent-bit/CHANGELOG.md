# Fluent Bit 10x Helm Chart Changelog

> [!NOTE]
> All notable changes to this project will be documented in this file; the format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

<!--
### Added - For new features.
### Changed - For changes in existing functionality.
### Deprecated - For soon-to-be removed features.
### Removed - For now removed features.
### Fixed - For any bug fixes.
### Security - In case of vulnerabilities.
-->

## [UNRELEASED]

## [v1.0.17] - 2026-05-02

### Changed

- Bumped engine appVersion to 1.0.17. Engine 1.0.17 ships the Reducer→Receiver app rename: bundled modules now contain `apps/receiver/` (with `apps/reducer/` removed), and chart-side launch args emit `@apps/receiver` instead of `@apps/reducer`. Plus the modules#34 logstash JS expression fix and modules#33 fluentd `tenx-optimize-unix.conf` launch-arg fix that engine 1.0.16 was missing.
- Chart prose + values comments updated to reference "Receiver" instead of "Reducer". Engine identifiers (`reducerOptimize`, `reducerReadOnly`) and the Prometheus label `tenx_app="reducer"` are unchanged — no metric churn.

## [v1.0.16] - 2026-05-02

### Changed

- Bumped engine appVersion to 1.0.16. First chart release with the `apps/receiver` launch path (paired with the corresponding modules + config rename).

## [v1.0.13] - 2026-04-29

### Added

- New `tenx.readOnly` value (default `false`) — non-intervening reporter mode. When `true`, the embedded 10x sub-process reads, aggregates, and publishes `TenXSummary` metrics to the Log10x backend, but does **not** write events back to Fluent Bit. Events continue through the original Fluent Bit pipeline to the configured outputs unchanged. Replaces the prior `@apps/reporter` pairing for non-Fluent-Bit-DaemonSet integrations.
- `tenx-report.conf` filter entry under `tenx.configFiles` — mode-specific Lua filter (`tenx-report.lua`) used when `tenx.readOnly: true`. Launches the 10x sub-process with `reducerReadOnly true` and sets `filterNonProcessed = false` so events flow through Fluent Bit unmodified.
- Mutual-exclusion guard between `tenx.readOnly` and `tenx.optimize` in a dedicated `templates/tenx-validate.yaml` — fires on every `helm install`/`upgrade`, including when the user supplies `existingConfigMap` and bypasses the rendered ConfigMap.

### Changed

- ConfigMap (`templates/configmap.yaml`) now selects between three Lua filter variants (`tenx-regulate.conf` / `tenx-optimize.conf` / `tenx-report.conf`) based on `tenx.readOnly` and `tenx.optimize`. The Unix-socket return input (`tenx-readback.conf`) is **skipped** in read-only mode — there is no return loop to wire up.

### Fixed

- `templates/_pod.tpl` image-tag composition no longer applies a hardcoded jit fallback to `tenx.variant`. The default still ships in `values.yaml` (variant: jit), but explicit empty-string overrides are now respected — required for image tags that do not carry a jit or native suffix.

## [v1.0.12] - 2026-04-28

### Changed

- Upgraded 10x engine to appVersion 1.0.12 — completes the streamer→retriever rename inside the engine. Pipeline app paths emitted at runtime now resolve to `@apps/retriever/*` (previously `@apps/streamer/*` against engine-bundled stale modules), and the forward-output Fluentd tag for retriever stream events is now `tenx-cloud-retriever` (previously `tenx-cloud-streamer`).

## [v1.0.9] - 2026-04-28

### Changed

- Upgraded 10x engine to appVersion 1.0.9

## [v1.0.8] - 2026-04-25

### Changed

- Renamed regulator to reducer (cosmetic) — `regulatorOptimize` env → `reducerOptimize`. Pipeline action verb `regulate` and config filenames preserved. Companion to log-10x/modules#21 and log-10x/config#20.

## [v1.0.7] - 2026-04-22

### Changed

- Upgraded 10x engine to appVersion 1.0.7

### Removed

- Removed `tenx.kind` option (report/regulate/optimize) — chart is now hardcoded to reducer mode
- Removed reporter and optimizer Lua scripts and config entries — use reducer with `tenx.optimize=true` for optimization

### Added

- Added `tenx.optimize` flag (default `false`) to enable optimization mode (lossless event compaction)

## [v1.0.6] - 2026-03-25

### Changed

- Upgraded 10x engine to appVersion 1.0.6

## [v1.0.5] - 2026-03-22

### Changed

- Upgraded 10x engine to appVersion 1.0.5

## [v1.0.0] - 2026-03-22

### Changed

- Upgraded 10x engine to appVersion 1.0.0

## [v0.9.7] - 2026-03-10

### Changed

- Added custom configuration option via volume mount
- Switched github config fetcher to git agnostic one

## [v0.9.5] - 2026-03-05

### Changed

- Upgraded 10x engine to appVersion 0.9.5.
- Switch 10x images from GHCR to Docker Hub

## [v0.9.0] - 2026-02-06

### Changed

- Added 10x Observability engine integration to fluent-bit.
- Added fluent keyword to chart metadata.
- Updated container image to use Log10x fluent-bit-10x image.
- Added 10x configuration options (report, regulate, optimize modes).
- Added GitHub config fetcher init container for fetching config and symbols.
- Updated maintainers and sources to Log10x.

<!--
RELEASE LINKS
-->
[UNRELEASED]: https://github.com/log-10x/fluent-helm-charts/tree/main/charts/fluent-bit
[v0.9.7]: https://github.com/log-10x/fluent-helm-charts/releases/tag/fluent-bit-0.9.7
[v0.9.5]: https://github.com/log-10x/fluent-helm-charts/releases/tag/fluent-bit-0.9.5
[v0.9.0]: https://github.com/log-10x/fluent-helm-charts/releases/tag/fluent-bit-0.9.0
[v0.2.1]: https://github.com/log-10x/fluent-helm-charts/releases/tag/fluent-bit-0.2.1
