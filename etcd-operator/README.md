# Etcd Operator

[etcd](https://coreos.com/etcd/) is a distributed key/value store that is used
as a building block by a large and growing 
[list](https://github.com/coreos/etcd/blob/master/Documentation/v2/libraries-and-tools.md) 
of cloud-native systems. 

See [here](https://coreos.com/etcd/docs/latest/demo.html) for a video demo.

This document will show how to install the 
[etcd operator](https://github.com/coreos/etcd-operator#create-and-destroy-an-etcd-cluster)
in Kubernetes. The operator is software that runs in a cluster to install, manage
and delete an etcd cluster.

## Install the Operator

Install the operator software. This is management software that will respond
to requests to create, manage and destroy etcd clusters

```console
helm install stable/etcd-operator --namespace etcd-operator --name etcd-operator --set rbac.install=true
```

Next, view the operator running, but not the etcd cluster itself:

```console
kubectl get pods -n etcd-operator
```

## Create an Etcd Cluster

Next, tell the operator to install an actual Etcd cluster:

```console
helm upgrade --set cluster.enabled=true --set rbac.install=true etcd-operator stable/etcd-operator
```

A three-node etcd cluster should start launching in the `etcd-operator` namespace.
Let's see it:

```console
kubectl get pods -n etcd-operator -w
```

Notice the following pods in the list:

- `etcd-cluster-0000`
- `etcd-cluster-0001`
- `etcd-cluster-0002`

## Scale up the etcd Cluster

Next, add more replicas to the etcd cluster:

```console
helm upgrade --set cluster.enabled=true --set cluster.size=5  --set rbac.install=true etcd-operator stable/etcd-operator
kubectl get po -n etcd-operator
```

Next, delete the etcd cluster:

```console
helm upgrade --set cluster.enabled=false --set rbac.install=true etcd-operator stable/etcd-operator
kubectl get pods -n etcd-operator -w
```

Finally, delete the operator software:

```console
helm delete --purge etcd-operator
```
