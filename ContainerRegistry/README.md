# Azure Container Registry

### To login Azure Container Registry
```
sudo docker login <ACR-name>.azurecr.io
```

### To push an image to repository by Docker
```
sudo docker push <ACR-name>.azurecr.io/<repo-name>/<image-name>:tag
```

### To pull an image from ACR by Docker

#### Use **Docker** env:
```
sudo docker pull <ACR-name>.azurecr.io/<repo-name>/<image-name>:tag
```

#### Use **OpenShift** env, you must create a docker-registry secret at first.
Get ACR Access Key
```
az acr credential show -n <ACR-name>
```

Create a **docker-registry secret**.
```
oc create secret docker-registry \
    --docker-server=<your registry name>.azurecr.io \
    --docker-username=<ACR-name> \
    --docker-password=******** \
    --docker-email=unused \
    acr-secret
```

Create a new Pod by using image in ACR.
```
apiVersion: v1
kind: Pod
metadata:
  name: hello-world
spec:
  containers:
  - name: hello-world
    image: <your registry name>.azurecr.io/hello-world:v1
  imagePullSecrets:
  - name: acr-secret
  ```
