# Облачная ВМ на vSphere - базовый блюпринт

Свойства ВМ включают поля:
 - `name` - имя виртуальной машины
 - `cpuCount` - количество виртуальных процессоров (минимум = 1, по-умолчанию = 1)
 - `totalMemoryMB` - объём памяти виртуальной машины в МБ (минимум = 32, по-умолчанию = 1024) 
 - `imageRef` - [ссылка на образ](https://docs.vmware.com/en/vRealize-Automation/8.0/Using-and-Managing-Cloud-Assembly/GUID-9CBAA91A-FAAD-4409-AFFC-ACC1810E4FA5.html) из которого разворачивается виртуальная машина