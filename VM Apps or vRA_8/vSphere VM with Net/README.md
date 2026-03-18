# Cloud VM on vSphere connected to a specific network

The VM properties include the same fields as in the [vSphere VM with CPU&Mem](/Basic/vSphere VM with CPU&Mem) blueprint,
and the `networks` field contains the name of the network to which the VM should be connected. The network is described as `Cloud.vSphere.Network`, and in the properties of the network its name is specified - `dhcp`.