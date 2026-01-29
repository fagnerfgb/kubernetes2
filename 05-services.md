# Services

**Autor:** Fagner Geraldes  
**Data de criação:** 26/01/2026  
**Data de atualização:** 26/01/2026  
**Versão:** 0.01  

## ClusterIP

```bash
k3d cluster create meucluster --servers 3 --agents 3 -p "30000:30000@loadbalancer"
kubectl apply -f 05-deployment.yaml && watch 'kubectl get pods'
kubectl get pod -o wide | awk 'NR>1 {print $6}'
kubectl run -it --image kubedevio/ubuntu-curl ping-test --restart=Never --rm -- /bin/bash
```

```bash
curl http://10.42.4.4
```

```bash
kubectl delete -f 05-deployment.yaml
kubectl apply -f 05-service-clusterip.yaml && watch 'kubectl get svc,po'
kubectl describe svc web-service | grep Type:
```

```bash
curl http://web-service
exit
```

```bash
kubectl scale deployment deployment --replicas 10 && watch 'kubectl get svc,po'
kubectl delete -f 05-service-clusterip.yaml
```

## NodePort

```bash
kubectl apply -f 05-service-nodeport.yaml && watch 'kubectl get svc,po'
kubectl get node k3d-meucluster-server-0 -o wide | awk 'NR>1 {print $6}'
kubectl run -it --image kubedevio/ubuntu-curl ping-test --restart=Never --rm -- /bin/bash
```

```bash
curl http://web-service
curl http://172.19.0.2:30000
```

```bash
kubectl scale deployment deployment --replicas 10 && watch 'kubectl get svc,po'
```

```bash
curl http://web-service
curl http://172.19.0.2:30000
exit
```

## LoadBalancer

```bash
kubectl delete -f 05-service-nodeport.yaml
kubectl apply -f 05-service-loadbalancer.yaml && watch 'kubectl get svc,po'
kubectl get service web-service
kubectl delete -f 05-service-loadbalancer.yaml
```

## ExternalName

```bash
kubectl apply -f 05-service-externalname.yaml && watch 'kubectl get svc,po'
kubectl run -it --image kubedevio/ubuntu-curl ping-test --restart=Never --rm -- /bin/bash
```

```bash
curl https://www.google.com
curl http://web-service
exit
```

```bash
kubectl delete -f 05-service-externalname.yaml
k3d cluster delete meucluster
```
