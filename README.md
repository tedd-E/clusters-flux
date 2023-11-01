# clusters-flux

This repo contains Flux config for a collection of clusters.

All clusters deploy a component bundle defined in a separate repo

* alpaca - uses Kustomization to deploy bundle in repo cluster-components-flux-kustomize
* badger - same as alpaca
* camel - uses HelmRelease to deploy bundle in repo cluster-components-flux-helm

## Usage

Dependencies: Kubernetes cluster, kubectl client, [Taskfile](https://taskfile.dev/)

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
