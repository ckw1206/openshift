### To run docker in Windows platform
  - Download and install Docker desktop for Windows
  
    https://docs.docker.com/desktop/install/windows-install/

### To use Azure Container Registry
- Download and install latest release of the Azure Cli

  https://aka.ms/installazurecliwindows

### Export & Import images
- To export/save an exist image to a file
  - Use docker save
  ```
  docker save <IMAGE ID> > image.tar
  ```
  - Use docker export
  ```
  docker export <CONTAINER ID> > image.tar
  ```
 
- To import/load an image from a file
  - Use docker import
  ```
  docker import <path>/<to>/<image>
  ```
  - Use docker load
  ```
  docker load -i <path>/<to>/<image>
  ```
  
  Check Docker images
  ```
  docker images
  ```



### Import image to Azure Container Registry

- To import image to Azure Container Registry from a file.
  
  Rename Repo and tag
  ```
  docker image tag <IMAGE ID> <registry-name>.azurecr.io/<repo-name>/<image-name>:tag
  ```
  
  Log in to Azure Subscription with Container Role
  ```
  az login
  ```
  
  Create a new Azure Container Registry
  ```
  az acr create --resource-group <ResourceGroup> \
  --name <registry-name> --sku Basic/Standard/Premium
  ```
  
  Enable admin
  ```
  az acr update -n <registry-name> --admin-enabled true
  ```
  
  Get Registry Credential
  ```
  az acr credential show -n <registry-name>
  
  Sample output:
  {
  "passwords": [
    {
      "name": "password",
      "value": <pwdvalue-1>
    },
    {
      "name": "password2",
      "value": <pwdvalue-2>
    }
  ],
  "username": <registry-name>
  }
  ```
  
  Log in to Registry
  ```
  docker login <registry-name>.azurecr.io
  Username: <registry-name>
  Password: <pwdvalue>
  ```
  
  Push image to Azure Container Registry
  ```
  sudo docker push <registry-name>.azurecr.io/<repo-name>/<image-name>:tag
  ```
  
  List container images
  ```
  az acr repository list --name <registry-name> --output table
  ```
  
