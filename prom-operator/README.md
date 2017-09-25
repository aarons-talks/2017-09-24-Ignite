# Prometheus Operator

The [Prometheus Operator](https://coreos.com/blog/the-prometheus-operator.html)
runs a [Prometheus](https://prometheus.io/) monitoring cluster in Kubernetes.

## Install Operator

First, install it:

```console
kubectl create ns prom-operator
kubectl create -n prom-operator -f manifests.yaml
```

## Install Example Application

Next, install an application for prometheus to monitor:

```console
kubectl create -n prom-operator -f example-app.yaml
```

## Tell the Operator to Monitor the App

Next, install the Custom Resource Definition to tell the operator to start
monitoring the app:


```console
kubectl create -n prom-operator -f service-monitor.yaml
```

## View the Monitoring UI

The monitoring UI is available on port `30900` of the node.
