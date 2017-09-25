# ignite2017

Code and resources for Ignite 2017 Demos. All of the demos in this repository
can be run against an Azure Kubernetes cluster created with
[acs-engine](https://github.com/Azure/acs-engine). Create one with `acs-engine`
[version 0.7.0](https://github.com/Azure/acs-engine/releases/tag/v0.7.0) 
using this command:

```console
acs-engine deploy \
    --subscription-id $SUB_ID \
    --dns-prefix ignite2017 \
    --location westus2 \
    --auto-suffix \
    --api-model acs-engine/kubernetes-config.json
```

# Simple Walkthroughs

There is one simple walk-through to demonstrate Kubernetes controllers and 
reconciliation [here](./simple-nginx).

# Operators

This repository has walk-throughs for the following operators:

- [Etcd Operator](./etcd-operator/README.md)
- [Prometheus Operator](./prom-operator/README.md)

