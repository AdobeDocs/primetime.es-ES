---
description: Reemplace una línea de tiempo de VOD enviando una nueva solicitud de inserción de publicidad al servidor de manifiesto con un parámetro de consulta ptlínea de tiempo definido correctamente.
title: Reemplazar una línea de tiempo de VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Reemplazar una cronología de VOD {#replace-a-vod-timeline}

Reemplace una línea de tiempo de VOD enviando una nueva solicitud de inserción de publicidad al servidor de manifiesto con un parámetro de consulta ptlínea de tiempo definido correctamente.

1. Prepare una solicitud de inserción de publicidad de la forma habitual.
1. Establezca el parámetro de consulta `ptcueformat` en DPIScte35.
1. Defina el parámetro de consulta `enableC3` en true o false según corresponda.
1. Cree un parámetro `pttimeline` utilizando el formato de cronología de VOD:
   1. Especifique cada bloque de contenido (capítulo) con `duration = 0` y `number_of_lots = 1`.
   1. Especifique cada bloque de publicidad como de costumbre, pero configure `lots = 0` para eliminar una pausa. Configure `duration = 0` para utilizar la duración de la pausa publicitaria (desde el archivo M3U8).

## Ejemplo: Reemplazar una línea de tiempo de VOD

En este ejemplo se supone que el contenido de VOD está en `Original.m3u8` con una cronología de `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

La siguiente solicitud del servidor de manifiesto reemplaza los saltos en `Original.m3u8` con un anuncio previo de 30 segundos, seguido de dos pausas de duración dos minutos cada una.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

La siguiente solicitud del servidor de manifiesto elimina los saltos en `Original.m3u8` y agrega un anuncio previo de 30 segundos y un anuncio posterior de 30 segundos.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
