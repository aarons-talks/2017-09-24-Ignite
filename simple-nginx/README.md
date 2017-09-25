# Simple Nginx Installation

This document has instructions for installing Nginx and showing how the
built-in Kubernetes control loops work to provide declarative installation,
management and deletion semantics.

## Install

A Kubernetes [pod](https://kubernetes.io/docs/concepts/workloads/pods/pod/) is
the smallest unit of deployment and management in the system.

We'll install a 
[deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
to manage nginx pods. The deployment is the way that we tell Kubernetes 
controllers to manage these pods.

First, run the installation:

```console
kubectl create ns simple-nginx
kubectl create -f deployment.yaml -n simple-nginx
```

## View

Next, observe the nginx pods launching asynchronously:

```console
kubectl get pods -n simple-nginx -w
```

## Scale

This installation created a deployment that then told Kubernetes to install
two nginx pods. Let's scale up the number of pods:

```console
kubectl apply -n simple-nginx -f deployment-scaled.yaml
```

This time, when we view the nginx pods, there should be 10:

```console
kubectl get pods -n simple-nginx -w
```

## Clean up

Finally, let's delete the `simple-nginx` namespace and let the Kubernetes
namespace controller delete the deployment and all of its child resources
(pods, etc...):

```console
kubectl delete namespace simple-nginx
```

Then, watch the pods shut down:

```console
kubectl get pods -n simple-nginx -w
```

Finally, observe that the namespace is gone:

```console
kubectl get namespaces
```
