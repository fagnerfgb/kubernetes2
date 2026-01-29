#Autor: Fagner Geraldes  
#Data de criação: 26/01/2026  
#Data de atualização: 26/01/2026  
#Versão: 0.01  

### Pod

```bash
k3d cluster create meucluster --servers 2 --agents 2
kubectl api-resources | grep Pod
kubectl apply -f 01-pod.yaml && watch 'kubectl get pods'
kubectl describe pod
kubectl port-forward $(kubectl get pod -o name) 8080:80
kubectl delete pod meupod
kubectl get po
k3d cluster delete meucluster
```