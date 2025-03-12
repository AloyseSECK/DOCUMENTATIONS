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

## 1. Gestion des contextes et clusters
```bash
kubectl config get-contexts         # Liste les contextes disponibles
```
```bash
kubectl config use-context <nom>    # Change de contexte
```
```bash
kubectl config view                 # Affiche la configuration actuelle
```
```bash
kubectl cluster-info                # Infos sur le cluster
```
```bash
kubectl get nodes                    # Liste les nœuds du cluster
```

## 2. Gestion des namespaces
```bash
kubectl get namespaces               # Liste les namespaces
```
```bash
kubectl create namespace <nom>       # Crée un namespace
```
```bash
kubectl delete namespace <nom>       # Supprime un namespace
```

## 3. Gestion des pods
```bash
kubectl get pods -A                    # Liste tous les pods de tous les namespaces
```
```bash
kubectl get pods -n <namespace>        # Liste les pods d'un namespace
```
```bash
kubectl describe pod <nom> -n <namespace>  # Détails d'un pod
```
```bash
kubectl logs <nom-du-pod> -n <namespace>   # Affiche les logs d'un pod
```
```bash
kubectl delete pod <nom> -n <namespace>    # Supprime un pod
```
```bash
kubectl exec -it <nom-du-pod> -- /bin/sh   # Ouvre un shell dans un pod
```

## 4. Gestion des déploiements
```bash
kubectl get deployments -n <namespace>     # Liste les déploiements
```
```bash
kubectl describe deployment <nom> -n <namespace>  # Détails d'un déploiement
```
```bash
kubectl delete deployment <nom> -n <namespace>    # Supprime un déploiement
```
```bash
kubectl rollout restart deployment <nom> -n <namespace>  # Redémarre un déploiement
```

## 5. Gestion des services et ingress
```bash
kubectl get svc -n <namespace>             # Liste les services
```
```bash
kubectl describe svc <nom> -n <namespace>  # Détails d'un service
```
```bash
kubectl get ingress -n <namespace>         # Liste les ingress
```
```bash
kubectl describe ingress <nom> -n <namespace>  # Détails d'un ingress
```

## 6. Gestion des configurations et secrets
```bash
kubectl get configmap -n <namespace>        # Liste les configmaps
```
```bash
kubectl describe configmap <nom> -n <namespace>  # Détails d'une configmap
```
```bash
kubectl get secrets -n <namespace>          # Liste les secrets
```
```bash
kubectl describe secret <nom> -n <namespace>  # Détails d'un secret
```

## 7. Gestion des volumes et PV/PVC
```bash
kubectl get pv                     # Liste les Persistent Volumes
```
```bash
kubectl get pvc -n <namespace>     # Liste les Persistent Volume Claims
```

## 8. Surveillance et débogage
```bash
kubectl top nodes                  # Consommation des nœuds
```
```bash
kubectl top pods -n <namespace>    # Consommation des pods
```
```bash
kubectl get events -n <namespace>  # Liste des événements
```

## 9. Gestion des rôles et permissions
```bash
kubectl get roles -n <namespace>         # Liste les rôles
```
```bash
kubectl get rolebindings -n <namespace>  # Liste les liaisons de rôles
```
```bash
kubectl describe role <nom> -n <namespace>  # Détails d'un rôle
```

## 10. Autres commandes utiles
```bash
kubectl apply -f <fichier.yaml>         # Applique une configuration
```
```bash
kubectl delete -f <fichier.yaml>        # Supprime une ressource
```
```bash
kubectl explain <ressource>             # Détails sur une ressource
```


