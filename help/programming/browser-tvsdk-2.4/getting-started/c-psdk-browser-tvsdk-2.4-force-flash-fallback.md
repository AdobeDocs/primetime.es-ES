---
description: El indicador forceflash de la lista de origen fuerza la reserva de Flash para una URL. Para esta URL, puede utilizar el Flash Player de Adobe para reproducir el contenido.
title: Forzar la reserva de Flash mediante la lista de fuentes de medios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 2%

---


# Forzar la reserva de Flash mediante la lista de fuentes de medios{#forcing-the-flash-fallback-using-the-media-source-list}

El indicador forceflash de la lista de origen fuerza la reserva de Flash para una URL. Para esta URL, puede utilizar el Flash Player de Adobe para reproducir el contenido.

En la lista de fuentes de medios (por ejemplo, en el archivo `sources.js` ), puede establecer `forceflash` en `true`. Por ejemplo:

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

