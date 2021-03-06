### Список PERL для изучения языков

### Традиционные REPL

#### Go

[Gore](https://github.com/motemen/gore)

[go-pry](https://github.com/d4l3k/go-pry)

#### C++17

[inspector](https://github.com/inspector-repl/inspector)

#### Rust

[Evcxr REPL](https://crates.io/crates/evcxr_repl)

[Rusti](https://github.com/murarth/rusti)

[Runner](https://crates.io/crates/runner) for quick scripts or snippets

### На базе Jupyter

### C++17

[xeus-cling](https://github.com/QuantStack/xeus-cling)
Install from Miniconda (brew version) and then kernels copying

```shell
cd /usr/local/miniconda3
cp -r ./envs/xeus-cling/share/jupyter/kernels/* ~/Library/Jupyter/kernels/
```

[Interactive C++: Meet Jupyter / Cling - Neil Horlock, ACCU 2019](https://www.youtube.com/watch?v=UzfYG8GdB3I)

#### Rust

[EvCxR](https://github.com/google/evcxr/blob/master/evcxr_jupyter/README.md),
краткий [обзор](https://github.com/google/evcxr/blob/master/evcxr_jupyter/samples/evcxr_jupyter_tour.ipynb)

#### Golang

[gophernotes](https://github.com/gopherdata/gophernotes)

```shell
$ go get -u github.com/gopherdata/gophernotes
$ mkdir -p ~/Library/Jupyter/kernels/gophernotes
$ cp $GOPATH/src/github.com/gopherdata/gophernotes/kernel/* ~/Library/Jupyter/kernels/gophernotes
```

