# Building a Multi-Tier Web Application with Aria Automation Templates

In this tutorial, we'll use Aria Automation Templates to create a multi-tier web application infrastructure that includes load balancing. We will work with the `tito-multi-tier-with-lb` template to deploy an architecture using VMware Aria Automation.

## Prerequisites

Before starting, make sure you have:
- An active VMware Aria Automation environment.
- Basic knowledge of YAML and cloud infrastructure.

## Step-by-Step Guide

### Step 1: Clone the Repository

First, clone the Aria Automation Templates Collection repository to your local environment to access the templates:

```bash
git clone https://github.com/<username>/aria-automation-templates.git
cd aria-automation-templates
```

### Step 2: Import the Template

Navigate to the `tito-multi-tier-with-lb` template location.

In your Aria Automation:
1. Go to the **Design** tab.
2. Click on **Import Blueprint**.
3. Select the `tito-multi-tier-with-lb` YAML file.

### Step 3: Configure the Template

After importing, configure the template parameters to suit your environment. Key configurations include:

- **VM Naming**: Change `vm_name` to your preferred naming convention.
- **CPU and Memory**: Set `cpu_count` to meet your system needs.
- **Network Configuration**: Ensure `Cloud_Network` settings match your network setup.

#### Example Configuration

```yaml
inputs:
  vm_name:
    type: string
    title: VM Name
    default: web-tier-vm
  cpu_count:
    type: integer
    title: CPU Count
    default: 4
resources:
  Cloud_Machine:
    type: Cloud.vSphere.Machine
    properties:
      name: ${input.vm_name}
      flavor: medium
      image: ubuntu-20.04
      cpuCount: ${input.cpu_count}
      networks:
        - network: ${resource.Cloud_Network.id}
  Cloud_Network:
    type: Cloud.Network
    properties:
      networkType: existing
```

### Step 4: Deploy the Template

Once you've customized the template, deploy it:

1. Click on the **Deploy** button in the blueprint designer.
2. Monitor the deployment progress from the **Deployments** tab.

⏳ **Note:** Deployment times can vary depending on infrastructure and template complexity.

### Step 5: Verify the Deployment

After deployment, verify that all components are working properly:

- Check the VMs.
- Ensure the load balancer directs traffic correctly across application tiers.

## Additional Use Cases

The Aria Automation Templates are versatile. Consider these additional uses:

- **CI/CD Pipelines**: Use the `Jenkins on Docker - Ubuntu` template to set up a Jenkins server.
- **Cloud Infrastructure**: Automate AWS S3 bucket creation with the `aws-s3-create-bucket-object-and-policy` template.
- **Kubernetes Deployments**: Create complete Kubernetes clusters using the `k8s-create-cluster` template.
- **Network Security**: Configure NSX routed networks with `NSX Routed Network`.

These templates help streamline complex deployments, allowing for further customization to fit specific project requirements. 🚀