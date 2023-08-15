# Monitoring

[Prometheus Opertator](https://github.com/prometheus-operator/prometheus-operator) which is the common solution on Kubernetes, it also support _`Thonas`_, there are a lot of articles to show how to use it, easy to understand the whole stack.

## Prerequisites of running it locally

- Kubernetes or KinD for local testing.
- Have selected prometheus stack manifests version for example:

  ```yaml
    apiVersion: kustomize.config.k8s.io/v1beta1
    kind: Kustomization

    namespace: monitoring

    resources:
    - ./namespace.yaml

    helmCharts:
    - name: kube-prometheus-stack
        includeCRDs: true
        releaseName: kube-prometheus-stack
        version: 46.8.0
        valuesFile: values.yaml
        repo: https://prometheus-community.github.io/helm-charts

  ```

- ArogCD which is very famous GitOps tools to manage Kubernetes deploy. (optional)

## Prometheus operator work on alibaba cloud.

- Work with `SLS` metric store [HA, Cloud native Prometheus solutions and practies](https://developer.aliyun.com/article/765358).

- `Arms Prometheus` which work out of box on Ack.

## Observability Methods

USE: the strategies provided by USE, we can quickly locate common performance problems.

- Utilization
  - Resource usage, usually expressed as a percentage of a time period, for example, the average memory usage in the last minute is 90%. High usage is often a sign of a system performance bottleneck.
- Saturation

  - The degree of overloading of resources, tasks that cannot get resources are usually put into the queue, so the queue length or queuing time can be used to measure.

- Errors
  - The number of error events, which is of particular concern when errors persist and cause performance degradation.

RED: clearly perceive the health of microservice applications and help measure end-user experience issues.

- (Request) Rate

  - The number of requests processed per second.

- (Request) Errors

  - The number of failed requests per second.

- (Request) Duration
  - Distribution of request processing times.

## Issues

A solved solution steps for apply the helm chart from ArgoCD:

- Apply without _`replace`_ sync options.

- Select _`replace`_ sync option if a sync problem occurred like this:

  - _"one or more objects failed to apply, reason: CustomResourceDefinition.apiextensions.k8s.io "prometheuses.monitoring.coreos.com" is invalid: metadata.annotations: Too long: must have at most 262144 bytes"_

- Apply without _`replace`_ sync option again.

Problem:

- [Github issue](https://github.com/prometheus-community/helm-charts/issues/1500)

- One or more objects failed to apply, reason: CustomResourceDefinition.apiextensions.k8s.io "prometheuses.monitoring.coreos.com" is invalid: metadata.annotations: Too long: must have at most 262144 bytes

Solution:

- Find the CRM and have to then do a manual sync and checkmark "replace".
  <https://github.com/argoproj/argo-cd/issues/820#issuecomment-838544049>

## Others

- [Kubernetes application publishing and monitoring linkage](https://developer.aliyun.com/article/715849)
- [Prometheus Operator Design](https://prometheus-operator.dev/docs/operator/design/)
- [Prometheus Operator Concept](https://github.com/prometheus-operator/prometheus-operator)
