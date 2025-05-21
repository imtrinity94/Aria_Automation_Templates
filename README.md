# 🚀 Aria Automation Templates Collection

Welcome to the Aria Automation Templates Collection! This repository contains a curated set of VMware Aria Automation (formerly vRealize Automation) templates for various infrastructure and application deployments.

## 🎯 Quick Start

To use these templates:
1. 📥 Clone this repository
2. 🔄 Import the desired template into your Aria Automation environment
3. ⚙️ Configure the template according to your environment
4. 🚀 Deploy!

## 💡 Example Template

Here's a simple example of an Aria Automation template:

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

## 📄 List of Templates

### Application Templates
- [2-Tier CAS Demo Application](./2-Tier%20CAS%20Demo%20Application) - Two-tier application deployment template
- [3 Tier Demo Application](./3%20Tier%20Demo%20Application) - Three-tier application architecture deployment
- [CAS Demo Application](./CAS%20Demo%20Application) - Sample Cloud Assembly demonstration template
- [Blueprint Expressions Sample](./Blueprint%20Expressions%20Sample) - Examples of blueprint expressions usage
- [tito-multi-tier-with-lb](./tito-multi-tier-with-lb) - Multi-tier application with load balancing

### Load Balancing
- [Avi Load Balancer](./Avi%20Load%20Balancer) - NSX Advanced Load Balancer (Avi) integration

### AWS Services
- [aws-autoscale](./aws-autoscale) - AWS Auto Scaling Group configuration
- [aws-bitnami-artifactory](./aws-bitnami-artifactory) - Bitnami Artifactory deployment on AWS
- [aws-bitnami-tomcat](./aws-bitnami-tomcat) - Bitnami Tomcat deployment on AWS
- [aws-openfaas-node](./aws-openfaas-node) - OpenFaaS Node.js deployment on AWS
- [aws-route53-create-a-record](./aws-route53-create-a-record) - AWS Route53 DNS A record creation
- [aws-route53-create-alias-record](./aws-route53-create-alias-record) - AWS Route53 DNS alias record creation
- [aws-s3-create-bucket-object-and-policy](./aws-s3-create-bucket-object-and-policy) - S3 bucket with object and policy setup
- [aws-s3-create-policy](./aws-s3-create-policy) - AWS S3 bucket policy creation
- [aws-ubuntu-docker-host](./aws-ubuntu-docker-host) - Ubuntu Docker host on AWS

### Azure Services
- [azure-create-resource-group](./azure-create-resource-group) - Azure resource group creation
- [azure-create-storage-account](./azure-create-storage-account) - Azure storage account setup

### Infrastructure
- [Cloud Config](./Cloud%20Config) - Cloud-init configuration templates
- [Cloud VM](./Cloud%20VM) - Basic cloud VM deployment
- [Custom Username and Password](./Custom%20Username%20and%20Password) - VM deployment with custom credentials

### Container & DevOps
- [Docker Host Build - Ubuntu](./Docker%20Host%20Build%20-%20Ubuntu) - Ubuntu Docker host deployment
- [Jenkins on Docker - Ubuntu](./Jenkins%20on%20Docker%20-%20Ubuntu) - Jenkins CI/CD server
- [docker-host-cloudinit](./docker-host-cloudinit) - Docker host with cloud-init
- [harbor-host](./harbor-host) - Harbor container registry

### Kubernetes
- [k8s-create-cluster](./k8s-create-cluster) - Kubernetes cluster creation
- [k8s-create-from-yaml](./k8s-create-from-yaml) - K8s resources from YAML
- [k8s-create-namespace](./k8s-create-namespace) - Kubernetes namespace
- [k8s-create-supervisor-namespace](./k8s-create-supervisor-namespace) - Supervisor namespace

### vSphere Templates
- [vSphere Disk on Datastore](./vSphere%20Disk%20on%20Datastore) - vSphere storage configuration
- [vSphere Template Builder](./vSphere%20Template%20Builder) - vSphere template creation
- [vSphere VM Custom Spec](./vSphere%20VM%20Custom%20Spec) - Custom VM specifications
- [vSphere VM from OVA](./vSphere%20VM%20from%20OVA) - VM deployment from OVA
- [vSphere VM from Snapshot](./vSphere%20VM%20from%20Snapshot) - VM from snapshot
- [vSphere VM in Folder](./vSphere%20VM%20in%20Folder) - VM with folder organization
- [vSphere VM tagged](./vSphere%20VM%20tagged) - VM with tags
- [vSphere VM with Ansible Wrapper](./vSphere%20VM%20with%20Ansible%20Wrapper) - VM with Ansible integration
- [vSphere VM with CPU&Mem](./vSphere%20VM%20with%20CPU%26Mem) - VM with custom CPU and memory
- [vSphere VM with Disk](./vSphere%20VM%20with%20Disk) - VM with disk configuration
- [vSphere VM with Flavor](./vSphere%20VM%20with%20Flavor) - VM with predefined flavors
- [vSphere VM with Multi-Net](./vSphere%20VM%20with%20Multi-Net) - VM with multiple networks
- [vSphere VM with Net & Static IP](./vSphere%20VM%20with%20Net%20%26%20Static%20IP) - VM with static IP
- [vSphere VM with Net](./vSphere%20VM%20with%20Net) - VM with network configuration
- [vSphere VM with Remote Access](./vSphere%20VM%20with%20Remote%20Access) - VM with remote access

### Networking & Security
- [Networking & Security/App with LB](./Networking%20%26%20Security/App%20with%20LB) - Application with load balancer
- [Networking & Security/Cloud VM with NSX SG](./Networking%20%26%20Security/Cloud%20VM%20with%20NSX%20SG) - VM with NSX security groups
- [Networking & Security/Cloud VM with internal IP](./Networking%20%26%20Security/Cloud%20VM%20with%20internal%20IP) - VM with internal IP configuration
- [Networking & Security/NSX Outbound Network](./Networking%20%26%20Security/NSX%20Outbound%20Network) - NSX outbound networking
- [Networking & Security/NSX Routed Network](./Networking%20%26%20Security/NSX%20Routed%20Network) - NSX routed networking
- [Networking & Security/On-Demand NSX Networks](./Networking%20%26%20Security/On-Demand%20NSX%20Networks) - Dynamic NSX network provisioning

### Configuration Management
- [VM with Saltstack](./VM%20with%20Saltstack.yml) - Template for deploying a Windows Server VM with SaltStack configuration management integration. Includes automatic SaltStack agent installation and state file application.
- [ansible-control-machine](./ansible-control-machine) - Ansible control node
- [saltstack-add-grains](./saltstack-add-grains) - SaltStack configuration
- [VM with Saltstack](./VM%20with%20Saltstack.yml) - VM with SaltStack integration

### Storage and Volumes
- [VM with multiply disks](./VM%20with%20multiply%20disks) - Multi-disk configurations
- [volume-request-multiple-volumes](./volume-request-multiple-volumes) - Multiple volume requests

### Additional Templates
- [big-blueprint-bab](./big-blueprint-bab) - Large-scale blueprint example
- [vmw-veba](./vmw-veba) - VMware Event Broker Appliance
- [tf-aws-ec2-create-security-group-and-attach-to-instance](./tf-aws-ec2-create-security-group-and-attach-to-instance) - AWS EC2 with security group

## Contributing
Feel free to contribute by submitting pull requests with your templates and improvements. Please ensure your templates are well-documented and follow the existing format.

## License
This collection is available for use under standard open-source terms.