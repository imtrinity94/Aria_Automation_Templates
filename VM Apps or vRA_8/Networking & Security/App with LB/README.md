An example of a template with a balancer.
The balancer was used for the port translation task, since in vRA8 only SNAT is implemented in the scheme with a NAT network.
The "private" network configuration is static and it is also written in the template, and is not taken from the Network Profile.
For an understanding of how vRA8 works with NSX see the article series: https://blogs.vmware.com/management/2019/04/network-automation-cloud-assembly-and-nsx-part-1.html