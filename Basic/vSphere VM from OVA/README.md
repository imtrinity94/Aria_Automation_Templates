# Облачная ВМ на vSphere из OVA

Свойства ВМ включают те же поля, что и в блюпринте [vSphere ВМ с ЦПУ/Памятью](/Basic/vSphere VM with CPU&Mem),
а поле `imageRef` является ссылкой на расположение OVA-файл.

Например, можно использовать следующие ссылки:
- Ubuntu 16.04 LTS: https://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64.ova
- Ubuntu 18.04 LTS: https://cloud-images.ubuntu.com/releases/bionic/release/ubuntu-18.04-server-cloudimg-amd64.ova 
- Ubuntu 19.04 LTS: https://cloud-images.ubuntu.com/releases/disco/release/ubuntu-19.04-server-cloudimg-amd64.ova
- VMware Photon OS 2.0: https://bintray.com/vmware/photon/download_file?file_path=2.0%2FGA%2Fova%2Fphoton-custom-hw11-2.0-304b817.ova
- VMware Photon OS 3.0: https://bintray.com/vmware/photon/download_file?file_path=3.0%2FGA%2Fova%2Fphoton-hw13_uefi-3.0-26156e2.ova
- CentOS 7: https://cloud.centos.org/centos/7/vagrant/x86_64/images/centos-7-atomicapp-dev-1-1.x86_64.vsphere.ova
- FreeBSD 10: https://liquidtelecom.dl.sourceforge.net/project/virtualappliances/BSD/FreeBSD/FreeBSD-10.1-i386-minimal.ova 