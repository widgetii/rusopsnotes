## Методы отладки k8s

(идея взяты с http://troubleshooting.kubernetes.sh/)

Создаем отдельный ns для отладки:

```
kubectl create ns debugns
```

В отдельном терминале (вкладке) можем отобразить все, что там происходит:

```
watch kubectl -n debugns get all
```

Все, что мы видим в отдельном окне в колонке NAME, мы можем исследовать через
команды (предположим, что NAME равно statefulset.apps/elasticsearch-logging):

```
kubectl -n debugns describe statefulset.apps/elasticsearch-logging
kubectl -n debugns logs statefulset.apps/elasticsearch-logging
```

или зайти в под (если он еще живой) по имени:

```
kubectl -n debugns exec -it elasticsearch-logging-0 -- sh
```

Имена подов можно получить по меткам:

```
THEPODS=$(kubectl -n debugns get po -l=k8s-app=elasticsearch-logging --output="jsonpath={.items[*].metadata.name}")
```

### Редактирование конфигурации на лету

```
kubectl -n elasticsearch edit deployment.apps/kibana-logging
```

позволит поэкспериментировать с параметрами без изменений в yaml файлах. Не
забудьте потом прибить POD для пересоздания его с новыми параметрами:

```
kubectl -n elasticsearch delete pod <elk-kibana-Pod-name>
```

### kubectl proxy

Если у нас между станцией управления и кластером нет общей сети (внутренние IP
адреса недоступны без специально обученного VPN), то для доступна в внутренним
сервисам можно воспользоваться встроенным костыликом:

В терминале:

```
kubectl proxy
```

В браузере:

```
http://localhost:8001/api/v1/namespaces/debugns/services/http:elasticsearch-logging:/proxy/
```

, где
- `debugns` - namespace
- `http` - протокол, под которым наш прокси цепляется на конечный сервис, здесь
    должен быть `http` или `https`
- `elasticsearch-logging` - название сервиса, к которому цепляемся

Доп ссылки по теме:
- [Для любителей Web UI](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)
- [Доступ к самому API](https://kubernetes.io/docs/tasks/access-kubernetes-api/http-proxy-access-api/)

