# VCF Automation All Apps – VM Service with Load Balancer

## Overview

Deploys a **VM Service** virtual machine into an existing **Supervisor Namespace** and, alongside it, a **`VirtualMachineService` of type `LoadBalancer`** that publishes **SSH (TCP 22)**. The load balancer gets an external IP from the namespace's network (NSX / VPC / Avi), so the VM can be reached from outside the namespace, for example from a jump server.

---

## Template: `VM_Service_with_LoadBalancer.yaml`

`formatVersion: 1` Cloud Template with two `CCI.Supervisor.Resource` objects in the same namespace.

### Inputs

| Input | Type | Default | Description |
|---|---|---|---|
| `hostname` | string | `vm-` | Name of the virtual machine; the load balancer is named `lb-<hostname>` |

### Resources

- **`CCI_Supervisor_Namespace_1`** (`CCI.Supervisor.Namespace`) – references the existing namespace `csd-namespace-01-byp23`
- **`Virtual_Machine_1`** – `VirtualMachine` (`vmoperator.vmware.com/v1alpha3`):
  - `className: best-effort-medium`, `imageName: vmi-f84f523a54e293552`, `powerState: PoweredOn`
  - `storageClass: csd-dr-vks-policy-latebinding` (the *late-binding* / `WaitForFirstConsumer` variant of the storage class)
  - waits for `VirtualMachineCreated = True`
- **`LoadBalancer`** – `VirtualMachineService` (`vmoperator.vmware.com/v1alpha3`):
  - `type: LoadBalancer`
  - port `ssh`: TCP `22` → target port `22`
  - `selector` used to pick the backend VM(s)

### How the load balancer finds the VM

A `VirtualMachineService` sends traffic to the VMs whose **labels** match its `spec.selector`. Check the external IP once it's deployed:

```bash
kubectl get virtualmachineservice lb-<hostname> -n <namespace>
```

> **Note:** In this template the VM has no `metadata.labels`, and the selector key is written as `vm-lb-selector-$/input.hostname: null`. If the load balancer comes up with no endpoints, give the VM a label and point the selector at it, for example `vm-lb-selector: ${input.hostname}` on both. The **VM Service with Dynamic Inputs** blueprint in this folder shows that pattern.

---

## Before you use it

Replace `csd-namespace-01-byp23`, `best-effort-medium`, `vmi-f84f523a54e293552` and `csd-dr-vks-policy-latebinding` with the namespace, VM class, VM image and storage class from your environment. The namespace needs a network that can hand out load balancer IPs.
