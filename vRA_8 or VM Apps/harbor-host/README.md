### Summary
This blueprint creates an Harbor Host that can be used with Code Stream as a docker registry.
It uses cloud-init to install docker and docker-compose. It alsos download the harbor binaries to install a self-signed Harbor instance with Clair to scan docker images for vulnerabilities.

### Usage:
You need a Route 53 hosted zone to use the way it is, but you can always remove the Route 53 block from the code.  