## H.264

https://github.com/SoylentGraham/Soy264/tree/master/src - чтение NAL пакетов и
печать их типа
https://gist.github.com/figgis/fd509a02d4b1aa89f6ef парсинг NALов на Петоне

## H.265

https://github.com/yin8086/HEVCLearn/commits/master китаей изучал h265
https://github.com/lmshao/RTP простейший RTP сервер
https://github.com/hi35xx/live-streamer

вариант декодировки потока (работает в вазм?) https://github.com/AlexVestin/WasmVideoEncoder/blob/master/webassembly/C/avio_read.c

извлечение потока из контейнера видео: ffmpeg -i your_file -vcodec copy -an video.h265

попытка сделать декодер на asm.js h.265 в 15 году https://github.com/strukturag/libde265.js

инжектирование метаданных в поток https://github.com/SK-Hardwired/nv_hevc_hdr_patcher

### библиотеки декодеров

https://github.com/OpenHEVC/openHEVC
https://github.com/strukturag/libde265
https://github.com/strukturag/gstreamer-libde265 (он же, только в качестве
плагина)

## Анализаторы потока

https://github.com/IENT/YUView

https://github.com/virinext/hevcesbrowser (анализ битового потока для h265)

https://github.com/virinext/hevcesbrowser


## Серверы вещания

https://github.com/mpromonet/v4l2rtspserver RTSP (UDP uni/multicast) и HTTP с
HLS, кодеки H264, HEVC, JPEG, VP8 or VP9 и PCM S16_BE, S16_LE, S32_BE or S32_LE.
Хорошо работает с RP

https://github.com/mpromonet/webrtc-streamer

## Идеи

Сделать сервер для RP, который бы брал выход с китайской камеры, не трогал
видео, а аудио в Opus перекодировал с заданным качеством, затем по UDP отправлял
в облако (при необходимости с буферизацией).

## Аппаратное ускорение

https://developer.nvidia.com/nvidia-video-codec-sdk (поддерживается ffmpeg и
libav)

## ML

https://github.com/tianyili2017/HEVC-Complexity-Reduction интересная попытка
предсказать лучшее кодирование

https://github.com/HEVC-Projects/CPH - еще одна

https://github.com/remega/Compressd_Domain_SaliencyPrediction

https://github.com/hchen1506/iterative-filtering-intra-prediction

## Новинки железа

IVG-HP500NS-AF Hi3516D + SC5239 5MP с объективом 2.8-12mm https://item.taobao.com/item.htm?spm=2013.1.20141001.1.24ec4ee8abSw0H&id=579731965039

IVG-83H80NV-BE 3516A + OS08A10 8MP без объектива https://item.taobao.com/item.htm?spm=2013.1.20141001.1.646b5ae45WbvUN&id=567613190474

IPG-85HE20PYA-S 3516EV100 + IMX307 без объектива https://item.taobao.com/item.htm?spm=2013.1.20141001.2.52f011ebBs8RVy&id=583391928748

IVG-80X20PS-S XM530+2235P без объектива https://item.taobao.com/item.htm?id=588219855810




