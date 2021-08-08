---
title: tfstate-postgres
description: Posgres deployment for use as Terraform state backend.
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
$ helm install example homelab/tfstate-postgres --file values.yaml
```

## Upgrade the Chart

Upgrade the chart:

```s
$ helm upgrade example homelab/tfstate-postgres --file values.yaml
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
| `imagePullSecrets` | Image pull secrets. |
| `image` |Postgres image related settings.|
| `image.repository` |Repository to pull Postgres image from.|
| `image.pullPolicy` |Pull policy for Postgres image.|
| `image.tag` |Postgres image tag override.|
| `user` |Postgres user related options.|
| `user.user` |Username of the Postgres user.|
| `user.password` |Password of the Postgres user.|
| `resources` |Postgres container resource limits and requests.|
| `service` |Load balancer service related options.|
| `service.port` |Port to expose Postgres on.|
| `podAnnotations` | Kubernetes annotations for the pod. |
| `pvcAnnotations` | Kubernetes annotations for the PVC template. |
| `podSecurityContext` | Security context of the pod. |
| `nodeSelector` | Pod node selector. |
| `tolerations` | Pod tolerations. |
| `affinity` | Pod affinity. |

## Example

Create basic Postgres deployment.

```yaml
user:
  user: yourname
  password: yourpassword

resources:
  limits:
    cpu: 200m
    memory: 1Gi
  requests:
    cpu: 100m
    memory: 500Mi
```

Note `sslmode` should be disabled in Terraform to connect to Postgres.
For this example, Terraform is to be configured the following way:

```tf
terraform {
  backend "pg" {
    conn_str = "host=<kubernetes-host> port=5432 user=yourname password=yourpassword dbname=yourname sslmode=disable"
  }
}
```
