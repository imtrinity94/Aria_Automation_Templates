Пример шаблона с балансировщиком.
Балансирощик был использован в для задачи port translation, поскольку в vRA8 в схеме с NAT сетью реализовано только SNAT.
Конфигурация "приватной" сети статична и она также прописана в шаблоне, а не берется из Network Profile.
Для понимания того, как vRA8 работает с NSX смотрите серию статей: https://blogs.vmware.com/management/2019/04/network-automation-cloud-assembly-and-nsx-part-1.html