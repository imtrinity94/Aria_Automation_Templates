# Cloud VM on vSphere connected to multiple networks

The VM properties include the same fields as in the [vSphere VM with Net](/Basic/vSphere VM with Net) blueprint,
and the `networks` field contains a list of networks to which the VM should be connected. The `deviceIndex` parameter defines the index
network adapter inside the VM.