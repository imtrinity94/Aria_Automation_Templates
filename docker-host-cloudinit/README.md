### Author(s)
  - Grant Orchard

### Summary
This blueprint creates a Docker host that can be used for many functions, including a valid endpoint for Codestream to use as part of its CI Workspace.

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