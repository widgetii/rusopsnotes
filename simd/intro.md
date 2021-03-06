## С чего начать?

![Эволюция](https://habrastorage.org/getpro/habr/post_images/bcc/54c/7ca/bcc54c7ca27096de07d326460b4941f3.jpg)

[Гайд по интринсикам](https://software.intel.com/sites/landingpage/IntrinsicsGuide/)

### SSE4

#### strings

https://www.strchr.com/strcmp_and_strlen_using_sse_4.2
https://github.com/WojciechMula/simd-string

### AVX

AVX - поддержка 256 битных регистров

Крайне нежелательно смешивать SSE- и AVX-инструкции. Если вам нужна какая-то
команда из SSE в AVX-коде, воспользуйтесь её AVX-аналогом с префиксом v.

Команды загрузки/сохранения выровненных данных vmovaps/vmovapd/vmovdqa требуют,
чтобы данные были выровнены на 16 байт, даже если сама команда загружает 32
байта.

Существующие 128 SSE будут использовать младшую половину YMM регистров, не меняя
старшую. Так, каждая инструкция из SSE (а также SSE2, SSE3, SSSE3, SSE4.1, SSE4.2
и AES-NI) имеет в AVX свой аналог с префиксом v. 

Есть трехоперадный синтаксис `c = a + b`. Intel рекомендует отказаться от старых
SSE инструкций в пользу новых 128-битных AVX-инструкций, даже если достаточно
двух операндов.

### AVX2

Реализована поддержка так называемых gather-инструкций, благодаря которым
перестает действовать строгое требование непрерывного расположения данных в
памяти. Теперь данные могут собираться из разных адресов памяти
