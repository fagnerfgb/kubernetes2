# Deployment

**Autor:** Fagner Geraldes  
**Data de criação:** 26/01/2026  
**Data de atualização:** 26/01/2026  
**Versão:** 0.01  

```bash
k3d cluster create meucluster --servers 2 --agents 2
kubectl apply -f 04-deployment.yaml && watch 'kubectl get deploy,rs,po'
kubectl describe pods | grep Image:
kubectl apply -f 04-deployment.yaml && watch 'kubectl get deploy,rs,po'
kubectl describe pods | grep Image:
kubectl describe deployment
kubectl get rs
kubectl rollout history deployment deployment
kubectl rollout undo deployment deployment && watch 'kubectl get deploy,rs,po'
kubectl describe pods | grep Image:
kubectl set image deployment deployment web=kubedevio/web-color:green && watch 'kubectl get deploy,rs,po'
kubectl describe pods | grep Image:
k3d cluster delete meucluster
```
