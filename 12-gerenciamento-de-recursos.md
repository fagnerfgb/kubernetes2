#Autor: Fagner Geraldes  
#Data de criação: 29/01/2026  
#Data de atualização: 29/01/2026  
#Versão: 0.01  

### Gerenciamento de Recursos de aplicações e de ambientes

### Resource Request e Resource Limits

```bash
k3d cluster create meucluster --servers 3 --agents 3 -p "30000:30000@loadbalancer"
kubectl apply -f 12-resource.yaml && watch 'kubectl get all'
kubectl top pods
kubectl get service
curl --data "megabytes=20&durationSec=30" http://localhost:30000/ConsumeMem && curl --data "millicores=130&durationSec=30" http://localhost:30000/ConsumeCPU && watch 'kubectl top pods'
curl --data "megabytes=80&durationSec=30" http://localhost:30000/ConsumeMem && curl --data "millicores=600&durationSec=30" http://localhost:30000/ConsumeCPU && watch 'kubectl top pods'
kubectl delete -f 12-resource.yaml
```

### Horizontal Pod AutoScaler

```bash
kubectl apply -f 12-hpa.yaml
kubectl apply -f 12-resource.yaml
curl --data "millicores=400&durationSec=120" http://localhost:30000/ConsumeCPU && watch 'kubectl top pods && kubectl get pods && kubectl get hpa'
```

### Quality of Service

```bash
kubectl describe $(kubectl get pod -o name) | grep "QoS Class:"
kubectl delete -f 12-resource.yaml
kubectl apply -f 12-resource2.yaml
kubectl describe $(kubectl get pod -o name) | grep "QoS Class:"
kubectl delete -f 12-resource2.yaml
kubectl apply -f 12-resource3.yaml
kubectl describe $(kubectl get pod -o name) | grep "QoS Class:"
kubectl delete -f 12-resource3.yaml
kubectl delete -f 12-hpa.yaml
```

```bash
kubectl apply -f ./k8s/mongodb/mongodb-secret.yaml
kubectl apply -f ./k8s/api/api-configmap.yaml
kubectl apply -f ./k8s/mongodb/deployment4.yaml
kubectl apply -f ./k8s/api/deployment4.yaml
watch 'kubectl get all'
kubectl top pods
kubectl delete -f ./k8s/mongodb/mongodb-secret.yaml
kubectl delete -f ./k8s/api/api-configmap.yaml
kubectl delete -f ./k8s/mongodb/deployment4.yaml
kubectl delete -f ./k8s/api/deployment4.yaml
```

### Limit Range

```bash
kubectl apply -f 12-limit-range.yaml
kubectl apply -f 12-deployment.yaml
kubectl get limitrange
kubectl describe limitrange limite-container
kubectl get pod
kubectl describe pod | grep Limits: -A 10
kubectl delete -f 12-deployment.yaml
kubectl apply -f 12-deployment2.yaml
kubectl get all
kubectl describe rs
kubectl delete -f 12-deployment2.yaml
kubectl delete -f 12-limit-range.yaml
```

### Resource Quota

```bash
kubectl apply -f 12-resource-quota.yaml
kubectl apply -f 12-deployment3.yaml
watch 'kubectl get all'
kubectl describe rs
kubectl delete -f 12-resource-quota.yaml
kubectl delete -f 12-deployment3.yaml
```

```bash
kubectl apply -f 12-resource-quota2.yaml
kubectl apply -f 12-deployment3.yaml
watch 'kubectl get all'
kubectl describe rs
kubectl delete -f 12-resource-quota2.yaml
kubectl delete -f 12-deployment3.yaml
k3d cluster delete meucluster
```