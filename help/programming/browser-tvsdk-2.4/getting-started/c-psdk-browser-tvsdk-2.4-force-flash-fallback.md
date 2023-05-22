---
description: El indicador forceflash de la lista de origen fuerza la reserva de Flash para una URL. Para esta URL, puede utilizar el Flash Player de Adobe para reproducir el contenido.
title: Forzar la reserva de Flash mediante la lista de fuentes de contenido
exl-id: 657bf9b1-d911-489d-80ca-2956b008431b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# Forzar la reserva de Flash mediante la lista de fuentes de contenido{#forcing-the-flash-fallback-using-the-media-source-list}

El indicador forceflash de la lista de origen fuerza la reserva de Flash para una URL. Para esta URL, puede utilizar el Flash Player de Adobe para reproducir el contenido.

En la lista de fuentes de contenidos (por ejemplo, en la `sources.js` file), puede establecer `forceflash` hasta `true`. Por ejemplo:

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
