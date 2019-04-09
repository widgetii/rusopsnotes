### Манипуляция машинами

### Снапшоты для резервного копирования

Смотрим какие диски есть у ВМ (в примере, это `vm1`):

```shell
virsh domblklist vm1
```

Делаем живой снэпшот:

```shell
virsh snapshot-create-as --domain vm1 snapshot1 --diskspec vda,file=/var/lib/libvirt/images/vmsnapshot1.qcow2 --disk-only --atomic --no-metadata
```

После этой команды у нас активен вновь созданный снэпшот и, при необходимости,
можно выполнить резервное копирование старого диска. Далее нам нужно закоммитить
все произошедшие изменения в оригинал:

```shell
virsh blockcommit vm1 vda --active --verbose --pivot
```

Теперь файл спапшота можно снести

```shell
rm /var/lib/libvirt/images/vmsnapshot1.qcow2
```

Для консистентных бэкапов файловых систем используйте Qemu Guest Agent и ключ
`–quiesce` при создании снэпшотов.

#### Windows

Создание

```shell
virt-install --name win10 --memory 4096 --cdrom /mnt/iso/Win10_1809Oct_EnglishInternational_x64.iso --disk "/var/lib/libvirt/images/win10.img",bus=virtio,size=50,format=qcow2,cache=writeback --hvm --accelerate --graphics vnc,password=evovi790,listen=0.0.0.0,port=5903 --network network=default,model=virtio --vcpus=4
```

идем в vnc и проводим установку до момента когда нас попросят выбрать диск для
установки системы (а вот в этом списке будет предательски пусто), качаем
[отсюда](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/archive-virtio/)
диск с драйверами (вида virtio-win-0.1.164.iso) и подсовываем в систему:

```shell
virsh # change-media win10 sda /mnt/iso/virtio-win-0.1.164.iso
Successfully updated media.
```

выбираем в установщике `Load driver`, `Browse`, на подключенном диске ищем папку
`viostor\w10\amd64`, загружаем драйвер и возвращаем установочный диск обратно:

```shell
virsh # change-media win10 sda /mnt/iso/Win10_1809Oct_EnglishInternational_x64.iso
Successfully updated media.
```

ставим чудо-систему до конца и после перезагрузки снова меняем диск на
драйверный и переходим в `Device Manager`, где будут устройства без драйверов на
сетевой адаптер и некое PCI `VirtIO Balloon Driver`, которые можно доставить,
просто указав корень компакт-диска.

Создаем снапшот сразу после установки:

```shell
virsh # snapshot-create-as --domain win10 --name 01_after_install
```

Откатывать по снапшоту систему проще простого:

```shell
virsh # shutdown --domain win10
virsh # shapshot-revert --domain win10 --snapshotname 01_after_install --running
```

Чтобы снести систему надо дать две команды на останов машины и ее удаление (диск
при этом остается и его нужно удалять вручную):

```shell
virsh # destroy win10
virsh # undefine win10
```

### Дополнительное чтение

[Virtualization Deployment and Administration Guide от
Redhat](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html-single/virtualization_deployment_and_administration_guide/index),
обязательно к прочтению при развертывании продакшн сред.

