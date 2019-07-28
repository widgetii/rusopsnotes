# Clang & LLVM notes

## clang-tools-extra

- [Линтер Clang Tidy](https://clang.llvm.org/extra/clang-tidy/index.html)

- [Clang-Include-Fixer](https://clang.llvm.org/extra/include-fixer.html),
  добавляющий #include в исходный текст программ (неактуально, так как это может
  делать Clangd)

- [Modularize](https://clang.llvm.org/extra/modularize.html)

- [pp-trace](https://clang.llvm.org/extra/pp-trace.html)

- [Clang-Rename](https://clang.llvm.org/extra/clang-rename.html), C++
  refactoring tool for renaming classes, functions, variables, arguments,
  namespaces etc

- [Clang-Doc](https://clang.llvm.org/extra/clang-doc.html)

- clang-format, есть целый [сайт](https://clangformat.com/) для интерактивного
    формирования файла со стилем

## Сторонние утилиты на базе Clang

- [Autoprogrammer, the C++ code generation](https://github.com/flexferrum/autoprogrammer):
  PIMPL generator, enum to string converter, unit test methods (and mock classes)
  generation

- У LibreOffice есть отличная пачка [плагинов к clang](https://github.com/LibreOffice/core/tree/master/compilerplugins/clang) для статического анализа кода проекта

- [cppgrep](https://github.com/peter-can-talk/cppnow-2017/tree/master/code/cppgrep)

- [Декомпилятор бинарников в IR LLVM](https://github.com/trailofbits/mcsema),
  [статья на Habr](https://habr.com/post/347000/)

## Language servers

- [Clangd](https://clang.llvm.org/extra/clangd.html)

## Интересные патчи

- [Реализация концептов в Clang](https://github.com/saarraz/clang-concepts),
  онлайн версия на [godbolt](https://godbolt.org/g/Xthpfw), [обсуждение](https://www.reddit.com/r/cpp/comments/958sj9/clang_concepts_is_now_featurecomplete/)

  Сборка:

  ```shell
  $ git clone http://llvm.org/git/llvm.git
  $ take llvm
  $ git checkout 893a41656b527af1b00a1f9e5c8fcecfff62e4b6   see actual commit on github
  $ cd tools
  $ git clone https://github.com/saarraz/clang-concepts clang
  $ cd ../..
  $ cmake -Hllvm -Bbuild -G "Ninja"
  $ cmake --build build
   check working for binary files
  $ cd build/bin
  $ ./clang --help
  $ export CC=$(pwd)/clang
  $ export CXX=$(pwd)/clang++
  ```

## Clang API

- [Choosing the Right Interface for Your Application](https://clang.llvm.org/docs/Tooling.html)

- [Несколько вводных туториалов на русском](http://white-knight-is-alive.blogspot.com/2016/01/clang-api_20.html)

- [Презентация по Clang AST](http://llvm.org/devmtg/2013-04/klimek-slides.pdf)

- [Много статьей по LLVM на Habr](https://habr.com/users/32bit_me/posts/)

## Clang LibTooling (более новый C++ API)

## Сборка всего подряд из исходников

[Building Clang and Working with the Code](http://clang.llvm.org/get_started.html)

```sh
git clone https://github.com/llvm/llvm-project.git
cd llvm-project
cmake -Hllvm -BRelease -G Ninja -DCMAKE_BUILD_TYPE=Release \
    -DBUILD_SHARED_LIBS=ON -DLLVM_ENABLE_LLD=OFF -DLLVM_TARGETS_TO_BUILD=X86 \
    -DLLVM_ENABLE_PROJECTS="clang;libcxx;clang-tools-extra"
ninja -C Release clang clangd clangd-indexer clangFormat clangFrontendTool \
    clangIndex clangTooling cxx
```

Для сборки только clangd достаточно:

```sh
ninja -C Release clang clangd
```

Для MacOS существует способ проще:

```sh
brew install --HEAD llvm
```
