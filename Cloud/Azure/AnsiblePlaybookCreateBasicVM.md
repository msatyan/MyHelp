

#### FYI: Ansible Playbook steps to create a VM
*  [Playbook steps to create a basic Linux VM in Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ansible-create-vm)

* [Playbook steps to create a complete Linux VM in Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ansible-create-complete-vm)

* [Ansible module : azure_rm_virtualmachine](http://docs.ansible.com/ansible/latest/azure_rm_virtualmachine_module.html)


## Prerequisite : 
* [Ansible Azure Setup done](https://github.com/msatyan/MyHelp/blob/master/Azure/AnsibleAzureSetup.md)


#### [Create ResGroup](https://docs.microsoft.com/en-us/cli/azure/group)
```
az group create  --name rdResourceGroup1 --location eastus
# az group delete --name rdResourceGroup1 --yes
```

#### [Create a virtual network for your VM](https://docs.microsoft.com/en-us/cli/azure/network/vnet#create)
```
az network vnet create --resource-group rdResourceGroup1 --name rdVnet1 --address-prefix 10.0.0.0/16 --subnet-name rdSubnet1 --subnet-prefix 10.0.1.0/24  
```



### Ansible Playbook for Basic Linux VM in Azure
Create **azure_create_basic_vm.yml** with the following.
```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create VM
    azure_rm_virtualmachine:
      resource_group: rdResourceGroup1
      name: rdMasterVM1
      vm_size: Standard_DS1_v2
      admin_username: satyan
      ssh_password_enabled: false
      ssh_public_keys: 
        - path: /home/satyan/.ssh/authorized_keys
          key_data: '<Insert yor ssh public key here... >'
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

### Run the playbook
```
ansible-playbook    azure_create_basic_vm.yml

PLAY [Create Azure VM] *****************************************************************************

TASK [Gathering Facts] *****************************************************************************
ok: [localhost]

TASK [Create VM] ***********************************************************************************
changed: [localhost]

PLAY RECAP *****************************************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```

##### FYI: if you get error saying
```diff
- ImportError: No module named packaging.version
```

```
sudo pip install -U pip setuptools

https://stackoverflow.com/questions/44583740/no-module-named-packaging-version-for-ansible-vm-provisioning-in-azure

```
