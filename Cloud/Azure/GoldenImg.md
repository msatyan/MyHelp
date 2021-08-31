
## Create rdMasterVM1
```
az group create  --name rdResourceGroup1 --location eastus

az disk create -g rdResourceGroup1 -n DataDisk1 --size-gb 10 --sku Premium_LRS
az disk list     --resource-group rdResourceGroup1 --output table

az vm create --resource-group rdResourceGroup1 --name rdMasterVM1 --image CentOS --generate-ssh-keys --admin-username rdadmin1 --authentication-type password --attach-data-disks DataDisk1

az vm list --resource-group rdResourceGroup1 

 ssh rdadmin1@40.121.155.24
 cat /etc/os-release
 lsblk
 scp /work/sample.txt rdadmin1@40.121.155.24:/work/.
```

## [Create an image of a virtual machine or VHD](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/capture-image)

#### Connect to your Linux VM using an SSH client
```
ssh rdadmin1@40.121.155.24
```

## Step 1: Deprovision the VM
```
sudo waagent -deprovision+user -force

exit the SSH session
exit
```

## Step 2: Create a GoldenImage1 from rdMasterVM1

#### Deallocate the VM that you deprovisioned
```
az vm deallocate --resource-group rdResourceGroup1 --name rdMasterVM1
```

#### Mark the VM as generalized
```
az vm generalize --resource-group rdResourceGroup1 --name rdMasterVM1
```


#### Now create an image of the VM
```
az image create --resource-group rdResourceGroup1 --name GoldenImage1 --source rdMasterVM1

az image list --resource-group rdResourceGroup1
```
## Step 3: Create a VM from the captured GoldenImage

#### Creating the VM in another resource group
```
az group create  --name CustResGroup1 --location eastus

az vm create --resource-group CustResGroup1 --name CustVM1 --image   "/subscriptions/<GUID>/resourceGroups/rdResourceGroup1/providers/Microsoft.Compute/images/GoldenImage1"   --admin-username custadmin1  --authentication-type password
```

## Step 4: Verify the deployment
```
az vm show --resource-group CustResGroup1 --name CustVM1 --show-details
```

### Access the new VM
```
ssh custadmin1@13.92.88.119
and it should all looks :)!
```

## Step 5: Cleanup
FYI: Deleting the Resource Group will delete the resources associated with the group. By any chance if you need to delete each of the resources individually the following commands can be used.

### Delete rdMasterVM1
```
az vm   deallocate -g rdResourceGroup1 -n rdMasterVM1 
az vm   delete     -g rdResourceGroup1 -n rdMasterVM1 --yes

az disk list     --resource-group rdResourceGroup1 --output table
az disk delete   --name <OS Disk> --resource-group rdResourceGroup1 --yes
eg: 
az disk delete   --name osdisk_d5b0924e89 --resource-group rdResourceGroup1 --yes
```


### Delete Network resources such as 
* rdMasterVM1NSG	      Network security group
* rdMasterVM1PublicIP	  Public IP address
* rdMasterVM1VMNic	      Network interface
* rdMasterVM1VNET         Virtual network
```
az network nic list   --resource-group rdResourceGroup1
az network nic delete --name rdMasterVM1VMNic --resource-group rdResourceGroup1

az network nsg list -g rdResourceGroup1 -o table
az network nsg show -g rdResourceGroup1 -n rdMasterVM1NSG
az network nsg delete -n rdMasterVM1NSG -g rdResourceGroup1

az network public-ip list  --resource-group rdResourceGroup1
az network public-ip delete --name  rdMasterVM1PublicIP --resource-group rdResourceGroup1

#az network vnet create ...
az network vnet list  --resource-group rdResourceGroup1
az network vnet delete --name rdMasterVM1VNET --resource-group rdResourceGroup1
```


### Delete CustVM1
```
az vm   deallocate -g CustResGroup1 -n CustVM1
az vm   delete     -g CustResGroup1 -n CustVM1 --yes

az disk list     --resource-group CustResGroup1 --output table
az disk delete   --name <OS Disk> --resource-group CustResGroup1 --yes
eg: 
az disk delete   --name osdisk_d5b0924e89 --resource-group CustResGroup1 --yes

az group delete  -n CustResGroup1  --yes
```

### Delete GoldenImage1
```
az image list    --resource-group rdResourceGroup1
az image delete  --name GoldenImage1 --resource-group rdResourceGroup1

# If you have no plan to keep the resource group of GoldenImage1, 
# then only delete it. 
az group delete  -n rdResourceGroup1 --yes
```




