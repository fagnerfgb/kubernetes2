#Autor: Fagner Geraldes  
#Data de criação: 26/01/2026  
#Data de atualização: 26/01/2026  
#Versão: 0.01  

### Replicaset

```bash
k3d cluster create meucluster --servers 2 --agents 2
kubectl apply -f 03-replicaset.yaml && watch 'kubectl get rs,po'
kubectl port-forward $(kubectl get pod -o name) 8080:80
kubectl get 03-replicaset
kubectl describe 03-replicaset
kubectl delete $(kubectl get pod -o name) && watch 'kubectl get rs,po'
kubectl scale 03-replicaset 03-replicaset --replicas 5 && watch 'kubectl get rs,po'
kubectl apply -f 03-replicaset2.yaml && watch 'kubectl get rs,po'
kubectl describe pods | grep Image:
kubectl apply -f 03-replicaset3.yaml && watch 'kubectl get rs,po'
kubectl describe pods | grep Image:
kubectl delete pods -l app=web && watch 'kubectl get rs,po'
kubectl describe pods | grep Image:
kubectl delete -f 03-replicaset3.yaml
k3d cluster delete meucluster
```