# Ciclo de vida de um pod

**Autor:** Fagner Geraldes  
**Data de criação:** 29/01/2026  
**Data de atualização:** 29/01/2026  
**Versão:** 0.01  

## PostStart e PreStop

```bash
k3d cluster create meucluster --servers 3 --agents 3 -p "30000:30000@loadbalancer"
kubectl apply -f 13-deployment.yaml
kubectl get pods
kubectl delete $(kubectl get pod -o name) && watch 'kubectl get po'
kubectl delete -f 13-deployment.yaml
kubectl apply -f 13-deployment2.yaml
kubectl get pods
kubectl delete -f 13-deployment2.yaml
```

## Init Container

```bash
kubectl apply -f 13-deployment3.yaml
watch 'kubectl get pods'
kubectl delete -f 13-deployment3.yaml
```

```bash
kubectl apply -f ./k8s/mongodb/mongodb-secret.yaml
kubectl apply -f ./k8s/api/api-configmap.yaml
kubectl apply -f ./k8s/mongodb/deployment4.yaml
kubectl apply -f ./k8s/api/deployment5.yaml
watch 'kubectl get all'

kubectl delete -f ./k8s/mongodb/deployment4.yaml
kubectl delete -f ./k8s/api/deployment5.yaml
kubectl delete -f ./k8s/mongodb/mongodb-secret.yaml
kubectl delete -f ./k8s/api/api-configmap.yaml
k3d cluster delete meucluster
```
