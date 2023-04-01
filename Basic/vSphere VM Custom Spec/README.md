# Облачная ВМ на vSphere с использованием кастомизации

Свойства ВМ включают те же поля, что и в блюпринте [vSphere ВМ с ЦПУ/Памятью](/Basic/vSphere VM with CPU&Mem),
а поле `customizationSpec` является именем настроек ([Customization Specification](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.vm_admin.doc/GUID-EB5F090E-723C-4470-B640-50B35D1EC016.html)), которые необходимо применить
при разворачивании ВМ. Описание настроек должно присутствовать на vCenter, в котором разворачивается ВМ.