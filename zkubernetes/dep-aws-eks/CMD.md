```sh
# Build users image and push to Docker Hub
docker build -t darrela/dep-aws-eks-users .
docker push darrela/dep-aws-eks-users

# Build auth image and push to Docker Hub
docker build -t darrela/dep-aws-eks-auth .
docker push darrela/dep-aws-eks-auth

# Setup AWS EKS: Follow instructions on README

# Deployment & Service
kubectl apply -f ./kubernetes/auth.yaml -f ./kubernetes/users.yaml

# Info
kubectl get deployments
kubectl get pods
kubectl get services
```
