#Autor: Fagner Geraldes  
#Data de criação: 26/01/2026  
#Data de atualização: 26/01/2026  
#Versão: 0.01  

### Endpoints

```bash
k3d cluster create meucluster --servers 3 --agents 3 -p "30000:30000@loadbalancer"
kubectl apply -f 06-endpoints.yaml && watch 'kubectl get svc,po,endpoints'
kubectl describe endpoints
kubectl delete -f 06-endpoints.yaml
k3d cluster delete meucluster
```