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

### Кросскомпиляция

[Crosscompiling](https://gitlab.kitware.com/cmake/community/wikis/doc/cmake/CrossCompiling)

### Тулинг на базе CMake

[Use The Tools Available](https://github.com/lefticus/cppbestpractices/blob/master/02-Use_the_Tools_Available.md)

### Как правильно работать с библиотеками

#### Qt

* [Правильный синтаксис подключения](https://blog.kitware.com/cmake-finding-qt5-the-right-way/)

* [Официальный мануал по CMake от Qt](http://doc.qt.io/qt-5/cmake-manual.html)

* [Подключение QtSingleApplication](https://github.com/qbittorrent/qBittorrent/blob/master/src/CMakeLists.txt#L61)

#### Boost

[Модульный подход с помощью Conan](https://github.com/bincrafters/conan-cmake_findboost_modular)

