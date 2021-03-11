---
title: Ejemplo de un recurso de VOD personalizado
description: Ejemplo de un recurso de VOD personalizado
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# Ejemplo de un recurso de VOD personalizado {#example-of-a-customized-vod-asset}

Este es un ejemplo de recurso de VOD personalizado:

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

* En el archivo existe una notificación cuando `#EXT-X-ASSET` etiquetas, o cualquier otro conjunto de nombres de etiquetas personalizados al que se haya suscrito.
* Inserte publicidades cuando se encuentre una etiqueta `#EXT-X-AD` o cualquier otro nombre de etiqueta personalizado en el flujo.

