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

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
