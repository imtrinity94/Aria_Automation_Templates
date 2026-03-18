# How to Create a Project Using the Aria Automation Templates Collection

## Overview

The Aria Automation Templates Collection offers a set of VMware Aria Automation templates for various infrastructure and application deployments. This guide will show you how to use these templates in your project.

## Prerequisites

- An active VMware Aria Automation environment
- Basic knowledge of YAML and infrastructure deployment
- Access to a Git repository management tool

## Step-by-Step Guide

### Step 1: Clone the Repository

Start by cloning the Aria Automation Templates Collection repository. It contains various templates that you can customize for your project.

```bash
git clone <repository-url>
```

### Step 2: Import the Template

Navigate to the desired template within the cloned repository and import it into your Aria Automation environment. This will allow you to use predefined configurations and components, simplifying the deployment process.

### Step 3: Configure the Template

After importing, adjust the template to fit your environment's needs. Pay special attention to the inputs and resources sections to ensure the template meets your requirements. 🎯

#### Example: Modify a Sample Template

Here’s an example of an Aria Automation template:

```yaml
formatVersion: 1
inputs:
  vm_name:
    type: string
    title: VM Name
    default: my-vm
  cpu_count:
    type: integer
    title: CPU Count
    default: 2
    minimum: 1
    maximum: 8
resources:
  Cloud_Machine:
    type: Cloud.vSphere.Machine
    properties:
      name: ${input.vm_name}
      flavor: small
      image: ubuntu-20.04
      cpuCount: ${input.cpu_count}
      networks:
        - network: ${resource.Cloud_Network.id}
  Cloud_Network:
    type: Cloud.Network
    properties:
      networkType: existing
```

Update values like `vm_name`, `cpu_count`, or network settings to customize the template.

### Step 4: Deploy the Template

Once your template is configured, deploy it in your Aria Automation environment. This step converts your configuration into a cloud deployment, automating the creation of virtual machines, networks, and other resources. 🚀

## Additional Resources

Explore more templates in the collection to support different use cases, from basic VM deployments to complex multi-tier applications and specific cloud services, including AWS and Azure.

- **AWS Services:** Templates like `aws-autoscale` and `aws-bitnami-tomcat` assist in AWS integrations.
- **Azure Services:** Templates such as `azure-create-resource-group` help with Azure provisioning.
- **Kubernetes:** Use templates like `k8s-create-cluster` for Kubernetes configurations.

## Conclusion

By following this guide, you've learned how to use the Aria Automation Templates Collection for faster infrastructure and application deployment. Whether you’re deploying a multi-tier application or setting up a Kubernetes cluster, these templates are versatile tools. Happy deploying! 🎉

## Contribute

You can improve the collection by submitting your templates or enhancements through pull requests. Make sure your contributions are well-documented and consistent with existing formats.

## Licensing

This template collection is provided under standard open-source terms.