# Prometheous Operator

The [Prometheus Operator](https://coreos.com/blog/the-prometheus-operator.html)
runs a [Prometheus](https://prometheus.io/) monitoring cluster in Kubernetes.

First, install it:

```console
kubectl create ns prom-operator
kubectl create --namespace=prom-operator -f https://coreos.com/operators/prometheus/latest/prometheus-operator.yaml
```
