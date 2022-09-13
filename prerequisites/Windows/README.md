### Download and install Docker desktop for Windows
https://docs.docker.com/desktop/install/windows-install/

### To use Azure Container Registry
- Download and install latest release of the Azure Cli
  
  PowerShell
  ```
  Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi; Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'; rm .\AzureCLI.msi
  ```
