```sh
docker build -t k8s-first .

minikube status
minikube start
minikube dashboard

docker tag k8s-first darrela/k8s-first
docker push darrela/k8s-first

kubectl create deployment k8s-first --image=darrela/k8s-first
kubectl get deployments
kubectl get pods
kubectl delete deployments k8s-first
```
