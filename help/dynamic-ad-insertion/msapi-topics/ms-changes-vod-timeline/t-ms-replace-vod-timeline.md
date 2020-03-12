---
description: Reemplace una línea de tiempo de VOD enviando una nueva solicitud de inserción de publicidad al servidor de manifiesto con un parámetro de consulta pttimeline definido correctamente.
seo-description: Reemplace una línea de tiempo de VOD enviando una nueva solicitud de inserción de publicidad al servidor de manifiesto con un parámetro de consulta pttimeline definido correctamente.
seo-title: Reemplazar una línea de tiempo de VOD
title: Reemplazar una línea de tiempo de VOD
uuid: 17a6daa3-5ee5-48fb-8981-0d183aed0fe4
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Reemplazar una línea de tiempo de VOD {#replace-a-vod-timeline}

Reemplace una línea de tiempo de VOD enviando una nueva solicitud de inserción de publicidad al servidor de manifiesto con un parámetro de consulta pttimeline definido correctamente.

1. Prepare una solicitud de inserción de publicidad de la manera habitual.
1. Establezca el parámetro de `ptcueformat` consulta en DPIScte35.
1. Establezca el parámetro de `enableC3` consulta en true o false según corresponda.
1. Cree un `pttimeline` parámetro con el formato de línea de tiempo VOD:
   1. Especifique cada bloque de contenido (capítulo) con `duration = 0` y `number_of_lots = 1`.
   1. Especifique cada bloque de publicidad como de costumbre, pero configure `lots = 0` para eliminar un salto. Se configura `duration = 0` para utilizar la duración de la pausa publicitaria (desde el archivo M3U8).

## Ejemplo: Sustitución de una línea de tiempo de VOD

En este ejemplo se asume que el contenido de VOD se encuentra en `Original.m3u8` una línea de tiempo de `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

La siguiente solicitud de servidor de manifiesto reemplaza los saltos en `Original.m3u8` con un prelanzamiento de 30 segundos, seguido de dos saltos de duración de dos minutos cada uno.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

La siguiente solicitud de servidor de manifiesto elimina los saltos `Original.m3u8` y agrega un prelanzamiento de 30 segundos y un postdesplazamiento de 30 segundos.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
