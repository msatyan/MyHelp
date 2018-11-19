
#### Azure CLI 2.0
* [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)

* [Azure CLI 2.0: Command reference - az](https://docs.microsoft.com/en-us/cli/azure/)  


```
az --version
az login
```


#### Highlights
[Common Azure CLI 2.0 commands for managing Azure resources](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/cli-manage)

[Azure CLI 1.0 vs 2.0 Compared](https://buildazure.com/2017/05/16/azure-cli-1-0-vs-2-0-compared-installation-and-usage/)


[How to create an image of a virtual machine or VHD](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/capture-image)

#### Sample 
```

az group create --name SatResourceGroupVM --location eastus
{
  "id": "/subscriptions/<UUID...>/resourceGroups/SatResourceGroupVM",
  "location": "eastus",
  "managedBy": null,
  "name": "SatResourceGroupVM",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}


C:\>az vm create --resource-group SatResourceGroupVM --name SatVM1  --image UbuntuLTS --generate-ssh-keys
SSH key files 'C:\Users\devc\.ssh\id_rsa' and 'C:\Users\devc\.ssh\id_rsa.pub' have been generated under ~/.ssh to allow SSH access to the VM. 
If using machines without permanent storage, back up your keys to a safe location.
{| Finished ..
  "fqdns": "",
  "id": "/subscriptions/<UUID ...>/resourceGroups/SatResourceGroupVM/providers/Microsoft.Compute/virtualMachines/SatVM1",
  "location": "eastus",
  "macAddress": "00-0D-3A-14-0A-AF",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.82.180.158",
  "resourceGroup": "SatResourceGroupVM"
}
```

#### Connect to the VM
```
$ssh 13.82.180.158
exit
```

#### az configure
```
C:\>az configure

Welcome to the Azure CLI! This command will guide you through logging in and setting some default values.

Your settings can be found at C:\Users\devc\.azure\config
Your current configuration is as follows:

[cloud]
name = AzureCloud

Do you wish to change your settings? (y/N): n

You're all set! Here are some commands to try:
 $ az login
 $ az vm create --help
 $ az feedback


C:\>
```

#### az vm create
```
C:\>az vm create --resource-group SatResourceGroupVM --name SatVM1  --image UbuntuLTS --generate-ssh-keys
{| Finished ..
  "fqdns": "",
  "id": "/subscriptions/<UUID of subscription>/resourceGroups/SatResourceGroupVM/providers/Microsoft.Compute/virtualMachines/SatVM1",
  "location": "eastus",
  "macAddress": "00-0D-3A-14-0A-AF",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.82.183.25",
  "resourceGroup": "SatResourceGroupVM"
}
```

#### az vm deallocate
```
C:\>az vm deallocate -g SatResourceGroupVM -n SatVM1 --no-wait
```
#### az vm delete
```
C:\>az vm delete     -g SatResourceGroupVM -n SatVM1 --yes
{/ Finished ..
  "endTime": "2017-07-29T23:59:56.076542+00:00",
  "error": null,
  "name": "81864f5c-b479-4fe9-a61c-ac21c282ee9a",
  "startTime": "2017-07-29T23:59:45.669401+00:00",
  "status": "Succeeded"
}
```
#### az disk list
```
C:\>az disk list --resource-group SatResourceGroupVM --output table
  DiskSizeGb  Location    Name               OsType    ProvisioningState    ResourceGroup       TimeCreated
------------  ----------  -----------------  --------  -------------------  ------------------  --------------------------------
          30  eastus      osdisk_170a7c39c8  Linux     Succeeded            SatResourceGroupVM  2017-07-29T23:34:53.919026+00:00
```

#### az disk delete
```
C:\>az disk delete --name osdisk_170a7c39c8 --resource-group SatResourceGroupVM --no-wait --yes

C:\>az disk list --resource-group SatResourceGroupVM --output table


C:\>
```


#### Delete the resource group
```
az group delete -n SatResourceGroupVM 
```

