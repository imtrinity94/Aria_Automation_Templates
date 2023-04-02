# Disk on vSphere storage

The disk properties include the fields:
  - `name` - disk resource name
  - `type` - disk resource type
  - `capacityGb` - disk size in GB (default = 1, minimum size = 1)
  - `dataStore` - disk resource (vSphere Datastore) on which to create a disk
  - `provisioningType` - [disk type in vSphere](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.storage.doc/GUID-AC8E9C20-C05F-4FB5-A5DA- 11D0A77A291B.html), possible values: `thick`, `thin`, `eagerZeroedThick`

**Note**: *this resource type is not supported on a storage cluster*.