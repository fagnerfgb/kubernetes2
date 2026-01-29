# Self Healing

**Autor:** Fagner Geraldes  
**Data de criação:** 28/01/2026  
**Data de atualização:** 28/01/2026  
**Versão:** 0.01  

## Liveness Probe

```bash
k3d cluster create meucluster --servers 3 --agents 3
kubectl apply -f ./k8s/api/api-configmap.yaml
kubectl apply -f ./k8s/mongodb/mongodb-secret.yaml
kubectl apply -f ./k8s/mongodb/deployment3.yaml
kubectl apply -f ./k8s/api/deployment-liveness.yaml
watch 'kubectl get all'

NODE_IP=$(kubectl get node k3d-meucluster-agent-0 -o wide | awk 'NR>1 {print $6}')
PORT=$(kubectl get svc api-service -o wide | awk 'NR>1 {print $5}' | cut -d':' -f2 | cut -d'/' -f1)
URL="http://${NODE_IP}:${PORT}/swagger"
echo "$URL"

watch 'kubectl get all'

kubectl delete -f ./k8s/api/deployment-liveness.yaml
```

## Readiness Probe

```bash
kubectl apply -f ./k8s/api/deployment-readiness.yaml
watch 'kubectl get all'

NODE_IP=$(kubectl get node k3d-meucluster-agent-0 -o wide | awk 'NR>1 {print $6}')
PORT=$(kubectl get svc api-service -o wide | awk 'NR>1 {print $5}' | cut -d':' -f2 | cut -d'/' -f1)
URL="http://${NODE_IP}:${PORT}/swagger"
echo "$URL"

watch 'kubectl get all'
kubectl delete -f ./k8s/api/deployment-readiness.yaml
```

## Startup Probe

```bash
kubectl apply -f ./k8s/api/deployment-startup.yaml
watch 'kubectl get all'

NODE_IP=$(kubectl get node k3d-meucluster-agent-0 -o wide | awk 'NR>1 {print $6}')
PORT=$(kubectl get svc api-service -o wide | awk 'NR>1 {print $5}' | cut -d':' -f2 | cut -d'/' -f1)
URL="http://${NODE_IP}:${PORT}/swagger"
echo "$URL"

watch 'kubectl get all'
kubectl delete -f ./k8s/api/deployment-startup.yaml
kubectl delete -f ./k8s/mongodb/deployment3.yaml
kubectl delete secret --all
kubectl delete -f ./k8s/api/api-configmap.yaml

k3d cluster delete meucluster
```
