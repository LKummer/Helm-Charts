---
title: backup
description: Restic based backup and restore solution for persistent volume claims.
---

## Prerequisites

Add the repository to Helm:

```s
$ helm repo add homelab https://lkummer.github.io/Helm-Charts
$ helm repo update
```

Restic REST server or another form of storage for Restic repositories is
required.
Support for cloud providers will be added soon.

## Deploy the Chart

Create a `values.yaml` file with values you wish to override.

Install the chart:

```s
$ helm install example homelab/backup --file values.yaml
```

## Upgrade the Chart

Upgrade the chart:

```s
$ helm upgrade example homelab/backup --file values.yaml
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
| `image` | Restic image settings. |
| `image.repository` | Image repository and name to use. |
| `image.tag` | Image version tag to use. |
| `image.pullPolicy` | Image pull policy. |
| `repositories` | List of Restic repositories to use. |
| `repositories.name` | Name of the Restic repository. |
| `repositories.address` | Address of the Restic repository. |
| `repositories.password` | Password for the Restic repository. |
| `repositories.create` | Options for creating the repository. |
| `repositories.create.enabled` | Enable repository creation. |
| `repositories.create.restartPolicy` | Restart policy for repository creation job. |
| `repositories.restore` | Options for restoring from the repository. |
| `repositories.restore.enabled` | Enable restore job from the repository. |
| `repositories.restore.snapshot` | Name of the snapshot to restore from. |
| `repositories.restore.restartPolicy` | Restart policy for restore job. |
| `repositories.backup` | Options for backup cron job. |
| `repositories.backup.enabled` | Enable backup cron job. |
| `repositories.backup.schedule` | Cron schedule to run backup jobs. |
| `repositories.backup.restartPolicy` | Restart policy for backup jobs. |
| `repositories.forget` | Options for snapshot removal cron job. |
| `repositories.forget.enabled` | Enable forget cron job. |
| `repositories.forget.schedule` | Cron schedule to run forget jobs. |
| `repositories.forget.keep` | Options for keeping snapshots. |
| `repositories.forget.keep.last` | Keep last amount of snapshots. |
| `repositories.forget.keep.hourly` | Keep hourly snapshots for amount of hours. |
| `repositories.forget.keep.daily` | Keep daily snapshots for amount of days. |
| `repositories.forget.keep.weekly` | Keep weekly snapshots for amount of weeks. |
| `repositories.forget.keep.monthly` | Keep monthly snapshots for amount of months. |
| `repositories.forget.keep.yearly` | Keep yearly snapshots for amount of years. |
| `repositories.forget.keep.within` | Keep snapshots within duration. |
| `repositories.forget.restartPolicy` | Restart policy for forget jobs. |
| `volumeClaims` | Persistent volume claims to create and manage. |
| `volumeClaims.enabled` | Enable persistent volume claims creation. |
| `volumeClaims.claims` | List of persistent volume claims to manage. |
| `volumeClaims.claims.name` | Name of the persistent volume claim. |
| `volumeClaims.claims.repositoryPath` | Path to use for backups in Restic repositories. |
| `volumeClaims.claims.annotations` | Kubernetes annotations for the persistent volume claim. |
| `volumeClaims.claims.resources` | Resource requests of the persistent volume claim. |
| `volumeClaims.claims.volumeMode` | Volume mode of the persistent volume claim. |
| `volumeClaims.claims.accessModes` | Access modes of the persistent volume claim. |
| `volumeClaims.claims.selector` | Selector of the persistent volume claim. |

## Examples

Basic usage examples to get you up and running quickly.

### Starting from Scratch

Create `some-volume` persistent volume claim, create Restic repository and basic backup
and forget jobs.

```yaml
repositories:
  - name: rest
    address: rest:http://user:pass@address:8000/repo
    password: secret
    create:
      enabled: true
    backup:
      enabled: true
    forget:
      enabled: true
      keep:
        daily: 90
  
volumeClaims:
  enabled: true
  claims:
    - name: some-volume
      repositoryPath: some-volume
      resources:
        requests:
          storage: 10Gi
```

### Disaster Recovery

Restore latest `some-volume` snapshot from existing Restic repository.

```yaml
repositories:
  - name: rest
    address: rest:http://user:pass@address:8000/repo
    password: secret
    restore:
      enabled: true
    backup:
      enabled: true
      schedule: 30 8 * * *
    forget:
      enabled: true
      schedule: 30 8 * * *
      keep:
        daily: 90
  
volumeClaims:
  enabled: true
  claims:
    - name: some-volume
      repositoryPath: some-volume
      resources:
        requests:
          storage: 10Gi
```

## Quirks

During restoration, the entire repository is downloaded.
It is recommended to create separate repositories for separate namespaces to avoid
wasting traffic when restoring in multiple namespaces.
