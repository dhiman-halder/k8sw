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

#### Apply updated definition and relist pods
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


## DEPLOYMENT
### Create a deployment from a yaml definition
```kubectl apply -f deployment.yaml```

### Check the rollout status of the deployment
```kubectl rollout status web-deploy```

### List deployments
```kubectl get deploy```

### Describe a deployment
```kubectl describe deploy web-deploy```

### Check the replicaset associated with the deployment
```kubectl get rs```

### List the pods managed by the replicaset & deployment
```kubectl get pods```

### Get the rollout history of a deployment
```kubectl rollout history web-deploy```

### Get the rollout history of a particular rollout of a deployment
```kubectl rollout history web-deploy --revision=1```

### Declarative way of updating deployment
#### Update the Image version of yaml definition to 1.8.1
#### Get the rollout history of the deployment
```kubectl rollout history web-deploy```
#### Verify the replicaset has changed and notice the rollout events
```kubectl describe deploy web-deploy```
#### List before and after replicaset associated with the deployment
```kubectl get rs```

### Imperative way of updating deployment
```kubectl set image deploy web-deploy nginx=nginx:1.9.1 --record```

```kubectl rollout history web-deploy```

```kubectl rollout undo deploy web-deploy```

```kubectl rollout undo deploy web-deploy --to-revision=1```


## SERVICE (WordPress with MySQL)
### View then apply all definitions within the service folder
```kubectl apply -f .```

### List the services
```kubectl get svc```

### Get the public DNS of the LoadBalancer and view on Browser, complete setup process

### Verify wordpress pod is communicating with the mysql pod

```kubectl exec -it mysql -- sh```

```mysql -u root -p```

```show databases;```

```use wordpress;```

```show tables;```

```quit```

```exit```




