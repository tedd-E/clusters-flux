# clusters-flux

This repo contains Flux config for a collection of clusters.

All clusters deploy a component bundle defined in a separate repo

## Usage

Dependencies:
Kubernetes cluster,
kubectl client,
[Flux CLI](https://fluxcd.io/flux/installation/#install-the-flux-cli),
[Taskfile](https://taskfile.dev/)

I recommend using a local Kubernetes cluster. Any should do, but I'm using [k3d](https://k3d.io)
to manage multiple local clusters.

You can install the [Taskfile CLI](https://taskfile.dev/installation/) using
`brew install go-task`. Alternatively, you can view the root [Taskfile.yaml](./Taskfile.yaml)
and run the commands directly.

First, install Flux:

```
$ task install
```

Then, apply the Flux config for a specific cluster. This will sync the bundle
repo with the cluster and apply the bundle to the cluster.

```
$ task camel:apply
```

There are other useful tasks to run, like deleting the Flux config or
uninstalling Flux. To see all available commands, run: `task --list-all`

## Clusters

### alpaca

Uses Kustomization to deploy bundle

Layers:
1. Kustomization "flux-system", source: clusters-flux.git
2. Kustomization "components", sources: clusters-flux.git, cluster-components-flux-kustomize.git

### badger

Similar to alpaca but with a single layer

Layers:
1. Kustomization "components", sources: clusters-flux.git, cluster-components-flux-kustomize.git

### camel

Uses HelmRelease to deploy bundle

Layers:
1. Kustomization "flux-system", source: clusters-flux.git
2. HelmRepository "components", source: cluster-components-flux-helm.git

### dingo

Similar to camel but with a single layer

Layers:
1. HelmRepository "components", source: cluster-components-flux-helm.git

## Cluster Components Bundle

Cluster components are defined in a separate bundle repo. The bundle is synced
to each cluster.

* HelmRelease-based bundle: https://github.com/merusso/cluster-components-flux-helm
* Kustomization-based bundle: https://github.com/merusso/cluster-components-flux-kustomize 
