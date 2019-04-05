aks-deployment
=========

A brief description of the role goes here.

Requirements
------------
At this time your local deployment host need the following prerequisites:

```
* kubectl
* helm
* az
```
Also python module
```
pip install ansible[azure]
pip install openshift
```
Note: If you are using MacOsx space the brackets

```
pip install ansible\[azure\] --user
```

In addition, you should create an azure temporal account. Go to portal.azure.com and create a service principal or via azure CLI , login with your email and password and run the following command:

```
az ad sp create-for-rbac -n "aks-deployment-user" --role owner --scope subscriptions/id-of-subscription --password 'insert-password'
```
To get information about suscription
```
az account list
```

Now export the following variables to environment
```
export AZURE_SUBSCRIPTION_ID=<your-subscription_id>
export AZURE_CLIENT_ID=<security-principal-appid>
export AZURE_SECRET=<security-principal-password>
export AZURE_TENANT=<security-principal-tenant>
```

Role Variables
--------------
Initial var to execution:
* hosted_on=aks 
* deployment_enviroment=dev

Current Support Vars:
```yaml
region:
  name: eastus2

resource_group:
  name: aks-poc

vnet:
  name: aks-vnet
  address_prefixes_cidr: 10.80.0.0/22
  dns: 8.8.8.8
  tag: testing

subnet:
  name: aks-subnet
  virtual_network_name: "{{ vnet.name }}"
  address_prefix_cidr: 10.80.0.0/24

aks:
  name: "aks-poc"
  dns_prefix: "poc"
  linux_profile:
    username: poc_claro
    ssh_key: "/Users/user/.ssh/id_rsa.pub"
  agent_pool_profiles:
    name: default
    count: 2
    vm_size: Standard_D2_v2
  auth_source: "cli"
  tag: "poc"
```
Dependencies
------------
* Service Principal Client ID
* Service Principal Password

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:
```yaml
---
- hosts: k8s-{{ hosted_on }}-{{ deployment_enviroment }}
  connection: local
  gather_facts: yes  
  tasks:
  - import_role:
       name: aks-deployment
```
host file

```
[k8s-aks-dev]
localhost
```

```bash
ansible-playbook site.yaml -i hosts -e 'hosted_on=aks' -e 'deployment_enviroment=dev'
```

License
-------

BSD

Author Information
------------------
Author: Jesus Sanchez
