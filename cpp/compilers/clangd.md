# Немного о Clangd

## Что он умеет

[Стоит начать отсюда](https://clangd.github.io/features.html)

## Расширения протокола

[Официальное описание](https://clangd.github.io/extensions.html)

Смерженные:

- `textDocument/typeHierarchy` [Первичная поддержка type hierarchy](https://github.com/arichardson/llvm-project/commit/577d7d28ee32c38ab380eed335caff8ddb923a19). [Пример в VS](https://user-images.githubusercontent.com/1405703/46948959-14e8ea00-d080-11e8-9f3a-6d82732c2410.gif)

Нереализованные:

- `textDocument/subTypes`, which, given the location of a symbol naming a class
  type, returns information about its derived classes

- `textDocument/superType`, given the location of a symbol naming a class type, returns information about its base classes

- `Semantic highlighting`, [protocol extension](https://github.com/Microsoft/language-server-protocol/issues/513), jdt.ls [уже умеет](https://github.com/eclipse/eclipse.jdt.ls/issues/715)
    [WIP](https://reviews.llvm.org/D61842)

## Интересные фичи

- [Type-deduction](), можно сделать как умный Hover - https://raw.githubusercontent.com/wiki/JBakamovic/cxxd-vim/images/type-deduction.gif
  , который будет определять что лучше показать, тип значения, где он определен,
  кусок документации или аналог tag-peek

  Current implementation is a couple of special cases:

- hover on a decltype or auto keyword shows its expansion
- hover on a reference to an expr shows its declaration (mostly as spelled, with
  initializer), [подробнее](https://github.com/clangd/clangd/issues/58)

- [Show AST and memory layout](https://reviews.llvm.org/D62538)

- tweaks (and other features) may be hidden (clangd -hidden-features flag). We
may choose to promote these one day. I'm not sure they're worth their own
feature flags though.

## Тесты реализованных методов

clang-tools-extra/test/clangd/type-hierarchy.test

## Полезные видео

- [Index-While-Building and Refactoring to Clang](https://www.youtube.com/watch?v=jGJhnIT-D2M)

## FAQ

- [Как Clangd ищет системные либы](https://github.com/clangd/clangd/issues/64)

- [Как его использовать вместе с Clang-tidy](https://github.com/clangd/clangd/issues/63)

## Доработки

