## Клиент iSCSI

Посмотреть какие сейчас устройства подключены можно через каталог
`/dev/disk/by-path`:

```
core@coreos1 ~ $ ls -l /dev/disk/by-path/
total 0
lrwxrwxrwx. 1 root root 9 Jun 18 12:48 ip-10.10.246.104:3260-iscsi-iqn.2005-10.nas2:1-lun-0 -> ../../sdc
lrwxrwxrwx. 1 root root 9 Jun 21 09:53 ip-10.10.246.104:3260-iscsi-iqn.2005-10.nas2:docker-lun-0 -> ../../sde
lrwxrwxrwx. 1 root root 9 Jun 18 12:46 ip-10.10.254.104:3260-iscsi-iqn.2005-10.nas2:1-lun-0 -> ../../sda
lrwxrwxrwx. 1 root root 9 Jun 18 12:46 ip-10.10.254.104:3260-iscsi-iqn.2005-10.nas2:docker-lun-0 -> ../../sdb
lrwxrwxrwx. 1 root root 9 Jun 14 08:54 pci-0000:00:01.1-ata-2 -> ../../sr0
````

а команда `iscsiadm -m session -P 3` даст еще больше информации по текущим интерфейсам

```
пример
````

поиск новых устройств выполняется через команду `iscsiadm -m discovery -t sendtargets -p 192.168.0.4`

Как multipath устройства отображаются? Как два разных?

Логин:

```
sudo iscsiadm -m node --login 
```

после этого в системе появляются новые блочные устройства.

Инструкция с CoreOS https://coreos.com/os/docs/latest/iscsi.html

### Список литературы

http://bog.pp.ru/hard/scsi.html

