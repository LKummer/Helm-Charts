# Lior's Helm Charts

For the uninitiated, [Helm](https://helm.sh/) is basically a templating solution for Kubernetes resource manifest.

This repository hosts Helm charts I use in my homelab.
All charts hosted here are catered for my own setup and might not be a perfect fit for everyone.
Please **do not** treat any charts as production ready.

## Usage

Make sure you have Helm installed.
This repository was built against Helm `v3.6.3`, newer and a bit older versions should work just fine.

```s
$ helm repo add homelab https://github.com/LKummer/Helm-Charts
$ helm repo update
```

Once the repository is added and updated, you are ready to install charts.
For more information on the available charts, [check out the repository's documentation](https://github.com/LKummer/Helm-Charts).
