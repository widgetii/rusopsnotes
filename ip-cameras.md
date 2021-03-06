### Рекомендуемые чипы и матрицы

#### Чипы от Hisilicon

Актуальный [каталог камер](http://www.hisilicon.com/en/Products/ProductList/Camera)

* [Hi3518e](https://github.com/PeterEmbedded/Hi3518E-IP-Camera) — для матриц ~1.3 мегапикс. (1280 х 960). И [еще](https://zftlab.org/pages/2015090300.html). [Сравнение чипов Hi3518E и Hi3518C](http://www.cctvsp.ru/articles/soc-protsessor-ip-kamer-hi3518e-protiv-hi3518c)

* Hi3516 — для матриц ~2 мегапикс. и более. Последние модели этой серии делаются
    на базе модификации Hi3516Ev100 и [Hi3516Cv300](http://support.hkvstar.com/file/Hi3516CV300_DataSheet_Brief.pdf)

* Hi3519 - для высоких разрешений

> Е или С без разницы?

У С память внешняя и ее больше может быть
У Е она встроена и там 64

### Матрицы

* Sony IMX225 и Aptina AR0130, обе 1.3 Мпикс, та, что от Sony — намного лучше работает в темноте. Hi3518e + IMX225 — не смог полностью отключить шарпенинг, но при слабой освещённости оно вроде не мешает. В случае с Hi3518e + AR0130 — отключается полностью.

* Sony IMX291 FullHD 

* Sony IMX178 5Mpx (IMX178 уже давно не производят, продаются остатки)

* Sony IMX335 5Mpx 2592х1944

* OmniVision OS08A10 4K

При низкой освещённости матрицы с более высоким разрешением работают хуже и им требуются хорошие объективы

[Более полный обзор по матрицам](http://www.cctvsp.ru/articles/obzor-i-sravnenie-matrits-dlya-kamer-videonablyudeniya)

#### Интересные ссылки

- http://marcusjenkins.com/linux/hacking-cheap-ebay-ip-camera/

- http://www.hkvstar.com/technology-news/china-ip-camera-configuration-firmware.html

- [Инженерное решение IP камера + роутер NEXX WT3020F + модем 4G Huawei E3372](http://www.youcam.pro/4G-camera)

### Облачные провайдеры для видео

[IpEye](https://www.ipeye.ru/tarify)

[Ivideon](https://ru.ivideon.com/)

### Форматы

[Типы кадров](https://ru.wikipedia.org/wiki/%D0%A2%D0%B8%D0%BF%D1%8B_%D0%BA%D0%B0%D0%B4%D1%80%D0%BE%D0%B2)

#### H.264

Используется фиксированный размер кодируемого блока 16x16 пикселей (называемый
Macroblock), каждый из них может быть задействован в предсказании в соседних
кадрах или в том же кадре с другими блоками (но не одновременно в обоих
случаях).

Есть 8 методов заимствования ближайших пикселей.

[Stream Video From Android](http://cagneymoreau.com/stream-video-android/)

[Some info about bitstream format](https://stackoverflow.com/questions/24884827/possible-locations-for-sequence-picture-parameter-sets-for-h-264-stream/24890903#24890903)

#### H.265

Используется переменный размер блока, в зависимости от содержания сцены до
64x64, при этом в одном кадре могут быть блоки разного размера (теперь вместо
Macroblocks они называются "Coding Tree Units" - CTU). Блоки могут ссылаться
одновременно на юниты в этом же и других кадрах.

![Сравнение с H.264](https://blog.frame.io/wp-content/uploads/2018/09/HEVC-Macroblock2.jpg)

CTU не обязательно должны быть квадратными (как макроблоки) и поэтому хорошо
передают видео по текстурам, которые раньше не попадали в заданную сетку. Кол-во
методов заимствования увеличилось с 8 до 35.

[Хорошая вводная по технической части](http://www.rle.mit.edu/eems/wp-content/uploads/2014/06/H.265-HEVC-Tutorial-2014-ISCAS.pdf)

##### H.265+, H.265++ или H.265X

Если коротко, то + технология делит сцену на зоны с движением и для них отдельно
строит опорные кадры и кадры с изменением движения, а на основную сцену долго
держит один опорный кадр. Но настройки качества сжатия должны оставаться. А сам
битрейт меняется только на CBR, в VBR уже нельзя его установить.

[Преимущества протоколов H.265+, H.265++ или H.265X](http://www.youcam.pro/new-protocol-H265X)

#### OpenIPC

```
V1
hi3516cv100|hi3518av100|hi3518cv100|hi3518ev100)
kernel 3.0.8      <= сделано на 95%, но готового нет

V2
hi3516cv200|hi3518ev200|hi3518ev201)
kernel 3.4.35      <= есть OpenWRT на openipc.org для сенсоров Aptina AR0130 и Sony IMX222/IMX323

V3
hi3516сv300|hi3516ev100)
kernel 3.18.20   <= и конь не валялся
```

### WebRTC and other ways to stream to browser

- [Kurento Media Server](https://github.com/Kurento/kurento-media-server) It is responsible for media transmission, processing, loading and recording. It is implemented in low level technologies based on GStreamer

- [WebRTC-streamer](https://github.com/mpromonet/webrtc-streamer) WebRTC-streamer is an experiment to stream video capture devices and RTSP sources through WebRTC using simple mechanism

- [videostreamer](https://github.com/horgh/videostreamer) provides a way to stream video from an input source to HTTP. It remuxes a video input into an MP4 container which it streams to connecting clients (uses ffmpeg). Read README and use like `./videostreamer -input='rtsp://192.168.1.10/user=admin&password=&channel=1&stream=0' -fcgi=false -verbose -format=rtsp `

### Доп оборудование

#### Микрофоны

MAX9814 по 35 рублей, можно запитать от выхода USB 5V
