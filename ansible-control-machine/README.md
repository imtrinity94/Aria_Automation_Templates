### Author(s)
  - Grant Orchard

### Summary
This blueprint creates an Ansible Control Machine that can be used with Cloud Assembly.
It uses the cloud-init "write_file" directive to create a playbook that is used to configure the host to be compliant with the requirements of Cloud Assembly.

### Usage:
You will note that there is no user creation block in cloud-init. I've moved to placing user creation under image profiles, however if you need to add this to your cloud-init block, the syntax is as follows:
```
users:
  - name: "${inputs.username}"
    ssh-authorized-keys:
     - "${inputs.ssh_public_key}"
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    groups: sudo
    shell: /bin/bash
```