### Что значительного появилось в последних версиях

#### CMake 3.8

[В системных файндерах добавлен экспорт имен библиотек](https://youtu.be/eC9-iRN2b04?t=2230)

Можно вставить слайд https://youtu.be/eC9-iRN2b04?t=2274

### PC-зависимости

https://youtu.be/eC9-iRN2b04?t=2314

### Написание своего файндера

https://youtu.be/eC9-iRN2b04?t=2444

#### Cmake 3.11

https://cliutils.gitlab.io/modern-cmake/chapters/projects/fetch.html

#### CMake 3.12

CONFIGURE_DEPENDS flags
https://www.reddit.com/r/cpp/comments/8zv4tx/cmake_312_released/

### FAQ

#### Как собирать проект определенным компилятором?

Например, у нас стоит системный gcc, а собрать нужно через clang, тогда:

```
$ export CC=/usr/bin/clang
$ export CXX=/usr/bin/clang++
```

#### Как поставить последнюю версию на 64-бит Linux систему в /usr/local

```shell
$ cd $HOME
$ wget https://cmake.org/files/v3.12/cmake-3.12.0-Linux-x86_64.sh
$ sudo sh cmake-3.12.0-Linux-x86_64.sh --prefix=/usr/local --exclude-subdir
```

Проверить:

```
$ cmake --version | head -n1
```

Удалить:

```
$ sudo rm -rfv /usr/local/bin/{cmake,cpack,ccmake,cmake-gui,ctest} \
             /usr/local/doc/cmake \
             /usr/local/man1/{ccmake.1,cmake.1,cmake-gui.1,cpack.1,ctest.1} \
             /usr/local/man7/cmake-* \
             /usr/local/share/cmake-3.12
```

#### Можно установить CMake для локального пользователя через pip

```shell
$ pip install cmake --user
$ export PATH=~/.local/bin:$PATH
```

### Кросскомпиляция

[Crosscompiling](https://gitlab.kitware.com/cmake/community/wikis/doc/cmake/CrossCompiling)

### Тулинг на базе CMake

[Use The Tools Available](https://github.com/lefticus/cppbestpractices/blob/master/02-Use_the_Tools_Available.md)

### Как правильно работать с библиотеками

#### Qt

* [Правильный синтаксис подключения](https://blog.kitware.com/cmake-finding-qt5-the-right-way/)

* [Официальный мануал по CMake от Qt](http://doc.qt.io/qt-5/cmake-manual.html)

* [Подключение QtSingleApplication](https://github.com/qbittorrent/qBittorrent/blob/master/src/CMakeLists.txt#L61)

