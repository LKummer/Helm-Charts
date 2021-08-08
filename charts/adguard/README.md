---
title: adguard
description: Adguard Home DNS server.
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
$ helm install example homelab/adguard --file values.yaml
```

## Upgrade the Chart

Upgrade the chart:

```s
$ helm upgrade example homelab/adguard --file values.yaml
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
| `adguard` | Options regarding Adguard Home container. |
| `adguard.repository` | Adguard image repository and name. |
| `adguard.tag` | Adguard image tag. |
| `adguard.pullPolicy` | Adguard image pull policy. |
| `adguard.securityContext` | Adguard container security policy. |
| `adguard.resources` | Adguard container resource requests and limits. |
| `adguard.config` | Adguard configuration options. |
| `adguard.config.users` | List of web interface users. |
| `adguard.config.users.name` | Name of the user. |
| `adguard.config.users.password` | Password of the user. |
| `adguard.config.upstream_dns` | List of upstream DNS servers. |
| `adguard.config.rewrites` | List domain rewrites. |
| `adguard.config.rewrites.domain` | Domain to rewrite. |
| `adguard.config.rewrites.answer` | Address to rewrite to. |
| `adguard.config.user_rules` | List of user rules, [see Adguard documentation](https://github.com/AdguardTeam/AdGuardHome/wiki/Hosts-Blocklists). |
| `prometheusExporter` | Options regarding Prometheus exporter sidecar. |
| `prometheusExporter.enabled` | Enables Prometheus exporter sidecar. |
| `prometheusExporter.image` | Options regarding Prometheus exporter image. |
| `prometheusExporter.image.repository` | Prometheus exporter image repository and name. |
| `prometheusExporter.image.tag` | Prometheus exporter image tag. |
| `prometheusExporter.image.pullPolicy` | Prometheus exporter image pull policy. |
| `prometheusExporter.securityContext` | Prometheus exporter container security policy. |
| `prometheusExporter.resources` | Promehteus exporter resource requests and limits. |
| `prometheusExporter.config` | Prometheus exporter configuration options. |
| `prometheusExporter.config.port` | Prometheus exporter port. |
| `prometheusExporter.config.interval` | Prometheus exporter polling interval. |
| `prometheusExporter.config.log_limit` | Prometheus exporter log limit. |
| `podMonitor` | Promehteus Operator PodMonitor related options. |
| `podMonitor.enabled` | Enable PodMonitor. |
| `podMonitor.labels` | PodMonitor labels. |
| `imagePullSecrets` | Image pull secrets. |
| `podAnnotations` | Kubernetes annotations for the pod. |
| `podSecurityContext` | Security context of the pod. |
| `ingress` | Options for ingress resource. |
| `ingress.enabled` | Enable ingress creation. |
| `ingress.annotations` | Kubernetes annotations for the ingress. |
| `ingress.hosts` | Lists of hosts for the ingress. |
| `ingress.hosts.host` | Hostname. |
| `ingress.tls` | Ingress TLS options. |
| `nodeSelector` | Pod node selector. |
| `tolerations` | Pod tolerations. | 
| `affinity` | Pod affinity. | 

## Example

Create DNS server with admin user, private rewrite and ingress.

```yaml
adguard:
  config:
    users:
      - name: admin
        password: verysecret
    rewrites:
      - domain: '*.example.com'
        answer: '192.168.0.100'

ingress:
  enabled: true
  hosts:
    - host: dns.example.com
```
