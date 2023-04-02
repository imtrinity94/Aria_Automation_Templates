# Диск на хранилище vSphere

Свойства диска включают поля:
 - `name` - имя дискового ресурса
 - `type` - тип дискового ресурса
 - `capacityGb` - размер диска в ГБ (по-умолчанию = 1, минимальный размер = 1)
 - `dataStore` - дисковый ресурс (vSphere Datastore) на котором создать диск
 - `provisioningType` - [тип диска в vSphere](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.storage.doc/GUID-AC8E9C20-C05F-4FB5-A5DA-11D0A77A291B.html), возможные значения: `thick`, `thin`, `eagerZeroedThick`

**Внимание**: *данный тип ресурса не поддерживается на кластере хранилищ*. 