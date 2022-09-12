## Install Podman on MacOS
```
brew install podman
```

### To build a ubuntu image for MacOS with M1 chip and pre-install openshift-installer 
```
FROM --platform=linux/amd64 ubuntu:latest
RUN apt-get update  && apt-get upgrade && apt-get install -y vim curl wget ssh-tools
RUN wget https://mirror.openshift.com/pub/openshift-v4/x86_64/clients/ocp/stable/openshift-install-linux.tar.gz && tar xvf openshift-install-linux.tar.gz && rm README.md openshift-install-linux.tar.gz
RUN mkdir -p /home/root/.ssh/ && ssh-keygen -t ed25519 -N '' -f /home/root/.ssh/id_ocp && eval "$(ssh-agent -s)"
```
