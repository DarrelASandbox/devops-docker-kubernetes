```sh
# Imperative approach
docker build -t k8s-first .

minikube status
minikube start
minikube dashboard

docker tag k8s-first darrela/k8s-first
docker push darrela/k8s-first

# Deployment
kubectl create deployment k8s-first --image=darrela/k8s-first
kubectl get deployments
kubectl get pods

# Service
# Options: --type=ClusterIp OR NodePort
kubectl expose deployment k8s-first --type=LoadBalancer --port 8080
kubectl get services
minikube service k8s-first

##############################################################

# Scaling
# A "replica" is simply an instance of a Pod/ Container
# 3 Replicas means that the same Pod/ Container is running 3 times
kubectl scale deployment/k8s-first --replicas=3

##############################################################

# Update
# Pushing new image with a different tag to Docker Hub
docker build -t darrela/k8s-first:2 .
docker push darrela/k8s-first:2

# K8S CONTAINER=DOCKER HUB REPO
kubectl set image deployment/k8s-first k8s-first=darrela/k8s-first:2
kubectl rollout status deployment/k8s-first

##############################################################

# Rollback deployment
# Create error by setting to image that doesn't exist
kubectl set image deployment/k8s-first k8s-first=darrela/k8s-first:3
# Waiting for deployment "k8s-first" rollout to finish: 1 old replicas are pending termination...
kubectl rollout status deployment/k8s-first
# ErrImagePull/ ImagePullBackOff STATUS
kubectl get pods
# Undo latest deployment
kubectl rollout undo deployment/k8s-first

# Show REVISION & CHANGE-CAUSE
kubectl rollout history deployment/k8s-first
kubectl rollout history deployment/k8s-first --revision=3

# Undo to specific revision
kubectl rollout undo deployment/k8s-first --to-revision=1

##############################################################

kubectl delete service k8s-first
kubectl delete deployments k8s-first
```

```sh
# Declarative approach
# We can edit deployment.yaml file then re-apply changes if required
# e.g. changing image tag or `replicas` number
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
minikube service k8s-second-ser

# Delete resources not the .yaml file
kubectl delete -f deployment.yaml
kubectl delete -f deployment.yaml,service.yaml

# Delete which kind by label
kubectl delete deployments,services -l group=deleteByLabel

# Combining 2 .yaml files together
kubectl apply -f singleConfig.yaml
```
