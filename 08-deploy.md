# Deploy

**Autor:** Fagner Geraldes  
**Data de criação:** 27/01/2026  
**Data de atualização:** 27/01/2026  
**Versão:** 0.01  

```bash
git clone https://github.com/KubeDev/pedelogo-catalogo.git
docker build -t fagnerfgb/pedelogo-catalogo:v1.0.0 -f "./pedelogo-catalogo/src/PedeLogo.Catalogo.Api/Dockerfile" "./pedelogo-catalogo"
docker image ls
docker push fagnerfgb/pedelogo-catalogo:v1.0.0


k3d cluster create meucluster --servers 3 --agents 3
kubectl apply -f ./k8s/mongodb/deployment.yaml && watch 'kubectl get svc,po,endpoints'
kubectl apply -f ./k8s/api/deployment.yaml && watch 'kubectl get svc,po,endpoints'
kubectl get nodes -o wide
kubectl get svc -o wide
#http://ip:porta/swagger

kubectl delete -f ./k8s/mongodb/deployment.yaml
kubectl delete -f ./k8s/api/deployment.yaml
k3d cluster delete meucluster
```
