## Отличия StrongSWAN, libreswan

### Примеры конфигураций

[Mikrotik, IPSec, libreswan](https://nixman.info/?p=2633)

[Juniper SRX и Libreswan (и ещё StrongSwan)](https://nixman.info/?p=2816)

## Мой FAQ по StrongSwan

### Отладка глобального конфига когда ничего не работает

```shell
ipsec start --nofork --debug-all
```

### no matcing CHILD_SA config found

Скорее всего не совпадают сети/маски сетей шифруемого трафика.

### Ресурсы поддержки

[Google Group](https://groups.google.com/forum/#!forum/strongswan-users)

