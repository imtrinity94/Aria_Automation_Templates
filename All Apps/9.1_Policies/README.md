# VCF Automation 9.1 – Infrastructure Policies

## Overview

**Infrastructure Policies** are a new feature in VCF Automation 9.1 that allow workloads to be placed on specific compute hosts by linking a **vCenter Compute Policy** to a deployment. Policies are applied conditionally using **Policy Enforcement Criteria** based on Guest OS, OS Family, or Labels.

This template demonstrates how to use boolean inputs (`drPolicy`, `oraclePolicy`) to dynamically apply compute policies at deploy time via the `policies` field in a `VirtualMachine` manifest.

---

## UI Reference

![New Infrastructure Policy – VCF Automation Provider Management](image.png)

**Navigation:** `Provider Management → Infrastructure → Infrastructure Policies → New`

| Field | Description |
|---|---|
| **Name** | Policy identifier (e.g. `disaster-recovery`) |
| **Description** | Optional description |
| **vCenter Compute Policy** | The vSphere Compute Policy to enforce |
| **Mandatory Policy** | Apply policy to all workloads in the assigned region |
| **Policy Enforcement Criteria** | Rules to match workloads (e.g. `GuestOS EQUALS "Linux" AND Label[AZ-1] EXISTS`) |

---

## Template: `VCFA_9.1_Policies.yaml`

A VCF Automation Cloud Template deploying a `VirtualMachine` on a CCI Supervisor Namespace with optional policy assignment.

### Inputs

| Input | Type | Description |
|---|---|---|
| `namespace` | string | Target Supervisor Namespace |
| `storageClass` | string | Storage class for the VM |
| `vm_size` | string | VM size class (default: `best-effort-medium`) |
| `vm_image` | string | OS image — Ubuntu 24.04 or Windows Server 2022 |
| `drPolicy` | boolean | Place VM on Disaster Recovery host (default: `true`) |
| `oraclePolicy` | boolean | Place VM on Oracle licensed host (default: `false`) |

### Resources

- **`CCI.Supervisor.Namespace`** — references an existing namespace
- **`CCI.Supervisor.Resource`** — deploys a `VirtualMachine` (`vmoperator.vmware.com/v1alpha5`) with:
  - `className`, `imageName`, `storageClass` driven by inputs
  - `policies` field dynamically set based on `drPolicy` / `oraclePolicy` booleans, referencing `ComputePolicy` objects (`disaster-recovery`, `oracle`)

### Policy Assignment Logic

```yaml
policies: '${(input.drPolicy || input.oraclePolicy) ? 
  [ (input.drPolicy ? {"apiVersion":"...","kind":"ComputePolicy","name":"disaster-recovery"} : null),
    (input.oraclePolicy ? {"apiVersion":"...","kind":"ComputePolicy","name":"oracle"} : null) 
  ] : null}'
```

The `policies` field accepts a list of `ComputePolicy` references. Conditional expressions ensure only the selected policies are applied.