# VCF Automation All Apps – Multi VM Service

## Overview

Deploys **several VM Service virtual machines (up to 5)** in one request into an existing **Supervisor Namespace**. The user enters a base name and how many VMs they want; the template uses `count` with `allocatePerInstance` to create one `VirtualMachine` per instance, each with a unique name and label.

---

## Template: `Multi_VM_Service.yaml`

`formatVersion: 1` Cloud Template with a counted `CCI.Supervisor.Resource`.

### Inputs

| Input | Type | Default | Description |
|---|---|---|---|
| `vm-name` | string | `vm` | Base name for the VMs |
| `count` | integer | – | Number of VMs to deploy (maximum `5`) |

### Resources

- **`CCI_Supervisor_Namespace_1`** (`CCI.Supervisor.Namespace`) – references the existing namespace `csd-namespace-01-byp23`
- **`CCI_Supervisor_Resource_1`** (`CCI.Supervisor.Resource`) – `VirtualMachine` (`vmoperator.vmware.com/v1alpha3`):
  - `count: ${input.count}` with `allocatePerInstance: true`, so each instance is evaluated separately
  - name: `<vm-name>-<count.index>-<shortDeploymentId>` (e.g. `app-0-a1b2c`, `app-1-a1b2c`, …)
  - label `vm-selector` set to the same value, so each VM can be targeted on its own (for example by a `VirtualMachineService`)
  - `className: best-effort-medium`, `imageName: vmi-f84f523a54e293552`, `storageClass: csd-dr-vks-policy`, `powerState: PoweredOn`

### Why `allocatePerInstance`

Without `allocatePerInstance: true`, expressions such as `${count.index}` are not resolved per instance, and all VMs would try to use the same name. With it, every VM gets its own index and therefore its own Kubernetes name.

---

## Before you use it

Replace the namespace (`csd-namespace-01-byp23`), VM class (`best-effort-medium`), VM image (`vmi-f84f523a54e293552`) and storage class (`csd-dr-vks-policy`) with values from your environment. Keep `vm-name` lower case so the generated names are valid Kubernetes names.
