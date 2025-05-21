# Collection of vRA Cloud Assembly Cloud Templates

A comprehensive collection of VMware Aria Automation (formerly vRA) Cloud Assembly templates for various infrastructure and application deployments. Help make it even bigger by contributing. Built with love.

## Table of Contents

### Application Templates
- [2-Tier CAS Demo Application](./2-Tier%20CAS%20Demo%20Application)
  - Deploys a two-tier application with frontend and API tiers
  - Supports multiple cloud environments (AWS, vSphere, Azure, VMC, GCP)
  - Includes load balancer for large deployments
  - Automated NGINX and Node.js setup

- [3 Tier Demo Application](./3%20Tier%20Demo%20Application)
  - Three-tier architecture with frontend, API, and database layers
  - Cloud-agnostic deployment across multiple platforms
  - Includes database tier with PostgreSQL
  - Advanced cloud-init configuration for each tier

### Load Balancing
- [Avi Load Balancer](./Avi%20Load%20Balancer)
  - NSX Advanced Load Balancer (Avi) integration
  - Includes health monitoring and persistence profiles
  - Automated virtual service configuration
  - Support for multiple web servers with least connection algorithm

### Cloud Infrastructure
- [Cloud Config](./Cloud%20Config) - Cloud-init configuration templates for automated VM setup
- [Cloud VM](./Cloud%20VM) - Basic cloud VM deployment with customizable specifications
- [Custom Username and Password](./Custom%20Username%20and%20Password) - Secure VM deployment with credential management

### AWS Specific Templates
- [aws-autoscale](./aws-autoscale)
  - AWS Auto Scaling Group configuration
  - Dynamic resource scaling based on CPU utilization
  - Customizable scaling policies and thresholds
  - Support for multiple instance types

### Kubernetes
- [k8s-create-cluster](./k8s-create-cluster)
  - Kubernetes cluster deployment automation
  - Enterprise PKS integration
  - Customizable cluster naming and configuration
  - Automated node management

### vSphere Specific
- [vSphere VM Custom Spec](./vSphere%20VM%20Custom%20Spec)
  - Customized VM deployment for vSphere
  - OS customization specification integration
  - Resource allocation control
  - Automated guest OS customization

### Operating Systems Templates
- [Operating Systems - Multiple](./Operating%20Systems%20-%20Multiple)
  - CentOS templates with various configurations
  - Windows 2016 deployment options
  - Network and security group integration
  - Multi-machine deployment capabilities

### Networking & Security
- [Networking & Security](./Networking%20%26%20Security)
  - NSX-T integration templates
  - Security group configurations
  - Load balancer setups
  - Network isolation and routing

### Container & DevOps
- [Docker Host Build - Ubuntu](./Docker%20Host%20Build%20-%20Ubuntu) - Automated Docker host deployment
- [Jenkins on Docker - Ubuntu](./Jenkins%20on%20Docker%20-%20Ubuntu) - CI/CD environment setup
- [harbor-host](./harbor-host) - Container registry deployment

### Database
- [Postgres Custom Database](./Postgres%20Custom%20Database) - PostgreSQL database deployment and configuration

### Storage
- [VM with multiply disks](./VM%20with%20multiply%20disks) - Multi-disk VM configurations
- [vSphere Disk on Datastore](./vSphere%20Disk%20on%20Datastore) - vSphere storage management

### Configuration Management
- [ansible-control-machine](./ansible-control-machine) - Ansible automation controller setup
- [saltstack-add-grains](./saltstack-add-grains) - SaltStack configuration management

### Remote Access
- [RemoteAccess with SSH Key](./RemoteAccess%20with%20SSH%20Key) - Secure SSH access configuration
- [ssh-access-all-types](./ssh-access-all-types) - Various SSH authentication methods

## Contributing
Feel free to contribute by submitting pull requests with your templates and improvements. Please ensure your templates are well-documented and follow the existing format.

## License
This collection is available for use under standard open-source terms.