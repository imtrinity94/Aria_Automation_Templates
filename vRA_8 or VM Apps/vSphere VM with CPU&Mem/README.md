# Cloud VM on vSphere - basic blueprint

VM properties include the fields:
 - `name` - virtual machine name
 - `cpuCount` - number of virtual processors (minimum = 1, default = 1)
 - `totalMemoryMB` - virtual machine memory size in MB (minimum = 32, default = 1024)
 - `imageRef` - [image link](https://docs.vmware.com/en/vRealize-Automation/8.0/Using-and-Managing-Cloud-Assembly/GUID-9CBAA91A-FAAD-4409-AFFC-ACC1810E4FA5 .html) from which the virtual machine is deployed