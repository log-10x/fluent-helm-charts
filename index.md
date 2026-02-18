# 10x + Fluent Helm Charts

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Release Status](https://github.com/log-10x/fluent-helm-charts/actions/workflows/release.yaml/badge.svg?branch=main)](https://github.com/log-10x/fluent-helm-charts/actions)

## Add the 10x + Fluent Helm repository

```sh
helm repo add log10x-fluent https://log-10x.github.io/fluent-helm-charts
```

You can then run `helm search repo log10x-fluent` to see the charts.

## Install Fluent-Bit + 10x observability engine

```sh
helm upgrade -i fluent-bit log10x-fluent/fluent-bit
```

For more details on installing Fluent-Bit + 10x observability engine, please see the [chart's README](https://github.com/log-10x/fluent-helm-charts/tree/main/charts/fluent-bit).

## Install Fluentd + 10x observability engine

```sh
helm upgrade -i fluentd log10x-fluent/fluentd
```

For more details on installing Fluentd + 10x observability engine, please see the [chart's README](https://github.com/log-10x/fluent-helm-charts/tree/main/charts/fluentd).

## License

[Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0)
