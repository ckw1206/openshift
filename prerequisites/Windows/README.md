### Download and install Docker desktop for Windows
https://docs.docker.com/desktop/install/windows-install/

### To use Azure Container Registry
- Download and install latest release of the Azure Cli
  
  PowerShell
  ```
  Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows \ 
  -OutFile .\AzureCLI.msi; Start-Process msiexec.exe -Wait \ 
  -ArgumentList '/I AzureCLI.msi /quiet'; rm .\AzureCLI.msi
  ```

### Import image to Azure Container Registry

- To import image to Azure Container Registry from a file.
  Load an image from a file to Docker
  ```
  docker import <path>/<to>/<image>
  ```
  
  Check Docker images
  ```
  docker images
  ```
  
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
  
