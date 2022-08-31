```sh
# Info
kubectl get namespaces

# Build users image and push to Docker Hub
docker build -t darrela/task-app-users .
docker push darrela/task-app-users

# Build auth image and push to Docker Hub
docker build -t darrela/task-app-auth .
docker push darrela/task-app-auth

# Build tasks image and push to Docker Hub
docker build -t darrela/task-app-tasks .
docker push darrela/task-app-tasks

# Build frontend image and run locally
docker build -t darrela/task-app-frontend .
docker run -dp 80:80 --rm darrela/task-app-frontend

# Deployment & Service
kubectl apply -f ./k8s/users-deployment.yaml
kubectl apply -f ./k8s/users-service.yaml
minikube service users-service

kubectl apply -f ./k8s/auth-deployment.yaml
kubectl apply -f ./k8s/auth-service.yaml

kubectl apply -f ./k8s/tasks-deployment.yaml
kubectl apply -f ./k8s/tasks-service.yaml
minikube service tasks-service

# Delete resources not the .yaml file
kubectl delete -f ./k8s/users-deployment.yaml,./k8s/users-service.yaml

# Debug
# POD NAME -c CONTAINER
kubectl get pods
kubectl logs users-deployment-d8d6f6db-sqhpf -c auth
```
