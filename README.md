prometheus-federator
========

Prometheus Federator is an operator (powered by [`rancher/helm-project-operator`](https://github.com/rancher/helm-project-operator) and [`rancher/charts-build-scripts](https://github.com/rancher/charts-build-scripts)) that manages deploying one or more Project Monitoring Stacks composed of the following set of resources that are scoped to project namespaces:
- [Prometheus](https://prometheus.io/) (managed externally by [Prometheus Operator](https://github.com/prometheus-operator/prometheus-operator))
- [Alertmanager](https://prometheus.io/docs/alerting/latest/alertmanager/) (managed externally by [Prometheus Operator](https://github.com/prometheus-operator/prometheus-operator))
- [Grafana](https://github.com/helm/charts/tree/master/stable/grafana) (deployed via an embedded Helm chart)
- Default PrometheusRules and Grafana dashboards based on the collection of community-curated resources from [kube-prometheus](https://github.com/prometheus-operator/kube-prometheus/)
- Default ServiceMonitors that watch the deployed Prometheus, Grafana, and Alertmanager

A user can specify that they would like to deploy a Project Monitoring Stack by creating a `ProjectHelmChart` CR in a Project Registration Namespace (`cattle-project-<id>`) with `spec.helmApiVersion: monitoring.cattle.io/v1alpha1`, which will deploy the Project Monitoring Stack in a Project Release Namespace (`cattle-project-<id>-monitoring`). 

> Note: Since this Project Monitoring Stack deploys Prometheus Operator CRs, an existing Prometheus Operator instance must already be deployed in the cluster for Prometheus Federator to successfully be able to deploy Project Monitoring Stacks. It is recommended to use [`rancher-monitoring`](https://rancher.com/docs/rancher/v2.6/en/monitoring-alerting/) for this. For more information on how the chart works or advanced configurations, please read the [`README.md` on the chart](packages/prometheus-federator/README.md).

For more information on ProjectHelmCharts and how to configure the underlying operator, please read the [`README.md` on the chart](packages/prometheus-federator/README.md) or check out the general docs on Helm Project Operators in [`rancher/helm-project-operator`](https://github.com/rancher/helm-project-operator).

For more information on how to configure the underlying Project Monitoring Stack, please read the [`README.md` of the underlying chart](packages/rancher-project-monitoring/README.md) (`rancher-project-monitoring`).


## Getting Started

For more information, see the [Getting Started guide](docs/gettingstarted.md).

## Developing

### Which branch do I make changes on?

Prometheus Federator is built and released off the contents of the `main` branch. To make a contribution, open up a PR to the `main` branch.

For more information, see the [Developing guide](docs/developing.md).

## Building

`make`

## Running

`./bin/prometheus-federator`

## License
Copyright (c) 2020 [Rancher Labs, Inc.](http://rancher.com)

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
