---
seo-title: Ejemplo de un recurso de VOD personalizado
title: Ejemplo de un recurso de VOD personalizado
uuid: e0dfaa72-d62f-4fb3-b7c5-ad94f0dc7ce0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

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

* Una notificación cuando `#EXT-X-ASSET` las etiquetas, o cualquier otro conjunto de nombres de etiquetas personalizados al que se haya suscrito, existan en el archivo.
* Inserte publicidades cuando se encuentre una `#EXT-X-AD` etiqueta o cualquier otro nombre de etiqueta personalizado en el flujo.

