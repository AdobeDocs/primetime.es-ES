---
title: Ejemplo de recurso de VOD personalizado
description: Ejemplo de recurso de VOD personalizado
copied-description: true
exl-id: cf37c551-fb94-425e-ae11-d6a421e60566
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# Ejemplo de recurso de VOD personalizado {#example-of-a-customized-vod-asset}

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

Su aplicación podría configurar los siguientes escenarios:

* Una notificación cuando `#EXT-X-ASSET` las etiquetas, o cualquier otro conjunto de nombres de etiqueta personalizados a los que se haya suscrito, existen en el archivo.
* Insertar anuncios cuando un `#EXT-X-AD` , o cualquier otro nombre de etiqueta personalizado, se encuentra en el flujo.
