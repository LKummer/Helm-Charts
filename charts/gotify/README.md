---
title: gotify
description: Gotify server.
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
$ helm install example homelab/gotify --file values.yaml
```

## Upgrade the Chart

Upgrade the chart:

```s
$ helm upgrade example homelab/gotify --file values.yaml
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
| `configuration` | Gotify configuration options. |
| `configuration.defaultUser` | Default Gotify admin user. |
| `configuration.defaultUser.name` | Default Gotify admin user name. |
| `configuration.defaultUser.password` | Default Gotify admin user password. |
| `configuration.additional` | Additional YAML to be appended to the Gotify configuration. |
| `volumeClaim` | PersistentVolumeClaim related options. |
| `volumeClaim.enabled` | Enable PersistentVolumeClaim resource. |
| `volumeClaim.name` | Name of the PersistentVolumeClaim resource. |
| `volumeClaim.annotations` | Kubernetes annotations for the PersistentVolumeClaim. |
| `volumeClaim.resources` | PersistentVolumeClaim resources options. |
| `volumeClaim.volumeMode` | PersistentVolumeClaim volumeMode option. |
| `volumeClaim.accessModes` | PersistentVolumeClaim accessModes option. |
| `volumeClaim.selector` | PersistentVolumeClaim selector option. |
| `ingress` | Ingress related options. |
| `ingress.enabled` | Enable ingress resource. |
| `ingress.annotations` | Kubernetes annotations for the ingress. |
| `ingress.hosts` | Ingress hosts configuration. |
| `ingress.tls` | Ingress TLS configuration. |
| `nameOverride` | Override the name of the chart. |
| `fullnameOverride` | Override the full name of the chart. |
| `imagePullSecrets` | Image pull secrets. |
| `image` |Gotify image related settings.|
| `image.repository` |Repository to pull Gotify image from.|
| `image.pullPolicy` |Pull policy for Gotify image.|
| `image.tag` |Gotify image tag override.|
| `resources` |Gotify container resource limits and requests.|
| `service` |Load balancer service related options.|
| `service.port` |Port to use for Gotify Service resource.|
| `podAnnotations` | Kubernetes annotations for the pod. |
| `podSecurityContext` | Security context of the pod. |
| `nodeSelector` | Pod node selector. |
| `tolerations` | Pod tolerations. |
| `affinity` | Pod affinity. |

## Example

Install Gotify and configure TLS.

```yaml
configuration:
  defaultUser:
    name: admin
    password: supersecret

ingress:
  enabled: true
  hosts: 
    - paths:
      - host: gotify.example.com
        path: /
        pathType: Prefix
  tls:
    - secretName: gotify-tls
      hosts:
        - gotify.example.com
```
