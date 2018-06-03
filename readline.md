## Горячие клавиши для командной строки Bash (и все, что использует Readline)

Это транскрипт видео [Readline: Your Other
Editor](https://www.youtube.com/watch?v=MxRTh8wlmJk) в моем вольном изложении.

Я хочу поговорить о библиотеке Readline, которая является еще одним редактором
из вашей повседневной жизни. Если вы используете терминал, то вы уже используете
Readline или что-то похожее на нее.  Readline - это строчный редактор, который
применяется в Bash, интерактивных интерпретаторах скриптовых языков типа Ruby.

Предположим, что мы ввели команду
```
snowball ~$ echo foo bar baz
```
и только потом осознали, что два последних ее аргумента были неправильными.

Новички, которые только знакомятся с командной строкой, начнут лихорадочно
нажимать Backscape, чтобы посимвольно удалить лишнее и ввести правильные данные.
Более опытные уже знают, что с помощью комбинации Ctrl-W смогут за одно нажатие
удалить по одному слову вместе с соседним пробелом.

Еще меньше знающих о том, что в том случае, если вы увлеклись и удалили одно
"лишнее" слово, на помощь может придти еще одна комбинация клавиш
Ctrl-Shift-(дефис) или Ctrl-X Ctrl-U, которая проведет откат последнего
удаления. (Кстати, знаете ли вы как откатить подобное случайное нажатие Ctrl-W в
Vim?).

На самом деле рассматриваемый нами редактор всецело работает со строками и
большинство горячих клавиш манипулируют этими строками. К примеру, переместите курсор в
центр вводимой строки и понажимайте комбинации клавиш Ctrl-A и Ctrl-E.
Фактически они заменяют нам клавиши Home и End (к слову, у меня на клавиатуре
ноутбука для экономии места таких клавиш нет вообще, а на полноразмерной
клавиатуре к этим клавишам приходится далеко тянуться и выполнять таким образом
лишние для моих рук действия).

Комбинация Meta-T поменяет последние два аргумента в командной строке:
попробуйте в нашем примере с выводом трех слов **foo bar baz** переместить
курсор в конец строки и посмотреть что произойдет? Что за клавиша Meta спросите
вы? Сейчас имеет смысл воспользоваться Google и поискать самостоятельно:
1. Какая комбинация клавиш по-умолчанию назначена как Meta?
2. Каким образом ее можно переназначить на другую?

Последнюю изученную комбинацию можно запоминить по слову *transpose*.
Примечательно, что у нее если похожая операция по перестановке, вызываемая по
Ctrl-T. Посмотрите на примере аргумента **123456**, что она делает? Для чего ее
можно использовать в вашей ежедневной работе?

Я остановился примерно на 4 минуте

Нужно описать команды 
(ctrl-f - move forward), (ctrl-b - move backward)
(ctrl-p - move up in history), (ctrl-n - move down in history),  and (ctrl-k -
delete to the end of the line)
what about alt+b or alt+f, alt+r, ctrl+u, etc. You left out the best
ones!!


The readline library not only lets you handle callbacks per line, but it also
handles character callbacks so you can do things interactively. I used it to
make an interactive regex tester with PCRE.

Also, you can bind up/down to the escape sequences for up/down ("\e[A" / "\e[B"
IIRC) and you can make a more typical text editor. The nice thing is that the
history function directly correlates to the correct line and the history updates
as you change it, so it basically behaves like a multiline buffer.﻿

### Что почитать еще

[Если вы вынуждены использовать Windows](http://mridgers.github.io/clink/)
[Bash Keyboard Shortcuts](https://ss64.com/bash/syntax-keyboard.html)
[Improving Command Line Productivity with GNU
Readline](https://spin.atomicobject.com/2017/11/10/readline-productivity/)
[Материал из Национальной библиотеки им. Н. Э.
Баумана](https://ru.bmstu.wiki/GNU_Readline) 
[Работа Readline в
Bash](https://www.gnu.org/software/bash/manual/html_node/Readline-Interaction.html)
[Readline Cheat Sheet](http://readline.kablamo.org/emacs.html) [Примеры оберток,
над неподдерживаемыми программами](http://xgu.ru/wiki/GNU_Readline)

[Programming with GNU Readline](http://web.mit.edu/gnu/doc/html/rlman_2.html)


