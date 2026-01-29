#Autor: Fagner Geraldes  
#Data de criação: 28/01/2026  
#Data de atualização: 28/01/2026  
#Versão: 0.01  

### ConfigMap por referencia

```bash
k3d cluster create meucluster --servers 3 --agents 3
kubectl apply -f ./k8s/mongodb/mongodb-configmap.yaml
kubectl get configmap
kubectl describe configmap mongodb-configmap
kubectl apply -f ./k8s/mongodb/deployment2.yaml
kubectl apply -f ./k8s/api/deployment.yaml
watch 'kubectl get all'

NODE_IP=$(kubectl get node k3d-meucluster-agent-0 -o wide | awk 'NR>1 {print $6}')
PORT=$(kubectl get svc api-service -o wide | awk 'NR>1 {print $5}' | cut -d':' -f2 | cut -d'/' -f1)
URL="http://${NODE_IP}:${PORT}/swagger"
echo "$URL"


kubectl delete -f ./k8s/mongodb/deployment2.yaml
kubectl delete -f ./k8s/api/deployment.yaml
```

### ConfigMap por referencia e por valor

```bash
kubectl apply -f ./k8s/api/api-configmap.yaml
kubectl get configmap
kubectl describe configmap api-configmap
kubectl apply -f ./k8s/mongodb/deployment2.yaml
kubectl apply -f ./k8s/api/deployment2.yaml
watch 'kubectl get all'

NODE_IP=$(kubectl get node k3d-meucluster-agent-0 -o wide | awk 'NR>1 {print $6}')
PORT=$(kubectl get svc api-service -o wide | awk 'NR>1 {print $5}' | cut -d':' -f2 | cut -d'/' -f1)
URL="http://${NODE_IP}:${PORT}/swagger"
echo "$URL"

kubectl delete -f ./k8s/mongodb/deployment2.yaml
kubectl delete -f ./k8s/api/deployment2.yaml
kubectl delete -f ./k8s/api/api-configmap.yaml
```

### Secret

```bash
echo -n "mongouser" | base64
echo -n "mongopwd" | base64
kubectl apply -f ./k8s/mongodb/mongodb-secret.yaml
kubectl get secrets
kubectl describe secret mongodb-secret
kubectl apply -f ./k8s/api/api-configmap.yaml
kubectl apply -f ./k8s/mongodb/deployment3.yaml
kubectl apply -f ./k8s/api/deployment3.yaml
watch 'kubectl get all'

NODE_IP=$(kubectl get node k3d-meucluster-agent-0 -o wide | awk 'NR>1 {print $6}')
PORT=$(kubectl get svc api-service -o wide | awk 'NR>1 {print $5}' | cut -d':' -f2 | cut -d'/' -f1)
URL="http://${NODE_IP}:${PORT}/swagger"
echo "$URL"

kubectl delete -f ./k8s/mongodb/deployment3.yaml
kubectl delete -f ./k8s/api/deployment3.yaml
kubectl delete -f ./k8s/mongodb/mongodb-secret.yaml
kubectl delete -f ./k8s/api/api-configmap.yaml
```

### Linha de comando

```bash
kubectl create configmap literal-configmap --from-literal=Mongo_Host=mongo-service
kubectl get configmap
kubectl describe configmap literal-configmap

kubectl create configmap file-configmap --from-file=prometheus.yaml
kubectl get configmap
kubectl describe configmap file-configmap

kubectl create secret generic literal-secret --from-literal=Mongo_PWD=mongopwd
kubectl get secret
kubectl describe secret literal-secret

kubectl create secret generic file-secret --from-file=password.txt
kubectl get secret
kubectl describe secret file-secret

kubectl delete configmap literal-configmap
kubectl delete configmap file-configmap
kubectl delete secret --all

k3d cluster delete meucluster
```