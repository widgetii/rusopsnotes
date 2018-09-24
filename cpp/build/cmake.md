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
