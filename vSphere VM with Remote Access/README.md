# Cloud VM on vSphere with login/password request for remote access

The VM properties include the same fields as in the [vSphere VM with CPU&Mem](/Basic/vSphere VM with CPU&Mem) blueprint,
and the `cloudConfig` field is [VM initialization code](https://docs.vmware.com/en/vRealize-Automation/8.0/Using-and-Managing-Cloud-Assembly/GUID-70EA052D-FABF-4CE5-875D- 9B52FED08AA3.html),
containing references to the input parameters (`inputs`) of the blueprint.

The VM initialization code allows SSH password authentication while adding a new user to the
VM administrators.