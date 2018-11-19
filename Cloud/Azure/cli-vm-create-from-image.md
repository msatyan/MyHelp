
#### Azure CLI
* [Azure CLI CMD](https://docs.microsoft.com/en-us/cli/azure/reference-index)
* [Create and Manage Linux VMs with the Azure CLI](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-vm)


#### Create a VM
```bash
# create resource group
az group create --name myResourceGroup1 --location eastus

# Create a VM
az vm create -n myVm1 -g MyResourceGroup1 --image Centos

# Enable Managed Service Identity (MSI) on the VM
# az vm identity assign -g myResourceGroup1 -n myVm1

# FYI: Delete resource group (by any chance)
# az group delete --name myResourceGroup1
```

---
#### Create image of the VM
[How to create an image of a virtual machine or VHD](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/capture-image)
```bash
# SSH to the VM
ssh <Public IP of the VM>
or
ssh <user>@<Public IP of the VM>

# FYI Only: to get Access token from the VM
# curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com%2F' -H Metadata:true -s


# Connect to your Linux VM using an SSH client, in the SSH window, type the following command:
sudo waagent -deprovision+user

# Exit the SSH 
exit

# 1) Deallocate the VM that you deprovisioned
az vm deallocate -g myResourceGroup1 -n myVm1

# 2) Mark the VM as generalized
az vm generalize -g myResourceGroup1 -n myVm1

# 3) create an image of the VM
az image create -g myResourceGroup1  -n myImage1 --source myVm1

# FYI: If you would like to store your image in zone-resilient storage, you need to create it in a region that supports availability zones and include the --zone-resilient true parameter.
```

---

## Test Image: Create a VM from the captured image
To create a VM from Image we need to specify ID of the image. If you know ImageName and the ResourceGroup of the image then you could query the ID by using the following command.


#### Get VM ID
```bash
# Get Image ID of the VmImage (Input ImageName, Resource Group)
az image show -n myImage1   -g myResourceGroup1 --query id  --out tsv

# sample output
/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup1/providers/Microsoft.Compute/images/myImage1
```

### Create a VM from the image
```bash
# Create a resource group for the new VM
az group create --name test_rgroup_01 --location eastus

az vm create -g test_rgroup_01 -n myTestVm1  --admin-username myadmin   --ssh-key-value ~/.ssh/id_rsa.pub \
--image "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup1/providers/Microsoft.Compute/images/myImage1"
```

---
#### Login to the new VM and access resources
```bash
# login to the VM
ssh myadmin@<public IP of new VM>

# if you need to become a specificuser1 to access resources ...
sudo -u specificuser1 bash

#run as root
sudo bash
```

#### delete the test resources
```bash
# FYI: Delete all resource used by test
az group delete -n test_rgroup_01
```
