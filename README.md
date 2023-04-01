# Блюпринты

Здесь мы будем выкладывать шаблоны сервисов из наших проектов.
Кроме того, очень хорошая подборка приверов есть у Cody De Arkland: 
https://gitlab.com/codydearkland/cas-blueprints

# Список блюпринтов в репозитории

## Базовые блюпринты
- [Облачная ВМ](Basic/Cloud VM) - простая облачная виртуальная машина
- [vSphere Диск](Basic/vSphere Disk on Datastore) - диск на датасторе vSphere
- [vSphere ВМ с диском](Basic/vSphere VM with Disk) - виртуальная машина на vSphere с дополнительным диском
- [vSphere ВМ с Flavor](Basic/vSphere VM with Flavor) - облачная ВМ на vSphere с указанием обобщённого типа ресурсов (flavor)
- [vSphere ВМ с ЦПУ/Памятью](Basic/vSphere VM with CPU&Mem) - облачная ВМ на vSphere с указанием количества ЦПУ и объёма памяти
- [vSphere ВМ из OVA](Basic/vSphere VM from OVA) - виртуальная машина на vSphere, развёрнутая из OVA-файла
- [vSphere ВМ из снапшота](Basic/vSphere VM from Snapshot) - виртуальная машина на vSphere, созданная из снапшота (linked clone)
- [vSphere ВМ в папке](Basic/vSphere VM in Folder) - виртуальная машина на vSphere, которая при разворачивании будет помещена в определённую папку
- [vSphere ВМ с кастомизацией](Basic/vSphere VM Custom Spec) - виртуальная машина на vSphere с использованием кастомизации
- [vSphere ВМ с тэгами](Basic/vSphere VM tagged) - виртуальная машина на vSphere с установленными тэгами
- [vSphere ВМ подключённая к сети](Basic/vSphere VM with Net) - виртуальная машина на vSphere, подключённая к сети
- [vSphere ВМ подключённая к нескольким сетям](Basic/vSphere VM with Multi-Net) - виртуальная машина на vSphere, подключённая к нескольким сетям
- [vSphere ВМ со статическим адресом](Basic/vSphere VM with Net & Static IP) - виртуальная машина на vSphere, подключённая к сети и использующая статическое назначение IP-адреса
- [vSphere ВМ с параметрами](Basic/vSphere VM with Remote Access) - виртуальная машина на vSphere с запросом входных параметров (логин/пароль) для активации удалённого доступа

## Сетевые блюпринты
to be continued...

# Как установить блюпринт

# Полезные ссылки

- [Интеграция блюпринтов с Gitlab](https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-069B2BC6-3DCF-4E9A-8664-32E28CAF90CD.html)
- [Описание схемы блюпринта](https://code.vmware.com/apis/894/vrealize-automation-resource-type-schema)
- [Синтаксис выражений и функций блюпринта](https://docs.vmware.com/en/vRealize-Automation/8.0/Using-and-Managing-Cloud-Assembly/GUID-12F0BC64-6391-4E5F-AA48-C5959024F3EB.html)
- [Официальный репозиторий примеров](https://github.com/vmware-samples/cloud-automation-samples/)