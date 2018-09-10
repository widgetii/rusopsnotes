## Conan

>> What's pip? A package manager. How do I get it? Use easy_install. What's easy_install? A package manager. How do I get it? Use apt. (c) 

### История создания

Жил-был простой испанский парень Диего Родригес-Лосада, который работал сначала доцентом
в Политехническом университета Мадрида, после чего занялся исследованиями в
робототехнике, в результате чего ему пришлось целыми днями писать код на C и
C++.

Примерно в 2012 он бросил работу на наемного дядю и, как и полагается
современным бородатым пацанам, основал свой стартап Biicode. Главной идей в
новой компании было создание нового прогрессивного менеджера зависимостей для
любых языков программирования, который бы одинаково хорошо работал как с
локальной файловой системой компьютера разработчика, так и с облачными
хранилищами.

В связи с отсутствием финансового образования у основателей стартапа, произошло
то, что и должно было произойти: инвесторы оказались прокинуты, а у пацанов, к
счастью, появился так необходимый им опыт работы в стартапах.

К счастью, они не рискнули воспользоваться этим опытом и найти других
инвесторов, а поэтому просто пошли работать фулл-тайм синьорами в компанию JFrog
на зарплату.

Как оказалось, по хитрому плану нового работодателя им пришлось заниматься тем
же самым, но под новым названием **Conan**. Было принято решение обобщить весь
предыдущий опыт по созданию пакетного менеджера из поддерживаемых языков
оставить только C/C++.

### Концепция пакетного менеджера

Работая с роботами и пописывая для них код под С++, Диего обнаружил, что так
необходимая ему библиотека OpenCV тянет за собой кучу других
[зависимостей](https://github.com/opencv/opencv/tree/master/3rdparty), которые
отсутствуют под всеми любимую платформу Windows и их сборка может оказаться
большой проблемой.  С другой стороны, скачивая исходники всех
библиотек-зависимостей OpenCV с GitHub в Linux, может оказаться, что они уже
были установлены в системе местным пакетным менеджером некоторое время назад и
мы выполняем ненужную работу.

Подобный геморрой привел к тому, что в мире С/C++ стали пользоваться спросом
`header-only` библиотеки. Если взять популярную библиотеку
[CImg](http://cimg.eu/), то она содержит более 40K строк в единственном
заголовочном файле. Но с другой стороны подобный подход приводит к увеличению
времени сборки и потенциально может раздувать размер конечного бинарного файла.

К тому же мы имеем громадные библиотеки такие как **Boost** или **POCO**,
которые уже язык не поворачивается называть библиотеками, а скорее как
коллекциями библиотек. Несмотря на то, что для каждого проекта вы используете
не более чем 10% их функциональности, вы должны скачивать и инсталлировать их
целиком.

Так исторически сложилось, что для C/C++ не существует сколько-нибудь
популярного менеджера пакетов и их зависимостей, зато у нас есть разные
операционные системы, компиляторы, процессорные архитектуры, которые обычно
требуют индивидуального подхода.

5:16

### Инструкция по установке

Под Windows:

Ставим [Chocolatey](https://chocolatey.org/install) методом копи-паста
скопировав однострочный скрипт в оболочку `cmd.exe` или `PowerShell.exe` с
административными правами (для PowerShell возможно что потребуется сперва
изменить политику запуска скриптов):

```shell
PS> choco install pip
PS> pip install conan
```

Под все остальное:

```shell
$ <системный пакетный менеджер> install conan
или
$ pikaur -S conan       # ArchLinux (вместо pikaur здесь будет ваш любимый AUR менеджер)
$ brew install conan    # MacOS
$ pip install conan     # Там где Conan в системных репозиториях еще не завезли
```

Более подробная и свежая инструкция по установке находится [здесь](https://docs.conan.io/en/latest/installation.html)

### Соглашения по названиям пакетов

По умолчанию Conan придерживается [Спецификации семантического
версионирования](https://semver.org/lang/ru/)

Краткий FAQ по номерам версий:

1. [Что я должен делать с ревизиями в 0.y.z на начальной стадии разработки?](https://semver.org/lang/ru/#%D1%87%D1%82%D0%BE-%D1%8F-%D0%B4%D0%BE%D0%BB%D0%B6%D0%B5%D0%BD-%D0%B4%D0%B5%D0%BB%D0%B0%D1%82%D1%8C-%D1%81-%D1%80%D0%B5%D0%B2%D0%B8%D0%B7%D0%B8%D1%8F%D0%BC%D0%B8-%D0%B2-0yz-%D0%BD%D0%B0-%D0%BD%D0%B0%D1%87%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D0%B9-%D1%81%D1%82%D0%B0%D0%B4%D0%B8%D0%B8-%D1%80%D0%B0%D0%B7%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%BA%D0%B8)
1. [Как я узнаю, когда пора делать релиз 1.0.0?](https://semver.org/lang/ru/#%D0%BA%D0%B0%D0%BA-%D1%8F-%D1%83%D0%B7%D0%BD%D0%B0%D1%8E-%D0%BA%D0%BE%D0%B3%D0%B4%D0%B0-%D0%BF%D0%BE%D1%80%D0%B0-%D0%B4%D0%B5%D0%BB%D0%B0%D1%82%D1%8C-%D1%80%D0%B5%D0%BB%D0%B8%D0%B7-100)
1. [Не препятствует ли это быстрой разработке и коротким итерациям?](https://semver.org/lang/ru/#%D0%BD%D0%B5-%D0%BF%D1%80%D0%B5%D0%BF%D1%8F%D1%82%D1%81%D1%82%D0%B2%D1%83%D0%B5%D1%82-%D0%BB%D0%B8-%D1%8D%D1%82%D0%BE-%D0%B1%D1%8B%D1%81%D1%82%D1%80%D0%BE%D0%B9-%D1%80%D0%B0%D0%B7%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%BA%D0%B5-%D0%B8-%D0%BA%D0%BE%D1%80%D0%BE%D1%82%D0%BA%D0%B8%D0%BC-%D0%B8%D1%82%D0%B5%D1%80%D0%B0%D1%86%D0%B8%D1%8F%D0%BC)
1. [Даже если малейшие обратно несовместимые изменения в публичном API требуют выпуска новой главной версии, не закончится ли это тем, что очень скоро версия станет 42.0.0?](https://semver.org/lang/ru/#%D0%B4%D0%B0%D0%B6%D0%B5-%D0%B5%D1%81%D0%BB%D0%B8-%D0%BC%D0%B0%D0%BB%D0%B5%D0%B9%D1%88%D0%B8%D0%B5-%D0%BE%D0%B1%D1%80%D0%B0%D1%82%D0%BD%D0%BE-%D0%BD%D0%B5%D1%81%D0%BE%D0%B2%D0%BC%D0%B5%D1%81%D1%82%D0%B8%D0%BC%D1%8B%D0%B5-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F-%D0%B2-%D0%BF%D1%83%D0%B1%D0%BB%D0%B8%D1%87%D0%BD%D0%BE%D0%BC-api-%D1%82%D1%80%D0%B5%D0%B1%D1%83%D1%8E%D1%82-%D0%B2%D1%8B%D0%BF%D1%83%D1%81%D0%BA%D0%B0-%D0%BD%D0%BE%D0%B2%D0%BE%D0%B9-%D0%B3%D0%BB%D0%B0%D0%B2%D0%BD%D0%BE%D0%B9-%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D0%B8-%D0%BD%D0%B5-%D0%B7%D0%B0%D0%BA%D0%BE%D0%BD%D1%87%D0%B8%D1%82%D1%81%D1%8F-%D0%BB%D0%B8-%D1%8D%D1%82%D0%BE-%D1%82%D0%B5%D0%BC-%D1%87%D1%82%D0%BE-%D0%BE%D1%87%D0%B5%D0%BD%D1%8C-%D1%81%D0%BA%D0%BE%D1%80%D0%BE-%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D1%8F-%D1%81%D1%82%D0%B0%D0%BD%D0%B5%D1%82-4200)
1. [Что мне делать, если я случайно зарелизил обратно несовместимые изменения как минорную версию?](https://semver.org/lang/ru/#%D1%87%D1%82%D0%BE-%D0%BC%D0%BD%D0%B5-%D0%B4%D0%B5%D0%BB%D0%B0%D1%82%D1%8C-%D0%B5%D1%81%D0%BB%D0%B8-%D1%8F-%D1%81%D0%BB%D1%83%D1%87%D0%B0%D0%B9%D0%BD%D0%BE-%D0%B7%D0%B0%D1%80%D0%B5%D0%BB%D0%B8%D0%B7%D0%B8%D0%BB-%D0%BE%D0%B1%D1%80%D0%B0%D1%82%D0%BD%D0%BE-%D0%BD%D0%B5%D1%81%D0%BE%D0%B2%D0%BC%D0%B5%D1%81%D1%82%D0%B8%D0%BC%D1%8B%D0%B5-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F-%D0%BA%D0%B0%D0%BA-%D0%BC%D0%B8%D0%BD%D0%BE%D1%80%D0%BD%D1%83%D1%8E-%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D1%8E)

Что делать, если по каким-то причинам мы должны выложить новую версию, но
инкрементировать номер ПАТЧ-версии мы не можем? Можно воспользоваться следующим
трюком и добавить еще одну точку и дату изменения, например, `glfw/3.2.1.20180327@bincrafters/stable`

### Минимальный conanfile (для разработчика программ)

Фактически система поддерживает два типа файлов: `conanfile.txt` и
`conanfile.py`. В принципе отличаются друг от друга только тем, что в первом
можно описать только простую логику, когда второй является полноценной
программой на языке Python, хоть и выполненной согласно определенным
соглашениям.

Минимальный `conanfile.txt` на самом деле является пустым. Но какой от такого
файла будет толк? Никакого. Поэтому как минимум нужно добавить секцию
`[generators]` и прописать там что-то навроде `cmake` (разумеется, это просто
один из самых популярных генераторов для систем сборки, но им одним все не
ограничивается):

```
[generators]
cmake
```

Давайте создадим минимальный файл для системы CMake, который включит в себя
скрипт, генерируемый системой Conan, который и подставит в дальнейшем правильные
пути к зависимым библиотекам:

```shell
$ cat > CMakeLists.txt << 'EOF'
project(ConanTest)
cmake_minimum_required(VERSION 3.0)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

add_executable(conantest conantest.cpp)
target_link_libraries(conantest ${CONAN_LIBS})
EOF

$ cat > conantest.cpp <<EOF
#include <iostream>

int main() { std::cout << "Hello, Conan!" << "\n"; }
EOF
```

Фактически нашего внимания здесь потребует только конструкция подключения
сгенерированного Conanом вспомогательного скрипта `conanbuildinfo.cmake`,
фукнция вызова этого хелпера из CMake файла `conan_basic_setup()` и
использование заполненной этим скриптом переменной `${CONAN_LIBS}`, содержащей
зависимые библиотеки.

Создаем каталог сборки вне наших исходников и запускаем `conan install`:

```shell
$ mkdir build && cd build
$ conan install ..

PROJECT: Generator cmake created conanbuildinfo.cmake
PROJECT: Generator txt created conanbuildinfo.txt
PROJECT: Generated conaninfo.txt
```

Мы обнаружим, что будет создан описываемый ранее хелпер для CMake и два
текстовых файла, содержимое которых мы будем рассматривать в другой раз.
Попробуем собрать проект:

```shell
$ cmake ..
$ cmake --build .
$ ./bin/conantest
Hello, Conan!
```

Давайте теперь добавим в зависимость какую-нибудь библиотеку, добавив секцию
`[requires]` в `conanfile.txt`

### Работа с удаленными репозиториями

При свежей установке conan командой `conan remote list` выдаст только один
центральный репозиторий `conan-center`:

```shell
$ conan remote list
conan-center: https://conan.bintray.com [Verify SSL: True]
```

командой

```shell
conan remote add bincrafters "https://api.bintray.com/conan/bincrafters/public-conan"
```

мы сразу можем подключить второй по популярности репозиторий пакетов
`public-conan` и после чего проверить, что у нас теперь их два:

```shell
$ conan remote list
conan-center: https://conan.bintray.com [Verify SSL: True]
bincrafters: https://api.bintray.com/conan/bincrafters/public-conan [Verify SSL: True]
```

Web интерфейс для обоих репозиториев соответственно
[conan-center](https://bintray.com/conan/conan-center) и [bincrafters](https://bintray.com/bincrafters/public-conan)

Мы можем найти какой-нибудь пакет и его *установить*, хотя эта операция не
является обязательной, так как если conan найдет пакет в зависимостях, то он
произведет его *установку* автоматически:

```shell
$ conan install Qt/5.9.6@bincrafters/stable
Qt/5.9.6@bincrafters/stable: Not found in local cache, looking in remotes...
Qt/5.9.6@bincrafters/stable: Trying with 'conan-center'...
Qt/5.9.6@bincrafters/stable: Trying with 'bincrafters'...
Downloading conanmanifest.txt
[==================================================] 232B/232B        
Downloading conanfile.py
[==================================================] 9.9KB/9.9KB      
Downloading conan_export.tgz
[==================================================] 2.5KB/2.5KB      
Qt/5.9.6@bincrafters/stable: Installing package
Requirements
    Qt/5.9.6@bincrafters/stable from 'bincrafters' - Downloaded
Packages
    Qt/5.9.6@bincrafters/stable:0f4662410f0a9bdf85201fd748f5a42c05d1f5a4 - Download

Qt/5.9.6@bincrafters/stable: Retrieving package 0f4662410f0a9bdf85201fd748f5a42c05d1f5a4 from remote 'bincrafters' 
Downloading conanmanifest.txt
[==================================================] 229.6KB/229.6KB  
Downloading conaninfo.txt
[==================================================] 2.4KB/2.4KB      
Downloading conan_package.tgz
[==================================================] 28.5MB/28.5MB
Qt/5.9.6@bincrafters/stable: Package installed 0f4662410f0a9bdf85201fd748f5a42c05d1f5a4
Name            : libxcb
Version         : 1.13-1
Description     : X11 client-side library
Architecture    : x86_64
URL             : https://xcb.freedesktop.org/
Licenses        : custom
Groups          : None
Provides        : None
Depends On      : xcb-proto>=1.12  libxdmcp  libxau
Optional Deps   : None
Required By     : ffmpeg  lib32-libxcb  libvirt  libx11  libxkbcommon-x11  p4v  xcb-util  xcb-util-cursor  xcb-util-image  xcb-util-keysyms  xcb-util-renderutil  xcb-util-wm
Optional For    : None
Conflicts With  : None
Replaces        : None
Installed Size  : 3.96 MiB
Packager        : Andreas Radke <andyrtr@archlinux.org>
Build Date      : Tue 06 Mar 2018 10:09:53 PM MSK
Install Date    : Tue 31 Jul 2018 12:58:23 PM MSK
Install Reason  : Installed as a dependency for another package
Install Script  : No
Validated By    : Signature

Package already installed: libxcb
```

Обратите внимание, что несмотря на то, что в имени пакета указан поставщик
`bincrafters`, скачиваться он может не только с одноименного репозитория. В
нашей конфигурации приоритет загрузки определяется так:
1. локальная файловая система (кэш, это обычно `~/.conan/data` или
   `C:\Users\<юзер>\.conan\data`)
1. первый удаленный репозиторий (в нашем случае 'conan-center')
1. второй удаленный репозиторий (в нашем случае 'bincrafters')
1. третий и далее...

Чтобы добавить очередной репозиторий в начало списка и, следовательно,
установить ему наивысший приоритет (например, это может потребоваться для
корпоративного репозитория, где мы можем централизованно хранить кэш часто
используемых пакетов), воспользуйтесь ключиком `--insert` для команды `add`:

```shell
conan remote add local_artifactory http://package.mycompany.ru/artifactory/api/conan/conan-local --insert
```

Чтобы поменять приоритет существующих репозиториев (без их удаления и повторного
добавления) можно воспользоваться командой `update`:

```shell
conan remote update local_artifactory http://package.mycompany.ru/artifactory/api/conan/conan-local --insert
```

Мне было очень любопытно посмотреть, что же происходит под капотом. Мы можем
выставить переменную окружения `CONAN_TRACE_FILE` и задать путь к файлу с
логами, куда conan заботливо выложит протокол своей работы.

Давайте удалим свежепоставленный пакет и выполним повторную *установку* с
логированием:

```shell
$ conan remove Qt/5.9.6@bincrafters/stable
Are you sure you want to delete from 'Qt/5.9.6@bincrafters/stable' (yes/no): yes
$ CONAN_TRACE_FILE=$(pwd)/verbose.log conan install Qt/5.9.6@bincrafters/stable
```

Технически после выполнения этой команды произойдет следующее:

1. 

### Как Conan локально хранит пакеты

```shell
$ tree -L 1 ~/.conan/data/
~/.conan/data/
├── OpenSSL
├── Poco
├── Qt
└── zlib
```

Внутри отдельно взятой библиотеки:

```shell
$tree ~/.conan/data/OpenSSL/ 
└── 1.0.2o
    └── conan
        ├── stable
        │   ├── export
        │   │   ├── conanfile.py
        │   │   └── conanmanifest.txt
        │   ├── locks
        │   │   └── 35ea421ef4c1d32898da44c28e3cc900bc6459dc
        │   └── package
        │       └── 35ea421ef4c1d32898da44c28e3cc900bc6459dc
        │           ├── conaninfo.txt
        │           ├── conanmanifest.txt
        │           ├── include
        │           │   └── openssl
        │           │       ├── aes.h
        │           │       ├── applink.c
        │           │       ├── asn1.h
        │           │       ├── asn1_mac.h
        │           │       ├── asn1t.h
        ...
        │           │       ├── x509v3.h
        │           │       └── x509_vfy.h
        │           ├── lib
        │           │   ├── libcrypto.a
        │           │   └── libssl.a
        │           └── LICENSE
        ├── stable.count
        └── stable.count.lock
```

`35ea421ef4c1d32898da44c28e3cc900bc6459dc` - это хэш бинарного пакета (так
называемый
[build_id()](https://docs.conan.io/en/latest/reference/conanfile/methods.html#build-id),
который может быть равен идентификатору пакета
[package_id()](https://docs.conan.io/en/latest/reference/conanfile/methods.html#build-id),
в свою очередь вычисляемый по совокупности его свойств `settings`, `options` и
`requires`. Если мы хотя бы на байт меняем что-то из перечисленного, то сумма
также будет пересчитана и будет создана отдельная папка для нового пакета. 

### Поиск пакетов

Посмотреть, что сейчас лежит в локальном кэше можно командой:

```shell
$ conan search
```

Ключик `-r <имя-репозитория>` позволяет поискать библиотеку в конкретном
репозитории:

```shell
$ conan search -r bincrafters Qt
Existing package recipes:

Qt/5.11.0@bincrafters/stable
Qt/5.11.1@bincrafters/stable
Qt/5.11@bincrafters/stable
Qt/5.6.3@bincrafters/stable
Qt/5.9.6@bincrafters/stable
Qt/5.9@bincrafters/stable
```

Причем в данном примере вместо `Qt` мы можем написать `"*test*"` и получить
список всех пакетов, содержащих в своем названии слово `test`.

### Свой собственный (а может быть корпоративный) Conan сервер

Вы, наверное, видели в некоторых презентациях Conan эту картинку:

![](https://docs.conan.io/en/latest/_images/systems.png)

Фактически у нас есть три варианта серверов, на которых пользователи могут
размещать свои собственные пакеты:

* `conan_server` - простой TCP сервер, который легко поднять для хостинга своих
    собственных приватных пакетов. Он является сервисом, который можно спрятать
    как за традиционным web-сервером (таким как Apache или Nginx) или вывесить
    голой Ж наружу. Также как и клиент `conan` распространяется под MIT
    лицензией и может свободно использоваться внутри компании.

* `JFrog Artifactory` в числе прочих дает возможность хостинга Conan
    репозиториев. В отличии от предыдущего варианта, он является более
    функциональным, имеет web-морду, несколько различных протоколов
    аутентификации, средства обеспечения высокой доступности и кучу всего
    прочего за отдельные деньги.

* `JFrog Bintray` - сервис от той же компании, предлагающий облачный хостинг для
    свободных проектов (бесплатно) или коммерческих (внезапно за деньги). На
    этом самом сервисе крутится центральный репозиторий `conan-center` и
    общедоступный `bincrafters`.

В этом разделе мы рассмотрим только первые два варианта.

#### Conan server

Для следующих экспериментов мы воспользуемся Docker-образом от [cguenther/conan-server](https://hub.docker.com/r/cguenther/conan-server/):

```shell
$ mkdir conan_server
$ docker run -d \
    -p 9300:9300 \
    -v $(pwd)/conan_server:/var/lib/conan \
    --name conan_server \
    cguenther/conan-server:latest
```

Добавляем в список удаленных репозиториев (не забываем про флаг `--insert` если
хотим, чтобы данные из этого репозитория скачивались в первую очередь). По
умолчанию conan server имеет единственного пользователя demo с паролем demo:

```shell
$ conan remote add my_local_server http://localhost:9300
$ conan search -r my_local_server
There are no packages
$ conan search
Existing package recipes:

OpenSSL/1.0.2o@conan/stable
Poco/1.9.0@pocoproject/stable
Qt/5.9.6@bincrafters/stable
zlib/1.2.11@conan/stable
$ conan upload zlib/1.2.11@conan/stable -r my_local_server
Uploading zlib/1.2.11@conan/stable to remote 'my_local_server'
Please log in to "my_local_server" to perform this action. Execute "conan user" command.
Please enter a password for "demo" account: 
ERROR: Permission denied for user: 'demo'. [Remote: my_local_server]
```

И здесь нас настигла ошибка!

### Команды обслуживания

* После сборки пакетов из исходников в соответствующих каталогах `build`
    остаются как и оригинальные исходники, так и всякий мусор в виде объектных
    файлов и готовых бинарников, которые в конце процесса были скопированы в
    целевое расположение. К слову, исходники у нас тоже уже хранятся в каталоге
    `source`, поэтому в данном случае они оказываются дублированы. Сохранение
    этих файлов обычно нужно для исследования причин проблемы со сборкой, но для
    обычного процесса разработки они не нужны. Мы можем дать
    команду для очистки кэша:

    ```shell
    conan remove * -b
    ```

* Перенос пакетов целиком между репозиториями

