---
description: Para la inserción de anuncios en directo, es posible que tenga que salir de una pausa publicitaria antes de que todas las publicidades del desglose se reproduzcan hasta la finalización.
seo-description: Para la inserción de anuncios en directo, es posible que tenga que salir de una pausa publicitaria antes de que todas las publicidades del desglose se reproduzcan hasta la finalización.
seo-title: Implementación de un retorno de pausa publicitaria temprano
title: Implementación de un retorno de pausa publicitaria temprano
uuid: 984b6ed0-c929-49a3-9553-e30d1a7758ed
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Implementación de una devolución anticipada de pausa publicitaria{#implementing-an-early-ad-break-return}

Para la inserción de anuncios en directo, es posible que tenga que salir de una pausa publicitaria antes de que todas las publicidades del desglose se reproduzcan hasta la finalización.

>[!NOTE]
>
>Debe suscribirse a los marcadores de anuncios de empalme de salida/entrada ( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN` y `#EXT-X-CUE`).

Estos son algunos de los requisitos que deben tenerse en cuenta:

* Analice marcadores como `EXT-X-CUE-IN` (o etiqueta de marcador equivalente) que aparecen en los flujos lineales o FER.

   Registre los marcadores como el marcador del punto de retorno inicial de publicidad. Reproducir sólo `adBreaks` hasta esta posición de marcador durante la reproducción, que anula la duración del `adBreak` marcado por el marcador `EXE-X-CUE-OUT` inicial.

* Si existen dos `EXT-X-CUE-IN` marcadores para el mismo marcador `EXT-X-CUE-OUT`, el primer marcador `EXT-X-CUE-IN` que aparece es el que cuenta.

* Si el marcador `EXE-X-CUE-IN` aparece en la línea de tiempo sin un marcador `EXT-X-CUE-OUT` inicial, se descarta el marcador `EXE-X-CUE-IN`.

   En un flujo en directo, si el marcador `EXT-X-CUE-OUT` inicial acaba de salir de la ventana, el TVSDK no responderá a él.

* Cuando hay un retorno anticipado de una pausa publicitaria, el `adBreak` se reproduce hasta que la cabeza lectora vuelve a la posición original cuando se suponía que la pausa publicitaria debía finalizar y reanuda la reproducción del contenido principal desde esa posición.

## SpliceOut y SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` y  `SpliceIn` los marcadores marcan el comienzo y el final de la pausa publicitaria. La duración del tipo `SpliceOut` del marcador `EXE-X-CUE` puede ser cero y el tipo `SpliceIn` del marcador `EXE-X-CUE` marca el final de la pausa publicitaria. Aparecen en una etiqueta y difieren por tipo.

**Un marcador con diferentes tipos**

Por ejemplo, aquí hay un marcador con diferentes tipos:

```
#EXTM3U#EXT-X-TARGETDURATION:10
#EXT-X-VERSION:3
#EXT-X-MEDIA-SEQUENCE:44
  
#EXTINF:9.9,
https://server-host/path/file44.ts
#EXTINF:4.2,
https://server-host/path/file45.ts
  
#EXT-X-CUE:TYPE="SpliceOut",ID="1",DURATION="0",TIME="266.198",PROGRAM-ID="138",AVAIL-NUM="1",AVAILS-EXPECTED="10"
#EXTINF:5.8,
https://server-host/path/file46.ts
#EXTINF:9.9,
https://server-host/path/file47.ts
...
#EXTINF:9.9,
https://server-host/path/file56.ts
#EXTINF:4.2,
https://server-host/path/file57.ts
#EXT-X-CUE:TYPE="SpliceIn",ID="1",DURATION="0",TIME="266.198",PROGRAM-ID="138"
#EXTINF:9.9,
https://server-host/path/file58.ts
```

En el ejemplo de un marcador con diferentes tipos, si la duración del tipo `SpliceOut` es cero, los `SpliceOut` y `SpliceIn` deben trabajar juntos por cada pausa publicitaria. Actualmente, un marcador `SpliceOut` con una duración no nula y no necesita emparejar marcadores `SpliceIn` es más típico.

**Dos marcadores independientes**

El escenario más típico es un marcador `SpliceOut` con una duración no nula y que no necesita los marcadores `SpliceIn` de emparejamiento. Aquí, un marcador `SpliceIn` de emparejamiento marca el final de la pausa publicitaria durante la reproducción de pausa publicitaria, pero la pausa publicitaria se corta en la posición del marcador `SpliceIn` y los inicios de contenido principal se reproducen en esta posición.

Por ejemplo, a continuación se muestran dos marcadores independientes:

```
#EXT-X-CUE-OUT:ID=105,DURATION=30.0,TIME=1081.08
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589090425811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589150485811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589210545811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589270605811,format=m3u8-aapl-v4)
#EXT-X-CUE-IN:ID=105,TIME=1105.104
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589330665811,format=m3u8-aapl-v4)
```

