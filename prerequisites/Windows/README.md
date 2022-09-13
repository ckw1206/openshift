### Download and install Docker desktop for Windows
https://docs.docker.com/desktop/install/windows-install/

### To use Azure Container Registry
- Download and install latest release of the Azure Cli
  
  PowerShell
  ```
  Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi; Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'; rm .\AzureCLI.msi
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
  
  Rename Repo and tag if needed
  ```
  docker image tag <IMAGE ID> REPOSITORY:TAG
  ```
  
  Login to Azure with Azure Container Registry Contributor Permission
  ```
  az login
  ```
  


  
