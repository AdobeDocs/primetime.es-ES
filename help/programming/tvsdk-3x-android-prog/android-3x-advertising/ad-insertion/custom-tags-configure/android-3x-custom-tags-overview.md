---
seo-title: Ejemplo de un recurso de VOD personalizado
title: Ejemplo de un recurso de VOD personalizado
uuid: 25927d5f-ac16-45f4-bf0d-92f1ab394c05
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# Ejemplo de un recurso de VOD personalizado{#example-of-a-customized-vod-asset}

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

