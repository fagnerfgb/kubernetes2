# Namespaces

**Autor:** Fagner Geraldes  
**Data de criação:** 27/01/2026  
**Data de atualização:** 27/01/2026  
**Versão:** 0.01  

```bash
k3d cluster create meucluster --servers 3 --agents 3
kubectl get namespaces
kubectl apply -f 07-deploy.yaml && watch 'kubectl get deploy,po'
kubectl port-forward $(kubectl get pod -o name -l app=blue) 8080:80
kubectl port-forward $(kubectl get pod -o name -l app=green) 8181:80
kubectl delete -f 07-deploy.yaml
```

```bash
kubectl create namespace blue
kubectl create namespace green
kubectl get namespaces
kubectl apply -f 07-deploy-blue.yaml -n blue && watch 'kubectl get deploy,po -n blue'
kubectl apply -f 07-deploy-green.yaml -n green && watch 'kubectl get deploy,po -n green'
kubectl delete -f 07-deploy-blue.yaml -n blue
kubectl delete -f 07-deploy-green.yaml -n green
```

```bash
kubectl apply -f 07-deploy2.yaml
watch 'kubectl get deploy,po -n blue'
kubectl get deploy,po -n blue
watch 'kubectl get deploy,po -n green'
watch 'kubectl get deploy,po --all-namespaces'
kubectl apply -f 07-service.yaml -n blue
kubectl apply -f 07-service.yaml -n green
kubectl get service -o wide --all-namespaces
kubectl get nodes -o wide
#pegar o numero da porta de cada svc e testar no navegador
kubectl get pod --all-namespaces -o wide
kubectl run -it --image kubedevio/ubuntu-curl ping-test2 --restart=Never --rm -- /bin/bash
```

```bash
curl http://10.42.2.5
curl http://10.42.6.3
curl http://web-service.blue.svc.cluster.local
curl http://web-service.green.svc.cluster.local
```

```bash
kubectl apply -f 07-service-blue.yaml
kubectl apply -f 07-service-green.yaml
```

```bash
curl http://blue
curl http://green
exit
```

```bash
kubectl delete -f 07-service-blue.yaml
kubectl delete -f###  07-service-green.yaml
kubectl delete -f 07-service.yaml -n blue
kubectl delete -f 07-service.yaml -n green
kubectl delete -f 07-deploy-blue.yaml -n blue
kubectl delete -f 07-deploy-green.yaml -n green

kubectl api-resources --namespaced=true

k3d cluster delete meucluster
```
