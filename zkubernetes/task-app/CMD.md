```sh
# Build user image and push to Docker Hub
docker build -t darrela/task-app-users .
docker push darrela/task-app-users

# Build auth image and push to Docker Hub
docker build -t darrela/task-app-auth .
docker push darrela/task-app-auth

# Deployment & Service
kubectl apply -f ./k8s/users-deployment.yaml
kubectl apply -f ./k8s/users-service.yaml
minikube service users-service

# Delete resources not the .yaml file
kubectl delete -f ./k8s/users-deployment.yaml,./k8s/users-service.yaml

# Debug
# POD NAME -c CONTAINER
kubectl get pods
kubectl logs users-deployment-d8d6f6db-sqhpf -c auth
```
