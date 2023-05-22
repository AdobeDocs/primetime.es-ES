---
description: Reemplace una cronología de VOD enviando una nueva solicitud de inserción de publicidad al servidor de manifiesto con un parámetro de consulta pttimeline configurado correctamente.
title: Reemplazar una cronología de VOD
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Reemplazar una cronología de VOD {#replace-a-vod-timeline}

Reemplace una cronología de VOD enviando una nueva solicitud de inserción de publicidad al servidor de manifiesto con un parámetro de consulta pttimeline configurado correctamente.

1. Prepare una solicitud de inserción de publicidad de la manera habitual.
1. Configure las variables `ptcueformat` parámetro de consulta a DPIScte35.
1. Configure las variables `enableC3` parámetro de consulta a true o false según corresponda.
1. Crear un `pttimeline` parámetro con el formato de cronología de VOD:
   1. Especifique cada bloque de contenido (capítulo) con `duration = 0` y `number_of_lots = 1`.
   1. Especifique cada bloque de publicidad como de costumbre, pero se establece `lots = 0` para quitar una rotura. Establecer `duration = 0` para utilizar la duración de la pausa publicitaria (del archivo M3U8).

## Ejemplo: Reemplazo de una línea de tiempo de VOD

En este ejemplo se supone que el contenido de VOD está en `Original.m3u8` con una cronología de `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

La siguiente solicitud de servidor de manifiesto reemplaza a los desgloses de `Original.m3u8` con un pre-roll de 30 segundos, seguido de dos descansos de duración de dos minutos cada uno.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

La siguiente solicitud del servidor de manifiesto elimina los saltos de `Original.m3u8` y añade un anuncio previo a la emisión de 30 segundos y un anuncio posterior a la emisión de 30 segundos.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
