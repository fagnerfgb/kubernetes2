# Labels

**Autor:** Fagner Geraldes  
**Data de criação:** 26/01/2026  
**Data de atualização:** 26/01/2026  
**Versão:** 0.01  

```bash
k3d cluster create meucluster --servers 2 --agents 2
kubectl apply -f 02-labels.yaml && watch 'kubectl get pods'
kubectl describe pod/meupodazul | grep Labels: -A 2
kubectl describe pod/meupodverde | grep Labels:  -A 2
kubectl get pods -l versao=azul
kubectl get pods -l versao=verde
kubectl get pods -l app=nginx
kubectl delete pods -l app=nginx
k3d cluster delete meucluster
```
