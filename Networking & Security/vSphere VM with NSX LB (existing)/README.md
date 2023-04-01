# Облачная ВМ на vSphere, подключённая к нескольким сетям

Свойства ВМ включают те же поля, что и в блюпринте [vSphere ВМ подключённая к сети](/Basic/vSphere VM with Net),
а поле `networks` содержит список сетей, к которым следует подключить ВМ. Параметр `deviceIndex` определяет индекс
сетевого адаптера внутри ВМ. Стоит обратить внимание, что в свойствах сети так же указан [тип (`networkType`) сети](https://docs.vmware.com/en/vRealize-Automation/8.0/Using-and-Managing-Cloud-Assembly/GUID-68197096-1155-49C0-8043-D6DDE4EED28E.html),
ссылающийся на существующую сеть.

Existing network with a load balancer