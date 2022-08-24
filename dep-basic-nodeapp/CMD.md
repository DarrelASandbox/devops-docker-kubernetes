```sh
docker build -t dep-basic-nodeapp .
docker run --rm --name dep-basic-nodeapp -dp 80:80 dep-basic-nodeapp

# For Apple M1 (Refer to Ryan's comment)
docker buildx build --platform linux/amd64 -t dep-basic-nodeapp .
# For Docker Hub
docker tag dep-basic-nodeapp darrela/dep-basic-nodeapp
docker push darrela/dep-basic-nodeapp
```
