### Консольные команды

#### Управление хостами

* Получить список хостов `xe host-list`

#### Управление ВМ

* Получить список всех ВМ `xe vm-list`

* Запуск ВМ `xe vm-start vm="vm_name"`

* Импорт ВМ из файла `xe vm-import filename=vm_name.xva`

* Узнать сетевые параметры ВМ `xe vm-list params=name-label,networks | grep -A 1 vm_name`

* Получить список параметров определенной ВМ `xe vm-param-list uuid=<...>`

* Список виртуальных сетей, к которым можно подключить ВМ `xe network-list`

## Установка Xen Tools

### Для Linux

[Проблема с установкой на старые ядра <2.6.36](https://wiki.xen.org/wiki/Xen_Linux_PV_on_HVM_drivers)

### Для FreeBSD

Устанавливаем командами:

```
pkg install -Rf sysutils/xe-guest-utilities
/usr/local/etc/rc.d/xenguest start
echo xenguest_enable=\"YES\" >> /etc/rc.conf
```

## Дополнительные ссылки

[Документация по сетевой настройке](https://docs.citrix.com/de-de/xenserver/index/ch04/ch04s04.html)

[Краткое описание командного интерфейса](https://wiki.xenproject.org/wiki/XAPI_Command_Line_Interface)
