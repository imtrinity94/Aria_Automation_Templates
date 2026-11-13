# VCF Automation All Apps – Basic VM

## Overview

The simplest **All Apps** blueprint: it deploys a single **VM Service** virtual machine into an existing **Supervisor Namespace**. The only thing the user is asked for is the VM name; everything else (VM class, image, storage policy) is fixed in the template.

Use it as a starting point to check that a namespace, VM class, VM image and storage class are working before building more complex blueprints.

---

## Template: `Basic_VM.yaml`

`formatVersion: 1` Cloud Template that deploys a `VirtualMachine` (`vmoperator.vmware.com/v1alpha3`) on a CCI Supervisor Namespace.

### Inputs

| Input | Type | Default | Description |
|---|---|---|---|
| `hostname` | string | `vm-` | Name of the virtual machine (used as `metadata.name`) |

### Resources

- **`CCI_Supervisor_Namespace_1`** (`CCI.Supervisor.Namespace`) – references the existing namespace `csd-namespace-01-byp23` (`existing: true`)
- **`Virtual_Machine_1`** (`CCI.Supervisor.Resource`) – a `VirtualMachine` with:
  - `className: best-effort-medium`
  - `imageName: vmi-f84f523a54e293552` (Photon VM image)
  - `storageClass: csd-dr-vks-policy`
  - `powerState: PoweredOn`
  - waits for the `VirtualMachineCreated` condition to be `True` before the deployment is marked complete

---

## Before you use it

Replace these environment-specific values with the ones from your own setup:

| Value | Where to find it |
|---|---|
| `csd-namespace-01-byp23` | Your Supervisor Namespace name |
| `best-effort-medium` | A VM class assigned to the namespace |
| `vmi-f84f523a54e293552` | A VM image (`vmi-…`) available in the namespace (`kubectl get vmi`) |
| `csd-dr-vks-policy` | A storage class assigned to the namespace |

The VM name must be a valid Kubernetes name (lower case letters, numbers and `-`), so change the default `vm-` to something like `vm-web01`.
