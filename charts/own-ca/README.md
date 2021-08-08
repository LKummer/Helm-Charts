---
title: own-ca
description: Cert Manager resources for own CA cluster issuer.
---

## Prerequisites

cert-manager has to be installed on the cluster.

```s
$ helm repo add jetstack https://charts.jetstack.io
$ helm repo update
$ helm install cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version v1.4.0 --set installCRDs=true
```

Including it as a dependency in the chart causes issues with custom resource definitions.


Add the repository to Helm:

```s
$ helm repo add homelab https://lkummer.github.io/Helm-Charts
$ helm repo update
```

## Deploy the Chart

Create a `values.yaml` file with values you wish to override.

Install the chart:

```s
$ helm install example homelab/own-ca --file values.yaml
```

## Upgrade the Chart

Upgrade the chart:

```s
$ helm upgrade example homelab/own-ca --file values.yaml
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
| `ca` | Options for own certificate authority certificate. |
| `ca.commonName` | CA certificate common name. |
| `ca.subject` | CA certificate subject, [see cert-manager documentation](https://cert-manager.io/docs/reference/api-docs/#cert-manager.io/v1.X509Subject). |
| `ca.duration` | CA certificate duration. |
| `ca.renewBefore` | Time before expiration to renew. |
| `clusterIssuer` | Options for own certificate authority cluster issuer. |
| `clusterIssuer.nameOverride` | Override the name of the cluster issuer. |

## Example

Create `own-ca` cluster issuer and self signed CA certificate.

```yaml
ca:
  commonName: Homelab Root CA
  subject:
    countries:
      - IL
    organizations:
      - Homelab
  duration: 8760h # 1 year.
  renewBefore: 360h # 15 days.

clusterIssuer:
  nameOverride: own-ca
```
