# K8s Workshop
## Pre-Requisites
aws, eksctl & kubectl tools installed and pre-configured
## General
### To create an EKS cluster
```eksctl create cluster -f cluster.yaml```
### To view the worker nodes of an EKS cluster
kubectl get nodes
### To view the cluster information
kubectl cluster-info
## PODS
### Create a pod
kubectl apply -f pod.yaml
### List the pods
kubectl get pods
### List the pods with additional info
kubectl get pods -o wide
### Get complete details of a pod
kubectl describe pod web-pod
### Get details of a pod in YAML format
kubectl get pod web-pod -o yaml
### Start a shell within a pod
kubectl exec -it web-pod -c nginx -- sh

ls
cat /etc/nginx/nginx.conf
exit

### Delete a pod
kubectl delete pod web-pod
### Imperative way of creating a pod
kubectl run web-pod  --image=nginx --restart=Never
### View logs of a pod
cat pod-random-logger.yaml
kubectl apply pod-random-logger.yaml
kubectl logs random-logger
### To tail logs
kubectl logs random-logger -f
