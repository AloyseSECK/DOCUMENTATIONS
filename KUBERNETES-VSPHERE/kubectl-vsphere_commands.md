# Quelques commandes utiles pour gérer les ressources Kubernetes sur vSphere

## Se logger sur le cluster Kubernetes
- Sur un terminal windows
```bash
.\kubectl-vsphere.exe login --server=x.x.x.x --insecure-skip-tls-verify `
>>   --tanzu-kubernetes-cluster-namespace <namespace> `
>>   --tanzu-kubernetes-cluster-name <cluster-name> `
>>   --vsphere-username <username> `  
```
- Sur un terminal linux
```bash
kubectl-vsphere login --server=x.x.x.x --insecure-skip-tls-verify \
>>   --tanzu-kubernetes-cluster-namespace <namespace> \
>>   --tanzu-kubernetes-cluster-name <cluster-name> \
>>   --vsphere-username <username> \ 
```

## Récupérer les pods d'un namespace
```bash
kubectl get pods -n <namespace>
```

## Récupérer les services d'un namespace
```bash
kubectl get service -n <namespace>
```

