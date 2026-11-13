# VCF Automation All Apps – Kubernetes (VKS) Cluster with Dynamic Inputs

## Overview

A request-time configurable version of the **Basic K8s Cluster** blueprint. Instead of hard-coding everything, the user picks the **namespace**, **Kubernetes version**, **control plane / worker node counts** and **VM class** on the request form. The namespace list is filled in **dynamically** from the namespaces in the user's project.

Shared values (storage policy and content library) are kept in `variables:` so they only need changing in one place.

---

## Template: `K8s_Cluster_with_Dynamic_Inputs.yaml`

`formatVersion: 2` Cloud Template that deploys a `Cluster` (`cluster.x-k8s.io/v1beta1`).

### Variables

| Variable | Value | Used for |
|---|---|---|
| `datastore-policy` | `csd-dr-vks-policy` | `storageClass` cluster variable |
| `content-library` | `cl-aeb0fe241bc6134a7` | Content library the Photon node image is resolved from |

### Inputs

| Input | Type | Options / Default | Description |
|---|---|---|---|
| `namespace-name` | string | Dynamic: `$data: /data/namespaces?projectId={{project}}` | Existing Supervisor Namespace in the selected project |
| `cluster-name` | string | – | Name of the Kubernetes cluster |
| `kubernetes-version` | string | `v1.33.6---vmware.1-fips-vkr.2`, `v1.33.3---vmware.1-fips-vkr.1` | VKr (Kubernetes release) |
| `controlPlaneCount` | integer | `1` (default) or `3` | Control plane nodes – use `3` for HA |
| `WorkloadNodeCount` | integer | `1` (default) or `3` | Worker nodes |
| `VmClass` | string | `best-effort-medium`, `best-effort-large`, `best-effort-xlarge`, `best-effort-2xlarge` | VM class for the nodes |

### Resources

- **`CCI_Supervisor_Namespace_1`** (`CCI.Supervisor.Namespace`) – the namespace chosen in `namespace-name` (`existing: true`)
- **`Kubernetes_Cluster_1`** (`CCI.Supervisor.Resource`) – a `Cluster` with:
  - ClusterClass `builtin-generic-v3.3.0`
  - `version` from `kubernetes-version`
  - pod CIDR `192.168.156.0/20`, service CIDR `10.96.0.0/12`, domain `cluster.local`
  - `vmClass` and `storageClass` cluster variables from the input and variable above
  - control plane replicas from `controlPlaneCount`
  - one worker machine deployment (class `node-pool`) with replicas from `WorkloadNodeCount`
  - Photon node image resolved from the content library via the `run.tanzu.vmware.com/resolve-os-image` annotation

### Dynamic namespace list

```yaml
$data: /data/namespaces?projectId={{project}}
```

This is a built-in VCF Automation data source: when the user selects a project on the request form, the drop-down lists the Supervisor Namespaces of that project. No vRO action or custom form is needed.

---

## Before you use it

- Update the two `variables:` values for your environment
- Adjust the `kubernetes-version` and `VmClass` lists to the VKrs and VM classes that are available to your namespaces
- Check that the ClusterClass `builtin-generic-v3.3.0` exists on your Supervisor (`kubectl get clusterclass -A`); the **Basic K8s Cluster** blueprint uses `builtin-generic-v3.4.0`
- The worker pool name is fixed (`kubernetes-cluster-9w19-np-4kd5`); it only has to be unique within the cluster, so this is fine as is
- Change the pod / service CIDRs if they overlap with your networks
