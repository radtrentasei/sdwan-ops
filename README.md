# sdwan-ops

This repo is a derivative of the full CI/CD Pipeline described in the [sdwan-devops](https:github.com/ciscodevnet/sdwan-devops) aimed just at daily operational tasks.  It is based on the [Cisco SD-WAN Ansible Modules](https:github.com/ciscodevnet/ansible-viptela).

## Cloning this repository

The repository contains the Cisco SD-WAN Ansible Modules as a submodule.  To clone the repo with the submodule:
``` bash
git clone --recursive https:github.com/ciscodevnet/sdwan-ops
```
## Requirements
* ansible
* requests

### Installing requirements with pip
```
pip install -r requirements.txt
```

## Playbooks

### Export/Import Policy

The following playbooks will export both templates and policy from vmanage in there entirety into a JSON file.  In addition, they will import
both templates and policy from a JSON file into vmanage, adding only the templates and/or policy that is not already present (i.e. idempotent)

> Extra Vars:
> * `vmanage_host`: The IP address or DNS name of vmanage
> * `vmanage_user`: User with adminsitrator privileges on vmanage
> * `vmanage_password`: Password for the user specified
> * `file`: the name of the file to either export to or import from.

#### Export Templates from vmanage

``` bash
ansible-playbook export-templates.yml -e vmanage_host=192.133.178.182 -e vmanage_user=admin -e vmanage_password=admin
```

#### Export Policy from vmanage

``` bash
ansible-playbook export-policy.yml -e vmanage_host=192.133.178.182 -e vmanage_user=admin -e vmanage_password=admin
```

#### Import Templates to vmanage

``` bash
ansible-playbook import-templates.yml -e vmanage_host=192.133.178.182 -e vmanage_user=admin -e vmanage_password=admin
```

#### Import Policy to vmanage

``` bash
ansible-playbook import-policy.yml -e vmanage_host=192.133.178.182 -e vmanage_user=admin -e vmanage_password=admin
```

### Generate Feature templates

#### Generate Banner Feature templates

The following playbook will generate 4 different banner feature template on the target vManage. It will also then delete two of them.

``` bash
ansible-playbook banner-template-example.yml -e vmanage_host=192.133.178.182 -e vmanage_user=admin -e vmanage_password=admin
```

The `feature-banner` task will take as input a dict `Feature_Templates`. In case of banner feature templates the `Feature_Templates` will have a dict Banner_Templates. `Banner_Templates` is a list of dict, each dict has:


| Parameter        | Choices           | Comment  |
| ------------- |:-------------:| -----:|
| templateName      |  | mandatory |
| templateDescription     |       | mandatory   |
| login |   globalValue/variableName   |     |
| motd |   globalValue/variableName   |    |
|state |    present/absent            |       |
