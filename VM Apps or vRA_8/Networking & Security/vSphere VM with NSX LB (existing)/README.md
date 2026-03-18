# Cloud VM on vSphere connected to multiple networks

The VM properties include the same fields as in the [vSphere VM with Net](/Basic/vSphere VM with Net) blueprint,
and the `networks` field contains a list of networks to which the VM should be connected. The `deviceIndex` parameter defines the index
network adapter inside the VM. It is worth noting that the network properties also indicate the [type (`networkType`) of the network](https://docs.vmware.com/en/vRealize-Automation/8.0/Using-and-Managing-Cloud-Assembly/GUID -68197096-1155-49C0-8043-D6DDE4EED28E.html),
referencing an existing network.

Existing network with a load balancer