## Install Podman on MacOS
```
brew install podman
```

### To build an ubuntu image for MacOS with M1 chip and pre-install openshift-installer.
- Add --platform=linux/amd64 parameter to ensure ubuntu run in x86_64 arch as OpenShift don't provide an arm64 version installer.
```
FROM --platform=linux/amd64 ubuntu:latest
RUN apt-get update  && apt-get upgrade && apt-get install -y vim curl wget ssh-tools
RUN wget https://mirror.openshift.com/pub/openshift-v4/x86_64/clients/ocp/stable/openshift-install-linux.tar.gz && tar xvf openshift-install-linux.tar.gz && rm README.md openshift-install-linux.tar.gz
RUN mkdir -p /home/root/.ssh/ && ssh-keygen -t ed25519 -N '' -f /home/root/.ssh/id_ocp && eval "$(ssh-agent -s)"
```

### To generate an Install-Config for OpenShift Container Platform customized deployment.
```
./openshift create install-config --dir=<path>
```

### To Modify OpenShift Container Platform settings
- Sample
```
apiVersion: v1
baseDomain: example.com 
controlPlane: 
  hyperthreading: Enabled   
  name: master
  platform:
    azure:
      osDisk:
        diskSizeGB: 1024 
        diskType: StandardSSD_LRS
      type: Standard_D8s_v3
  replicas: 3
compute: 
- hyperthreading: Enabled 
  name: worker
  platform:
    azure:
      type: Standard_D2s_v3
      osDisk:
        diskSizeGB: 512 
        diskType: StandardSSD_LRS
      zones: 
      - "1"
      - "2"
      - "3"
  replicas: 5
metadata:
  name: test-cluster 
networking:
  clusterNetwork:
  - cidr: 10.128.0.0/14
    hostPrefix: 23
  machineNetwork:
  - cidr: 10.0.0.0/16
  networkType: OpenShiftSDN
  serviceNetwork:
  - 172.30.0.0/16
platform:
  azure:
    baseDomainResourceGroupName: resource_group 
    region: centralus 
    resourceGroupName: existing_resource_group 
    outboundType: Loadbalancer
    cloudName: AzurePublicCloud
pullSecret: '{"auths": ...}' 
fips: false 
sshKey: ssh-ed25519 AAAA... 
```

> The minimum vm size for `master node is CPUs:4/RAM:16GB`, and for `worker node is CPUs:2/RAM:8GB`. Both `replicas can be set as 1`.
