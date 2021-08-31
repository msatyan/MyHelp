

Sample CLI2
```
az group create  --name SatResourceGroupVM --location eastus
az group list 
az group list --query "[?location=='eastus']"
#az group delete  -n SatResourceGroupVM  [--no-wait  --yes]

az vm   create     --resource-group SatResourceGroupVM --name SatVM1  --image UbuntuLTS --generate-ssh-keys

az vm   deallocate -g SatResourceGroupVM -n SatVM1 --no-wait
az vm   delete     -g SatResourceGroupVM -n SatVM1 --yes
az disk list       --resource-group SatResourceGroupVM --output table
az disk delete     --name osdisk_170a7c39c8 --resource-group SatResourceGroupVM --no-wait --yes

az group delete  -n SatResourceGroupVM  [--no-wait  --yes]

```

#### From Win Sub Linux
```
 az vm create --resource-group SatResourceGroupVM --name SatVM2 --image CentOS    --generate-ssh-keys  --admin-username myadmin1 --authentication-type password

 ssh myadmin1@52.168.164.131
 cat /etc/os-release
```

## [Create an image of a virtual machine or VHD](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/capture-image)

#### Connect to your Linux VM using an SSH client
```
ssh myadmin1@52.168.164.131
```

### Step 1: Deprovision the VM
```
sudo waagent -deprovision+user -force

exit the SSH session
exit
```

### Step 2: Create VM image

#### Deallocate the VM that you deprovisioned
```
az vm deallocate --resource-group SatResourceGroupVM --name SatVM2
```

#### Mark the VM as generalized
```
az vm generalize --resource-group SatResourceGroupVM --name SatVM2
```


### Now create an image of the VM
```
az image create --resource-group SatResourceGroupVM --name myAzImage1 --source SatVM2
```

### Creating the VM in another resource group
```
az group create  --name SatResourceGroupVM2 --location eastus

az vm create --resource-group SatResourceGroupVM2 --name SatVmFromImg1 --image     \
"/subscriptions/219bdedc-ff78-4adf-a8db-391f347c1508/resourceGroups/SatResourceGroupVM/providers/Microsoft.Compute/images/myAzImage1"        \
--admin-username myadmin2  --authentication-type password
```

### Step 4: Verify the deployment
```
az vm show --resource-group SatResourceGroupVM2 --name SatVmFromImg1 --show-details
```


### Cleanup 
```
az vm   deallocate -g SatResourceGroupVM -n SatVM2 
az vm   delete     -g SatResourceGroupVM -n SatVM2 --yes

az vm   deallocate -g SatResourceGroupVM2 -n SatVmFromImg1
az vm   delete     -g SatResourceGroupVM2 -n SatVmFromImg1 --yes

az disk list     --resource-group SatResourceGroupVM --output table
az disk delete   --name osdisk_d5b0924e89 --resource-group SatResourceGroupVM --yes

#az image list    --resource-group SatResourceGroupVM
#az image delete  --name myAzImage1 --resource-group SatResourceGroupVM
az group delete  -n SatResourceGroupVM --yes

az disk  list    --resource-group SatResourceGroupVM2 --output table
az disk  delete  --name osdisk_2d204a108a --resource-group SatResourceGroupVM2 --yes
az group delete  -n SatResourceGroupVM2  --yes
```




