# Setting up WeaveScope for visualizing Kubernetes Pods, Services, Containers & Hosts

## Pre-requisite

- Docker for Mac
- GKE Cluster 
- The ```docker context``` shows you GKE Cluster

```

kubectl create clusterrolebinding "cluster-admin-$(whoami)" --clusterrole=cluster-admin --user="$(gcloud config get-value core/account)"
```

## Installing WeaveScope

```
kubectl apply -f "https://cloud.weave.works/k8s/scope.yaml?k8s-version=$(kubectl version | base64 | tr -d '\n')"
```

This downloads a recent Scope image from Dockerhub and launches a probe onto every node as well as a single Scope app. Once launched, Scope doesn’t require any other configuration.

Allowable parameters for the launcher URL:

```
v - Weave Scope version or tag, e.g. latest current release is the default
k8s-service-type - Kubernetes service type (for running Scope in Standalone mode), can be either LoadBalancer or NodePort, by default this is unspecified (only internal access)
```

## Open Scope in Your Browser

```
kubectl port-forward -n weave "$(kubectl get -n weave pod --selector=weave-scope-component=app -o jsonpath='{.items..metadata.name}')" 4040
```

Now get ready to access via  http://localhost:4040.

![My Image](https://raw.githubusercontent.com/collabnix/dockerlabs/master/kubernetes/workshop/weave.jpg)


## Note:

If you're using Docker Desktop for Mac, follow the below steps:

```
kubectl apply -f https://github.com/weaveworks/scope/releases/download/v1.13.2/k8s-scope.yaml
kubectl port-forward -n weave "$(kubectl get -n weave pod --selector=weave-scope-component=app -o jsonpath='{.items..metadata.name}')" 4040
```

The URL is: http://localhost:4040.


[Next >>](https://collabnix.github.io/kubelabs/dockerdesktopformac/index.html)

