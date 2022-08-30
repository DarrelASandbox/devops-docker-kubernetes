```sh
# View the working directory of the host machine
minikube ssh
cd /var/data

# Build image and push to Docker Hub
docker build -t darrela/story-app .
docker push darrela/story-app

# Deployment & Service
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
minikube service story-app-ser

# Storage Class is provided by default
kubectl get sc

# PV & PVC
kubectl apply -f host-pv.yaml
kubectl apply -f host-pvc.yaml
kubectl apply -f deployment.yaml
kubectl get pv

# Using `env.yaml` file
kubectl apply -f env.yaml
kubectl get configmap
```
