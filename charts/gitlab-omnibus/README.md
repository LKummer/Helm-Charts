---
title: gitlab-omnibus
description: Gitlab Omnibus deployment.
---

## Prerequisites

Add the repository to Helm:

```s
$ helm repo add homelab https://lkummer.github.io/Helm-Charts
$ helm repo update
```

## Deploy the Chart

Create a `values.yaml` file with values you wish to override.

Install the chart:

```s
$ helm install example homelab/gitlab-omnibus --file values.yaml
```

## Upgrade the Chart

Upgrade the chart:

```s
$ helm upgrade example homelab/gitlab-omnibus --file values.yaml
```

## Delete the Chart

Delete the chart:

```s
$ helm delete example
```

## Configuration

The chart offers the following list of configuration values.

| Parameter | Description
| - | - |
| `nameOverride` | Override the name of the chart. |
| `fullnameOverride` | Override the full name of the chart. |
| `image` | Gitlab Omnibus image settings. |
| `image.repository` | Image repository and name to use. |
| `image.tag` | Image version tag to use. |
| `image.pullPolicy` | Image pull policy. |
| `image.pullSecrets` | Image pull secrets. |
| `podAnnotations` | Pod annotations. |
| `podSecurityContext` | Pod security context. |
| `volumeClaims` | Options for persistent volume claims. |
| `volumeClaims.config` | Options for config folder persistent volume claims. |
| `volumeClaims.config.enabled` | Enable creation of config persistent volume claim. |
| `volumeClaims.config.name` | Config persistent volume claim name. |
| `volumeClaims.config.annotations` | Config persistent volume claim annotations. |
| `volumeClaims.config.resources` | Config persistent volume claim resource requests. |
| `volumeClaims.config.volumeMode` | Config persistent volume claim volume mode. |
| `volumeClaims.config.accessModes` | Config persistent volume claim access modes. |
| `volumeClaims.config.selector` | Config persistent volume claim selector. |
| `volumeClaims.data` | Options for data folder persistent volume claims. |
| `volumeClaims.data.enabled` | Enable creation of data persistent volume claim. |
| `volumeClaims.data.name` | Data persistent volume claim name. |
| `volumeClaims.data.annotations` | Data persistent volume claim annotations. |
| `volumeClaims.data.resources` | Data persistent volume claim resource requests. |
| `volumeClaims.data.volumeMode` | Data persistent volume claim volume mode. |
| `volumeClaims.data.accessModes` | Data persistent volume claim access modes. |
| `volumeClaims.data.selector` | Data persistent volume claim selector. |
| `securityContext` | Container security context. |
| `service` | Service related options. |
| `service.port` | Service target port. |
| `service.type` | Service type. |
| `ingress` | Ingress related options. |
| `ingress.enabled` | Enable ingress creation. |
| `ingress.hosts` | Ingress hosts. |
| `ingress.hosts.gitlab.url` | Gitlab primary hostname. |
| `ingress.hosts.pages.url` | Gitlab Pages hostname. |
| `ingress.hosts.registry.url` | Gitlab container registry hostname. |
| `ingress.annotations` | Ingress annotations. |
| `ingress.tls` | Ingress TLS options. |
| `resources` | Gitlab Omnibus resource requests and limits. |
| `nodeSelector` | Pod node selector. |
| `tolerations` | Pod tolerations. |
| `affinity` | Pod affinity. |
| `metrics` | Prometheus metrics related options. |
| `metrics.gitlab.whitelist` | Addresses to whitelist for collection. |
| `metrics.workhorse.port` | Workhorse metrics port. |
| `metrics.gitaly.port` | Gitaly metrics port. |
| `podMonitor` | Promehteus Operator PodMonitor related options. |
| `podMonitor.enabled` | Enable PodMonitor. |
| `podMonitor.labels` | PodMonitor labels. |
| `timezone` | Gitlab time zone. |