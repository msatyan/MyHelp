### One of the option for Ansible we need to pre create:
* Storage account, 
* Network interface, 
* Security group 
* Public IP address

#### [Create ResGroup](https://docs.microsoft.com/en-us/cli/azure/group)
```
az group create  --name rdResourceGroup1 --location eastus
az group delete --name rdResourceGroup1 --yes
```

#### [Storage account](https://docs.microsoft.com/en-us/cli/azure/storage)
```
az storage account create -n rdstorageacc1 -g rdResourceGroup1 -l westus --sku Standard_LRS
az storage account list -g rdResourceGroup1
az storage account show -g rdResourceGroup1 -n rdstorageacc1
```

#### Network interface:
* [az network vnet create](https://docs.microsoft.com/en-us/cli/azure/network/vnet#create)
```
az network vnet create -n rdVnet1 -g rdResourceGroup1 --subnet-name rdSubnet1
```

* [az network nic create](https://docs.microsoft.com/en-us/cli/azure/network/nic#create)
```
az network nic create  -n rdNIC1 -g rdResourceGroup1 --vnet-name rdVnet1 --subnet rdSubnet1

az network nic list   --resource-group rdResourceGroup1
```

#### [Security group](https://docs.microsoft.com/en-us/cli/azure/network/nsg#create)
```
az network nsg create -g rdResourceGroup1 -n rdNsg1
```

#### [Public IP address](https://docs.microsoft.com/en-us/cli/azure/network/public-ip#create)
```
az network public-ip create -g rdResourceGroup1 -n rdPublicIP1
```

#### [Managed Disks](https://docs.microsoft.com/en-us/cli/azure/disk)
```
az disk create -n DataDisk1 -g rdResourceGroup1 --size-gb 10 --sku Premium_LRS
az disk list   -g rdResourceGroup1 --output table
az disk delete -n DataDisk1 -g rdResourceGroup1 --yes

```

#### [Virtual Machines](https://docs.microsoft.com/en-us/cli/azure/vm)
```
Yet to get it working...

az vm create --resource-group rdResourceGroup1 --name rdMasterVM1  
--image CentOS --generate-ssh-keys --admin-username rdadmin1  
--authentication-type password --attach-data-disks DataDisk1  
--storage-account rdstorageacc1  
--nics rdNIC1  
--nsg rdNsg1  
--public-ip-address rdPublicIP1  
```


