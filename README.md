# K8s Workshop
## Pre-Requisites
aws, eksctl & kubectl tools installed and pre-configured
## General
### To create an EKS cluster
```eksctl create cluster -f cluster.yaml```
### To list the worker nodes of an EKS cluster
```kubectl get nodes```
### To view the cluster information
```kubectl cluster-info```
## PODS
### Create a pod from a yaml definition
```kubectl apply -f pod.yaml```
### List the pods
```kubectl get pods```
### List the pods with additional info
```kubectl get pods -o wide```
### Get complete details of a pod
```kubectl describe pod web-pod```
### Get details of a pod in YAML format
```kubectl get pod web-pod -o yaml```
### Start a shell within the container of a pod
```kubectl exec -it web-pod -c nginx -- sh```

```ls```

```cat /etc/nginx/nginx.conf```

```exit```


### Delete a pod
```kubectl delete pod web-pod```
### Imperative way of creating a pod
```kubectl run web-pod  --image=nginx --restart=Never```
### View logs of a pod
```cat pod-random-logger.yaml```

```kubectl apply pod-random-logger.yaml```

```kubectl logs random-logger```

### To tail live logs
```kubectl logs random-logger -f```

## REPLICASETS
### Create a replicaset from a yaml definition
```kubectl apply -f replicaset.yaml```

### List the replicasets
```kubectl get rs```
or
```kubectl get replicasets```
### Get complete details of a replicaset
```kubectl describe rs web-rs```
### Get the pods managed by the replicaset
```kubectl get pods -o wide```
### To verify the autoheal capability of a rs
```kubectl delete pod <podname>```

```kubectl get pods```

```kubectl describe rs web-rs```

### Declarative way of scaling a replicaset
Edit replicaset.yaml and update the replica count to 5

#### Apply updated definition
```kubectl apply -f replicaset.yaml```

```kubectl get pods```

### Imperative way of scaling a replicaset

```kubectl scale rs web-rs —replicas=2```

```kubectl get pods```

### Edit a live replicaset
```kubectl edit rs web-rs```

```kubectl get pods```

### Delete replicaset
```kubectl delete rs web-rs```
