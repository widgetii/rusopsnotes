## Заметки по использованию бабушкиного Редхата

### CentOS 4.8

#### Обновление gcc на более свежую версию

```
tar -xzvf gcc-4.8.4.tar.gz
cd gcc-4.8.4
./contrib/download_prerequisites
cd ..
mkdir objdir
cd objdir
$PWD/../gcc-4.8.4/configure --prefix=$HOME/gcc-4.8.4 --enable-languages=c,c++
make
make install
```

далее нужно будет прописать пути для работы

```
PATH=$HOME/gcc-4.8.4/bin:$PATH
LIBDIR=$HOME/gcc-4.8.4/lib
LD_LIBRARY_PATH=$LIBDIR:$LD_LIBRARY_PATH
LD_RUN_PATH=$LIBDIR:$LD_RUN_PATH
```

#### Попытка обновления ядра

Рассмотрено на примере `2.6.36.4`.

* [Базовое HOWTO](https://www.howtoforge.com/kernel_compilation_centos)

* Необходимо использовать более свежий gcc, чем тот, что есть в дистрибутиве
    (подтверждена успешная компиляция на gcc >= 4.3.4)

* Возможно, что потребуется применить [этот патч](https://www.systutorials.com/linux-kernels/15853/x86-ptrace-fix-build-breakage-with-gcc-4-7-linux-2-6-32-61/)
