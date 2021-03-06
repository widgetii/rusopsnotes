# Bash

## Ветвления

Синтаксис:

```sh
if [[ условие ]]
then
 # действия, если условие истина
fi
```

Условия (строки):

```sh
-z <строка>      # строка пуста
-n <строка>      # строка не пуста
<стр1> == <стр2> # строки равны
<стр1> != <стр2> # строки не равны
```


Условия (числа):
```sh
-eq   # равно
-ne   # не равно
-lt   # меньше
```

Двойные скобки служат для сложных выражений, где проверяется сразу несколько
условий.  Одинарные скобки - синоним для утилиты test, проверяющей только одно
условие.  Другое отличие в том, что при использовании операторов < и > в условии
[[ ]] лексикографическое сравнение строк происходит в соответствии с текущей
локалью, а утилита test использует ASCII порядок.

Дополнительно: [секреты Bash](http://web.archive.org/web/20140209021437/http://redhat-club.org/2011/%D1%81%D0%B5%D0%BA%D1%80%D0%B5%D1%82%D1%8B-bash)
