## Немного о корпоративном

### Использование прозрачной AAA внутри AD с помощью sssd

#### Решение различных проблем

* Для CentOS 7 при логине в консоль доменным пользователем может выскакивать
    сообщение `Cannot enter home directory. Using /.`, однако последующий `cd
    ~` отрабатывает прекрасно и дальшейшая работа проходит без каких-либо
    проблем. При этом при входе этим же пользователем через ssh подобной ошибки
    не возникает. Решением проблемы является дать команду `setsebool -P use_nfs_home_dirs 1`

#### Полезные источники

[Рекомендации по настройке SSSD в Debian](https://blog.it-kb.ru/2017/11/18/recommendations-for-configuring-sssd-in-debian-gnu-linux-about-dns-kerberos-and-active-directory-dc-search/)
[Анатомия отображения пользователей в SSD](https://jhrozek.wordpress.com/2015/03/11/anatomy-of-sssd-user-lookup/)
[Хорошая документация по Kerberos на сайте Ubuntu](https://help.ubuntu.com/community/Kerberos)
