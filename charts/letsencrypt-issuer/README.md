---
title: letsencrypt-issuer
description: ClusterIssuer solving Let's Encrypt DNS challenge.
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
$ helm install example homelab/letsencrypt-issuer --file values.yaml
```

## Upgrade the Chart

Upgrade the chart:

```s
$ helm upgrade example homelab/letsencrypt-issuer --file values.yaml
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
| `clusterIssuerName` | Name of the ClusterIssuer resource. |
| `acme.server` | ACME DNS01 challenge server. |
| `acme.email` | Email associated with ACME account. |
| `acme.zones` | List of DNS zones to issue certificates for. |
| `cloudflare.email` | Email of Cloudflare account. |
| `cloudflare.token` | Token for Cloudflare account. |

## Examples

Create ClusterIssuer named `letsencrypt` for `example.com` zone.

```yaml
acme:
  email: you@example.com
  zones:
    - 'example.com'

cloudflare:
  email: you@example.com
  token: yourtoken
```
