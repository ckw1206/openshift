# Deploy ARO usign Azure cli 

```
LOCATION=japaneast               
RESOURCEGROUP=test-aro-rg         
CLUSTER=test-aro-cluster 
```

### Create resource group 
```
az group create \
  --name $RESOURCEGROUP \
  --location $LOCATION
```

### Create vnet
```az network vnet create \
   --resource-group $RESOURCEGROUP \
   --name aro-vnet \
   --address-prefixes 10.0.0.0/22
```

### Create Master subnet
```az network vnet subnet create \
  --resource-group $RESOURCEGROUP \
  --vnet-name aro-vnet \
  --name master-subnet \
  --address-prefixes 10.0.0.0/23 \
  --service-endpoints Microsoft.ContainerRegistry
```

### Create worker subnet
```
az network vnet subnet create \
  --resource-group $RESOURCEGROUP \
  --vnet-name aro-vnet \
  --name worker-subnet \
  --address-prefixes 10.0.2.0/23 \
  --service-endpoints Microsoft.ContainerRegistry
```

### Disable private link service network policy for Master subnet
```
az network vnet subnet update \
  --name master-subnet \
  --resource-group $RESOURCEGROUP \
  --vnet-name aro-vnet \
  --disable-private-link-service-network-policies true
```

### Create ARO
```
az aro create \
  --resource-group $RESOURCEGROUP \
  --name $CLUSTER \
  --vnet aro-vnet \
  --master-subnet master-subnet \
  --worker-subnet worker-subnet
```

### Delete ARO
```
az aro delete --resource-group $RESOURCEGROUP --name $CLUSTER
```
