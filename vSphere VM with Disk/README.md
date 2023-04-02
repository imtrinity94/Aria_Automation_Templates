# Cloud VM on vSphere with additional disk

The VM properties include the same fields as in the [vSphere VM with CPU&Mem](/Basic/vSphere VM with CPU&Mem) blueprint,
the disk properties include the same fields as in the [vSphere Disk](/Basic/vSphere Disk on Datastore) blueprint,
and the link here is the `attachedDisks` field of the VM object, which refers to the identifier of the virtual object
disk.