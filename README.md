# Fluent + 10x Helm Charts

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

> [!WARNING]
> **The Fluentd and Fluent Bit 10x charts are retired.**
>
> They used the old **image-swap** model: a fork of the official fluent chart
> whose base image was replaced with a `log10x/fluentd-10x` / `log10x/fluent-bit-10x`
> build that ran the 10x Engine **in-process, inside the forwarder container**.
>
> That model is no longer used. Fluentd and Fluent Bit now run the 10x Engine as a
> **separate `log10x/edge-10x` sidecar container** on the **official upstream**
> [`fluent/fluentd`](https://github.com/fluent/helm-charts) and
> [`fluent/fluent-bit`](https://github.com/fluent/helm-charts) Helm charts, via a
> values overlay (or a Helm post-renderer / kustomize overlay for Fluentd), talking
> over loopback TCP.
>
> **Use the current [Receiver deployment guide](https://doc.log10x.com/apps/receiver/deploy/) instead.**
>
> Filebeat remains an image swap (`log10x/filebeat-10x`) — see
> [elastic-helm-charts](https://github.com/log-10x/elastic-helm-charts) — because it
> is the one genuinely embedded forwarder.

## License

This repository is licensed under the [Apache License 2.0](LICENSE).

### Important: Log10x Product License Required

While the tooling itself is open source, **using Log10x requires a commercial license**.

| Component | License |
|-----------|---------|
| This repository (Helm charts) | Apache 2.0 (open source) |
| Log10x engine and runtime | Commercial license required |

**Get Started:**

- [Log10x Pricing](https://www.log10x.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=fluent-helm-charts&utm_content=footer)
- [Documentation](https://doc.log10x.com)
- [Contact Sales](mailto:sales@log10x.com)
