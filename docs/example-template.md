# 📄 Example Template

This guide provides an overview of a VMware Aria Automation template, detailing its components and structure. The example template is used to deploy a simple virtual machine within a vSphere environment, demonstrating the use of various parameters and resource definitions. It is designed to be easily integrated and customized, serving as a basic starting point for more complex deployments.

## 📋 Template Breakdown

### Format Version
- **formatVersion**: Specifies the version of the template format. Here, it is set to `1`, ensuring compatibility with standard cloud automation practices.

### Inputs 
Inputs allow for customization before deployment. This template uses:
- **vm_name**: Sets the virtual machine’s name. The default is `my-vm`, but it can be changed.
- **cpu_count**: Determines the number of CPUs, with a default value of `2`. This can be adjusted from `1` to `8`.

### Resources
Resources are key components of the deployment:
- **Cloud_Machine**: Represents the VM to be provisioned. Key properties are:
  - **name**: Taken from the `vm_name` input.
  - **cpuCount**: Adjusted through the `cpu_count` input.
  - **image**: Uses `ubuntu-20.04` as the base operating system.
  
- **Cloud_Network**: Defines the network configuration, set to use an existing network type.

This template provides a straightforward approach to VM deployment, which can be expanded based on specific project needs.