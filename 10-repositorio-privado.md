# Utilizando repositório privado no Kubernetes

**Autor:** Fagner Geraldes  
**Data de criação:** 28/01/2026  
**Data de atualização:** 28/01/2026  
**Versão:** 0.01  

```bash
k3d cluster create meucluster --servers 3 --agents 3

docker tag fagnerfgb/web-color:blue fagnerfgb/web-color-priv:blue
docker push fagnerfgb/web-color-priv:blue

kubectl create secret generic docker-auth --from-file=.dockerconfigjson=/home/fagner/.docker/config.json
kubectl get secret
kubectl get secret docker-auth -o yaml

kubectl apply -f 10-privado.yaml
watch 'kubectl get all'

NODE_IP=$(kubectl get node k3d-meucluster-agent-0 -o wide | awk 'NR>1 {print $6}')
PORT=$(kubectl get svc web -o wide | awk 'NR>1 {print $5}' | cut -d':' -f2 | cut -d'/' -f1)
URL="http://${NODE_IP}:${PORT}/"
echo "$URL"

kubectl delete -f 10-privado.yaml
kubectl delete secret --all
k3d cluster delete meucluster
```
