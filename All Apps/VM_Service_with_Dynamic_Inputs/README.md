# VCF Automation All Apps – VM Service with Dynamic Inputs

## Overview

A fuller **VM Service** blueprint that shows several VCF Automation features in one template. Its standout feature is a **custom, live-updating Overview tab** on the deployment page.

- ⭐ **Custom Overview tab** – the `__deploymentOverview` output adds an **Overview** tab to the deployment in the VCF Automation UI, showing the end user a styled summary of their VM and how to connect to it. It **stays up to date** as the deployment changes (see [below](#-the-overview-tab))
- **Dynamic drop-downs** for the namespace and the VM class
- An **auto-generated hostname** built from the requesting user's name and the deployment ID
- **cloud-init** guest customisation (users, password, timezone, FQDN, package updates) passed through a Kubernetes **Secret**
- An **optional SSH load balancer** (public IP) controlled by a single checkbox

---

## ⭐ The Overview tab

This is what makes the blueprint special. Any output named **`__deploymentOverview`** is not shown as a normal output: VCF Automation renders it as a separate **Overview** tab on the deployment, so the end user gets a ready-made "what did I get and how do I use it" page without any custom UI work.

### What the user sees

- A **Virtual Machines** table: name, hostname, domain, status, power state, zone, internal IP, public IP and VM class
- Colour-coded badges – e.g. a green **Ready** status and a blue VM-class label
- An **SSH** section with the exact login to use: the load balancer IP when *Assign public IP* was ticked, otherwise `vmware@<internal IP>`
- A disclaimer that the IP may take a minute to appear

### How it is built

The output `value` is a **Markdown** string, and Markdown can contain **HTML**, so the template mixes both:

| Technique | Example in the template | Purpose |
|---|---|---|
| Markdown headings / quotes | `## VM Service deployment`, `> **Disclaimer**` | Page structure |
| HTML table with UI CSS classes | `<table class="table">` | Table styled like the rest of the VCF Automation UI |
| Label classes | `<span class="label label-success">`, `label-info` | Coloured status / class badges |
| Live resource placeholders | `{{resource.linux_vm.object.status.network.primaryIP4}}` | Values read from the deployed Kubernetes object |
| Template expressions and conditions | `%{if input.expose-ssh == true} … %{else} … %{endif}`, `${resource.loadbalancer[*]…ip[0]}` | Show different content depending on the request inputs |

### Why it updates by itself

The `{{resource.<name>.object.…}}` placeholders point at the **live** VM object (`spec` and `status` of the `VirtualMachine`), not at values copied at request time. So when the deployment changes, the Overview tab reflects it, for example:

- the internal IP appearing once the VM gets an address
- the power state changing after a power off / on
- the VM class changing after a resize

Any field of the VM object can be added to the page the same way, so the tab is easy to extend with extra columns or sections.

> As the comments at the top of the YAML say, this is an **MVP / POC blueprint** to showcase capabilities, not a production-ready template. It was written for VCF Automation **9.0.2**, where some values cannot yet be fetched dynamically and must be entered in `variables:`.

---

## Template: `VM_Service_with_Dynamic_Inputs.yaml`

`formatVersion: 2` Cloud Template.

### Inputs

| Input | Type | Options / Default | Description |
|---|---|---|---|
| `namespace-name` | string | Dynamic: `$data: /data/namespaces?projectId={{project}}` | Existing Supervisor Namespace in the selected project |
| `vm-class` | string | Dynamic: `$data: /data/virtualmachineclasses?namespace={{namespace-name}}`, default `best-effort-xsmall` | VM classes available in the selected namespace |
| `vm-image` | string | `Photon-5.0` → `vmi-f84f523a54e293552` | VM image (cloud-init enabled) |
| `expose-ssh` | boolean | – | **Assign public IP** – creates an SSH load balancer for the VM |

### Variables

| Variable | Value | Description |
|---|---|---|
| `hostname` | `${substring(to_lower(split(env.requestedBy, '.')[0] + '-' + env.shortDeploymentId), 0, 14)}` | First part of the requester's username + deployment ID, lower case, max 14 chars |
| `user` | `${split(env.requestedBy, '@')[0]}` | Requester's username without the domain |
| `domain` | `fiscnet.ro` | DNS domain of the VM |
| `timezone` | `Europe\Bucharest` | Guest timezone |
| `nameserver01` / `nameserver02` | `10.253.9.11` / `10.253.9.12` | DNS servers |

### Resources

| Resource | Kind | What it does |
|---|---|---|
| `namespace` | `CCI.Supervisor.Namespace` | The namespace chosen in `namespace-name` (`existing: true`) |
| `secret` | `v1` `Secret` – `vm-<hostname>-bootstrap-secret` | Holds the `cloud-config` used to customise the guest |
| `loadbalancer` | `VirtualMachineService` (`v1alpha3`) – `lb-<hostname>` | `type: LoadBalancer`, TCP 22 → 22. `count` is `1` when `expose-ssh` is ticked, otherwise `0` (not created) |
| `linux_vm` | `VirtualMachine` (`v1alpha3`) – `vm-<hostname>` | VM with the selected class and image, storage class `csd-dr-vks-policy`, hostname / domain / DNS / search domain set under `spec.network`, and cloud-init bootstrap from the secret. `dependsOn` the secret and load balancer, and waits for `VirtualMachineCreated = True` |

The VM carries the label `vm-lb-selector: vm-<hostname>`, which is exactly what the load balancer's `selector` matches, so SSH traffic reaches this VM.

### cloud-init (from the Secret)

- Sets `timezone` and `fqdn` (`<hostname>.<domain>`)
- Enables SSH password login (`ssh_pwauth: true`)
- Sets the password for `root` and creates a `vmware` user with passwordless `sudo`
- Runs `package_update` / `package_upgrade` and reboots only if `/var/run/reboot-required` exists

Default password for `root` and `vmware` is **`VMware123!`** (stored as an MD5-crypt hash, because VCF Automation 9.0.2 has no `bcrypt()` function). **Change it** before using the blueprint anywhere beyond a lab.

### Outputs

| Output | Description |
|---|---|
| `__deploymentOverview` | Renders the custom **Overview** tab described [above](#-the-overview-tab) |

---

## Before you use it

- Update everything under `variables:` (domain, timezone, DNS servers) for your environment
- Update the `vm-image` options with the `vmi-…` IDs of your own cloud-init–ready Linux images (Ubuntu `-cloudimg-` images and all Photon images work)
- Change `storageClass: csd-dr-vks-policy` to a storage class assigned to your namespaces
- Replace the password hash in the Secret with your own
- `expose-ssh` needs a namespace network that can allocate load balancer IPs
