---
title: Objeto JSON para pausas publicitarias directas
description: Detalla el objeto JSON cuando el valor del tipo es saltos de publicidad directos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Objeto JSON para pausas publicitarias directas{#json-object-for-direct-ad-breaks}

El siguiente bloque de código define los detalles del objeto JSON cuando el valor del tipo es direct and breaks.

El `MetadataNode` devuelto por `IFeedItemAdapter:getStreamMetadata()` contiene una entrada con una clave de tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` y valor de una representación de cadena del valor de objeto JSON de detalles a continuación.

```
“metadata”: { 
    “ad” :  { 
        “type”: “direct ad breaks”, 
        “details”: { 
            "ad-breaks": [ 
                { 
                    "tag": "break-001", 
                    "time": 0, 
                    "replace": 0, 
                    "ad-list": [ 
                        { 
                        }, 
                        { 
                        } 
                    ] 
                }, 
                { 
                    "tag": "break-002", 
                    "time": 300000, 
                    "replace": 0, 
                    "ad-list": [ 
                        { 
                        } 
                    ] 
                } 
            ] 
        } 
    } 
} 
```

| Propiedad | Descripción |
|---|---|
| `tag` | Una cadena que se asigna al campo de etiqueta en `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `time` | Indica la hora de inicio de la pausa publicitaria y se asigna al campo de hora de `com.adobe.mediacore.timeline.advertising.AdBreak`. El valor 0 indica un anuncio previo a la emisión. |
| `replace` | Indica la duración de reemplazo de la pausa publicitaria, se asigna a `replaceDuration` field en `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `ad-list` | Una lista de anuncios que se reproducirán durante la pausa publicitaria dada, se asigna a la variable `List<Ad>` field en `com.adobe.mediacore.timeline.advertising.AdBreak`. |

El siguiente bloque de código define el objeto JSON para la matriz de listas de anuncios.

```
"ad-list": [ 
    { 
        "url": "https://cdn.auditude.com/player/downloads/data/espn/ads/csx/prog_index.m3u8", 
        "duration": 15000, 
        "tag": "1st break - 1st ad" 
    }, 
    { 
        "url": "https://cdn.auditude.com/player/downloads/data/espn/ads/csx/prog_index.m3u8", 
        "duration": 30000, 
        "tag": "1st break - 2nd ad" 
    } 
], 
```

| Propiedad | Descripción |
|---|---|
| `url` | La dirección URL del contenido del anuncio se asigna al campo URL en `com.adobe.mediacore.timeline.advertising.Ad`. |
| `duration` | La duración del anuncio se asigna al campo de duración en `com.adobe.mediacore.timeline.advertising.Ad`. |
| `tag` | Una cadena de descripción. |
