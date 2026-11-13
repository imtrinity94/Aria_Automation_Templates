# VCF Automation All Apps – Basic Kubernetes (VKS) Cluster

## Overview

Deploys a **vSphere Kubernetes Service (VKS) cluster** into an existing **Supervisor Namespace** using the Cluster API `Cluster` object and the built-in **ClusterClass**. The user only enters a cluster name; the size, version and networking are fixed in the template.

The result is a small cluster with **1 control plane node and 1 worker node** running Photon OS – good for a quick test or a demo.

---

## Template: `Basic_K8s_Cluster.yaml`

`formatVersion: 1` Cloud Template that deploys a `Cluster` (`cluster.x-k8s.io/v1beta1`).

### Inputs

| Input | Type | Default | Description |
|---|---|---|---|
| `clusterName` | string | `k8s-cluster-` | Cluster name prefix. The final name is `<clusterName>-<shortDeploymentId>`, so every deployment gets a unique name |

### Resources

- **`CCI_Supervisor_Namespace_1`** (`CCI.Supervisor.Namespace`) – references the existing namespace `csd-namespace-01-byp23`
- **`Kubernetes_Cluster_1`** (`CCI.Supervisor.Resource`) – a `Cluster` with:

| Setting | Value |
|---|---|
| ClusterClass | `builtin-generic-v3.4.0` from namespace `vmware-system-vks-public` |
| Kubernetes version (VKr) | `v1.33.6---vmware.1-fips-vkr.2` |
| Pod CIDR | `192.168.156.0/20` |
| Service CIDR | `10.96.0.0/12` |
| Service domain | `cluster.local` |
| VM class (all nodes) | `best-effort-medium` |
| Storage class | `csd-dr-vks-policy` |
| Control plane replicas | `1` |
| Worker pool | class `node-pool`, name `worker-<shortDeploymentId>`, `1` replica |
| Node OS image | Photon, resolved from content library `cl-aeb0fe241bc6134a7` via the `run.tanzu.vmware.com/resolve-os-image` annotation |

---

## Before you use it

Replace these values with the ones from your environment:

- Namespace `csd-namespace-01-byp23`
- ClusterClass `builtin-generic-v3.4.0` and the VKr version – check what your Supervisor offers (`kubectl get clusterclass -n vmware-system-vks-public`, `kubectl get kr`)
- VM class `best-effort-medium` and storage class `csd-dr-vks-policy`
- Content library ID `cl-aeb0fe241bc6134a7` (the library that holds the VKr images)
- Pod / service CIDRs, if they overlap with networks in your environment

Once the cluster is ready, get the kubeconfig from the deployment in VCF Automation or with the `vcf` CLI.
