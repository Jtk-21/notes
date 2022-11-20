# Kubernetes

## Command Refs

##### kubectl
```
kubectl get pods
kubectl get all
kubectl get events
kubectl get deployments
kubectl get nodes
kubectl get services
kubectl get replicasets

kubectl describe <resource>

kubectl delete <resource>

--all-namespaces

kubectl rollout pause deployment <name> (can same-same with "resume")

```

##### kube logs
```
kubectl logs <pod>
kubectl logs <pod> -c <container>
kubectl logs <service name>
kubectl logs -f <pod>
kubectl logs <pod> -p (previous failed pod logs)
```
`journalctl -u kubelet`

##### Exec into kube pod/container
```
kubectl exec -it <pod> -c <container> /bin/bash
```

## kubernetes layout (in my head)
docker container/image
deployed to helm
helm builds kubernetes deployment
replicaset is generated
pod is build 
