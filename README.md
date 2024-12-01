# proxmox-lab
[![license](https://img.shields.io/github/license/pkretzer/proxmox-lab)](https://github.com/pkretzer/proxmox-lab/blob/main/LICENSE)

The Playbooks lets you clone or create LXC containers and update the configuration defined in the variables or clone KVM machines/templates and configure them with Cloud-Init to setup your Lab or Workshop.  
You can find examples for LXC contaners in [group_vars/container/main.yml](group_vars/container/main.yml) and for KVM in [group_vars/kvm/main.yml](group_vars/kvm/main.yml).  
Secrets are defined in the corresponding vault.yml  

## Ansible Module Docs
[Container Management Module](https://docs.ansible.com/ansible/latest/collections/community/general/proxmox_module.html)  
[KVM Management Module](https://docs.ansible.com/ansible/latest/collections/community/general/proxmox_kvm_module.html#ansible-collections-community-general-proxmox-kvm-module)  

## Important
Sadly updating the LXC container configuration isn't working as expected with all parameters, more in the comments of the examples.

## Requirements
### Python 3 pip modules
- ansible
- proxmoxer
- requests
~~~bash
pip3 install -r requirements.txt
~~~

### Proxmox API Token
You need an API Token to run this playbooks.  
You can create a new API Token for user **root@pam** and call it ansible for example, important is to not separate  
the privileges in the Token so your Token has the same permissions as the Root Account.  
If you want more security you can create separate permissions for the API Token.  
You can find more informationen in the [official documentation](https://pve.proxmox.com/pve-docs/chapter-pveum.html#pveum_tokens).

**Ansible Galaxy Collections**
~~~bash
ansible-galaxy collection install community.general
~~~

## KVM Templates
Cloud-Init must be installed on the machine you are cloning to change the configuration.  

## Playbooks
[10-create-lab-container.yml](10-create-lab-container.yml) -> Create/Clone container defined in the group_vars  
[20-create-lab-lvm.yml](20-create-lab-lvm.yml) -> Clone KVM machines defined in the group_vars  
[90-delete-lab-container.yml](90-delete-lab-container.yml) -> Delete container defined in the group_vars  when state is absent  
[91-delete-lab-kmm.yml](91-delete-lab-kmm.yml) -> Delete KVM machines defined in the group_vars  when state is absent  