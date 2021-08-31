
#### FYI: Ansible Playbook steps to create a VM
*  [Playbook steps to create a basic Linux VM in Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ansible-create-vm)

* [Playbook steps to create a complete Linux VM in Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ansible-create-complete-vm)

* [Ansible module : azure_rm_virtualmachine](http://docs.ansible.com/ansible/latest/azure_rm_virtualmachine_module.html)


## Prerequisite : 
* [Ansible Azure Setup done](https://github.com/msatyan/MyHelp/blob/master/Azure/AnsibleAzureSetup.md)
* [Create ResGroup](https://docs.microsoft.com/en-us/cli/azure/group)
```
az group create  --name rdResourceGroup1 --location eastus
# az group delete --name rdResourceGroup1 --yes
```
  
  
### Ansible Playbook for Complex Linux VM in Azure
Create **azure_create_complex_vm.yml** with the following.
```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create virtual network
    azure_rm_virtualnetwork:
      resource_group: rdResourceGroup1
      name: rdVnet1
      address_prefixes: "10.0.0.0/16"
  - name: Add subnet
    azure_rm_subnet:
      resource_group: rdResourceGroup1
      name: rdSubnet1
      address_prefix: "10.0.1.0/24"
      virtual_network: rdVnet1
  - name: Create public IP address
    azure_rm_publicipaddress:
      resource_group: rdResourceGroup1
      allocation_method: Static
      name: rdPublicIP1
  - name: Create Network Security Group that allows SSH
    azure_rm_securitygroup:
      resource_group: rdResourceGroup1
      name: rdNetworkSecurityGroup1
      rules:
        - name: SSH
          protocol: Tcp
          destination_port_range: 22
          access: Allow
          priority: 1001
          direction: Inbound
  - name: Create virtual network inteface card
    azure_rm_networkinterface:
      resource_group: rdResourceGroup1
      name: rdNIC1
      virtual_network: rdVnet1
      subnet: rdSubnet1
      public_ip_name: rdPublicIP1
      security_group: rdNetworkSecurityGroup1
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
      network_interfaces: rdNIC1
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

### Run the playbook
```
ansible-playbook    azure_create_complex_vm.yml
```

### Output
```
$ ansible-playbook    azure_create_complex_vm.yml

PLAY [Create Azure VM] *****************************************************************************

TASK [Gathering Facts] *****************************************************************************
ok: [localhost]

TASK [Create virtual network] **********************************************************************
changed: [localhost]

TASK [Add subnet] **********************************************************************************
changed: [localhost]

TASK [Create public IP address] ********************************************************************
changed: [localhost]

TASK [Create Network Security Group that allows SSH] ***********************************************
changed: [localhost]

TASK [Create virtual network inteface card] ********************************************************
changed: [localhost]

TASK [Create VM] ***********************************************************************************
changed: [localhost]

PLAY RECAP *****************************************************************************************
localhost                  : ok=7    changed=6    unreachable=0    failed=0

```


#### FYI: if you get error saying
```diff
- ImportError: No module named packaging.version
```

```
sudo pip install -U pip setuptools

https://stackoverflow.com/questions/44583740/no-module-named-packaging-version-for-ansible-vm-provisioning-in-azure

```
