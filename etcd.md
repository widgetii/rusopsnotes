## Создание нового кластера

Получаем новый токен для кластера:

```
$ curl -w "\n" 'https://discovery.etcd.io/new?size=3'
https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
```

Далее его можно использовать в cloud-config для CoreOS:

```
coreos:
  etcd2:
    discovery: https://discovery.etcd.io/c41cda8c66f2198faa4f27f4d9d9cc27
    # multi-region and multi-cloud deployments need to use $public_ipv4
    advertise-client-urls: http://$private_ipv4:2379,http://$private_ipv4:4001
    initial-advertise-peer-urls: http://$private_ipv4:2380
    # listen on both the official ports and the legacy ports
    # legacy ports can be omitted if your application doesn't depend on them
    listen-client-urls: http://0.0.0.0:2379,http://0.0.0.0:4001<Paste>
	listen-peer-urls: http://$private_ipv4:2380
  units:
    - name: etcd2.service
	  command: start
```

Подробнее в [документации](https://coreos.com/os/docs/latest/cluster-discovery.html)

## Команды обслуживания

Проверка состояния кластера

```
$ etcdctl cluster-health
member e14dcba44c7da9b2 is healthy: got healthy result from http://192.168.2.13:2379
member e8baaa0420d6fd08 is healthy: got healthy result from http://192.168.2.14:2379
member f77be20fe67d8e1f is healthy: got healthy result from http://192.168.2.12:2379
```

## Использование

Запись нового ключа:

```
$ etcdctl set /message "Welcome"
OR
$ curl -L http://127.0.0.1:2379/v2/keys/message -XPUT -d value="Welcome"
{"action":"set","node":{"key":"/message","value":"Welcome","modifiedIndex":175334,"createdIndex":175334},"prevNode":{"key":"/message","value":"Welcome","modifiedIndex":175208,"createdIndex":175208}}
```

Прочитать ключ:

```
$ etcdctl get /message
OR
$ curl -L http://127.0.0.1:2379/v2/keys/message
{"action":"get","node":{"key":"/message","value":"Welcome
```


