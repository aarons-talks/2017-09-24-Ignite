# Prometheus Operator

The [Prometheus Operator](https://coreos.com/blog/the-prometheus-operator.html)
runs a [Prometheus](https://prometheus.io/) monitoring cluster in Kubernetes.

## Install Operator

First, install it:

```console
kubectl create ns prom-operator
kubectl create -n prom-operator -f manifests.yaml
```

And verify that it's running:

```console
kubectl get pods -n prom-operator
```

## Install Example Application

Next, install an application for prometheus to monitor:

```console
kubectl create -n prom-operator -f example-app.yaml
```

## Tell the Operator About the App

Next, install the Custom Resource Definition to tell the operator that your app
exists:


```console
kubectl create -n prom-operator -f service-monitor.yaml
```

## Tell the Operator to Monitor the App

Next, tell the operator to monitor the app:

```console
kubectl create -n prom-operator -f prom.yaml
```

## Create a Service for the Monitoring UI

Next, create a Kubernetes service for viewing the Prometheus monitoring UI:

```console
kubectl create -n prom-operator -f svc.yaml
```

## View the Monitoring UI

The monitoring UI is available on port `30900` of the service's load balancer.

## Clean Up

When we're done with everything, we can simply delete the namespace:

```console
kubectl delete ns prom-operator
```
