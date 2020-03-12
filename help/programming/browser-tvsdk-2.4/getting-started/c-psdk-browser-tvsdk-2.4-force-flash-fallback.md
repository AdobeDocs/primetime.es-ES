---
description: El indicador forceFlash de la lista de origen fuerza el respaldo Flash de una dirección URL. Para esta URL, puede utilizar Adobe Flash Player para reproducir el contenido.
seo-description: El indicador forceFlash de la lista de origen fuerza el respaldo Flash de una dirección URL. Para esta URL, puede utilizar Adobe Flash Player para reproducir el contenido.
seo-title: Forzar la reserva Flash mediante la lista de fuentes de medios
title: Forzar la reserva Flash mediante la lista de fuentes de medios
uuid: 04b09734-15f7-4e7e-8802-344f550f9b05
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Forzar la reserva Flash mediante la lista de fuentes de medios{#forcing-the-flash-fallback-using-the-media-source-list}

El indicador forceFlash de la lista de origen fuerza el respaldo Flash de una dirección URL. Para esta URL, puede utilizar Adobe Flash Player para reproducir el contenido.

En la lista de fuentes de medios (por ejemplo, en el `sources.js` archivo), puede establecer `forceflash` en `true`. Por ejemplo:

```js
{ 
        "title":"Title of the item listed in the media source list",
        "description":"Description of the item listed in the media source list",
        "isLive":true,
        "content":[ 
            { 
                "format":"HLS",
                "url":"https://path_to_HLS_stream.m3u8"
            },
 
        ],
        "forceflash" : true
},
```

