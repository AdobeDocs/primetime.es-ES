---
description: Para la inserción de anuncios de flujo en directo, es posible que tenga que salir de una pausa publicitaria antes de que se reproduzcan todos los anuncios de la pausa hasta su finalización.
title: Implementación de un retorno anticipado de la pausa publicitaria
exl-id: 584e870e-1408-41a9-bb6f-e82b921fe99e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# Implementación de un retorno anticipado de la pausa publicitaria{#implementing-an-early-ad-break-return}

Para la inserción de anuncios de flujo en directo, es posible que tenga que salir de una pausa publicitaria antes de que se reproduzcan todos los anuncios de la pausa hasta su finalización.

>[!NOTE]
>
>Debe suscribirse a los marcadores de anuncios de empalme out/in ( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`, y `#EXT-X-CUE`).

Estos son algunos requisitos que se deben tener en cuenta:

* Analizar marcadores como `EXT-X-CUE-IN` (o etiqueta de marcador equivalente) que aparecen en los flujos lineales o FER.

   Registre los marcadores como el marcador de un punto de retorno anticipado. Sólo reproducir `adBreaks` hasta esta posición del marcador durante la reproducción, que anula la duración del `adBreak` marcado por el interlineado `EXE-X-CUE-OUT` marcador.

* Si dos `EXT-X-CUE-IN` existen marcadores para lo mismo `EXT-X-CUE-OUT` marcador, el primero `EXT-X-CUE-IN` el marcador que aparece es el que cuenta.

* Si la variable `EXE-X-CUE-IN` el marcador aparece en la línea de tiempo sin interlineado `EXT-X-CUE-OUT` marcador, el `EXE-X-CUE-IN` el marcador se descarta.

   En una emisión en directo, si la inicial `EXT-X-CUE-OUT` El marcador acaba de salir de la ventana, TVSDK no responderá a él.

* Cuando hay un retorno anticipado de una pausa publicitaria, la variable `adBreak` se reproduce hasta que el cabezal de reproducción vuelva a la posición original en el momento en que se suponía que la pausa publicitaria debía finalizar y se reanude la reproducción del contenido principal desde esa posición.

## SpliceOut y SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` y `SpliceIn` los marcadores marcan el principio y el final de la pausa publicitaria. La duración de la `SpliceOut` tipo de la `EXE-X-CUE` el marcador puede ser cero y la variable `SpliceIn` tipo de `EXE-X-CUE` El marcador marca el final de la pausa publicitaria. Aparecen en una etiqueta y difieren según el tipo.

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

En el ejemplo de un marcador con diferentes tipos, si la duración del `SpliceOut` el tipo es cero, el `SpliceOut` y `SpliceIn` deben trabajar juntos en cada pausa publicitaria. Actualmente, un `SpliceOut` marcador con una duración distinta de cero y no necesita emparejamiento `SpliceIn` los marcadores son más típicos.

**Dos marcadores separados**

El escenario más típico es un `SpliceOut` marcador con una duración distinta de cero y que no necesita el emparejamiento `SpliceIn` marcadores. Aquí, un emparejamiento `SpliceIn` Un marcador marca el final de la pausa publicitaria durante la reproducción de la pausa publicitaria, pero esta se corta en el `SpliceIn` posición del marcador y el contenido principal comienza a reproducirse en esta posición.

Por ejemplo, hay dos marcadores independientes:

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
