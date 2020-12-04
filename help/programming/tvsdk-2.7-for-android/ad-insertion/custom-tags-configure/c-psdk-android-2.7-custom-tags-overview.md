---
seo-title: Ejemplo de un recurso de VOD personalizado
title: Ejemplo de un recurso de VOD personalizado
uuid: 21e83b47-d7e2-4a2d-8a0b-80dd09e253a8
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# Ejemplo de un recurso de VOD personalizado {#example-of-a-customized-vod-asset}

A continuación se muestra un ejemplo de un recurso de VOD personalizado:

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:7
 
#EXT-X-ASSET:AID=10
 
#EXTINF:9.9766,
seg1.ts
 
#EXTINF:9.9766,
seg2.ts
 
#EXTINF:9.9766,
seg3.ts
 
#EXT-X-AD:DURATION=10
#EXTINF:9.9766,
seg4.ts
 
#EXTINF:9.9766,
seg5.ts
 
#EXT-X-ENDLIST
```

La aplicación podría configurar los siguientes escenarios:

* Una notificación cuando `#EXT-X-ASSET` etiquetas, o cualquier otro conjunto de nombres de etiquetas personalizados al que se haya suscrito, existan en el archivo.
* Inserte publicidades cuando se encuentre una etiqueta `#EXT-X-AD` o cualquier otro nombre de etiqueta personalizado en el flujo.

