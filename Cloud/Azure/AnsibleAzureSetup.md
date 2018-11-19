# Ansible & Azure
```
ansible --version
az --version
```

[Ansible Getting Started with Azure](http://docs.ansible.com/ansible/latest/guide_azure.html)

[Install and configure Ansible to manage virtual machines in Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ansible-install-configure)

[Create a basic virtual machine in Azure with Ansible](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ansible-create-vm)

[azure_rm_virtualmachine - Manage Azure virtual machines.](http://docs.ansible.com/ansible/latest/azure_rm_virtualmachine_module.html)

# [Azure Ansible steps](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ansible-install-configure#create-azure-credentials)
* Install Ansible
* Create Azure credentials
* Create Ansible credentials file (or)
* Use Ansible environment variables
* [Create a basic virtual machine in Azure with Ansible](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ansible-create-vm)

### Create Azure credentials
```
$ az ad sp create-for-rbac --query [appId,password,tenant]
Retrying role assignment creation: 1/36
Retrying role assignment creation: 2/36
[
  "22222222-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "33333333-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "44444444-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
]


$ az account show --query [id] --output tsv
11111111-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

### Create Ansible credentials file
```
$ vi ~/.azure/credentials

$ cat ~/.azure/credentials
[default]
subscription_id=11111111-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=22222222-xxxx-xxxx-xxxx-xxxxxxxxxxxx
secret=33333333-xxxx-xxxx-xxxx-xxxxxxxxxxxx
tenant=44444444-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```


