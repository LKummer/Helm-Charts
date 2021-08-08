---
title: debug-webserver
description: Basic Nginx webserver for debugging.
---

## Prerequisites

Add the repository to Helm:

```s
$ helm repo add https://lkummer.github.io/Helm-Charts
$ helm repo update
```

## Deploy the Chart

Create a `values.yaml` file with values you wish to override.

Install the chart:

```s
$ helm install example homelab/debug-webserver --file values.yaml
```

## Upgrade the Chart

Upgrade the chart:

```s
$ helm upgrade example homelab/debug-webserver --file values.yaml
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
| `volumeMounts` | Additional container `volumeMounts` configuration. |
| `volumes` | Additional Pod `volumes` configuration. |
| `nginxConfig` | Custom Nginx configuration. |
| `probePath` | Path for HTTP probes. |
| `nameOverride` | Override the name of the chart. |
| `fullnameOverride` | Override the full name of the chart. |
| `imagePullSecrets` | Image pull secrets. |
| `image` |Postgres image related settings.|
| `image.repository` |Repository to pull Postgres image from.|
| `image.pullPolicy` |Pull policy for Postgres image.|
| `image.tag` |Postgres image tag override.|
| `resources` |Postgres container resource limits and requests.|
| `service` |Load balancer service related options.|
| `service.port` |Port to expose Postgres on.|
| `podAnnotations` | Kubernetes annotations for the pod. |
| `podSecurityContext` | Security context of the pod. |
| `nodeSelector` | Pod node selector. |
| `tolerations` | Pod tolerations. |
| `affinity` | Pod affinity. |

## Example

Create deployment serving ConfigMap keys.

```yaml
probePath: /

volumeMounts:
  - name: pages
    mountPath: /usr/share/nginx/html
    readOnly: true

volumes:
  - name: pages
    configMap:
      name: debug-webserver-pages

ingress:
  enabled: true
  hosts:
    - host: example.com
      paths:
      - path: /
  tls:
    - secretName: debug-webserver-tls
      hosts:
        - example.com
```
