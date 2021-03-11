---
title: Objeto JSON para pausas publicitarias directas
description: Detalla el objeto JSON cuando el valor de tipo es un salto de publicidad directo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Objeto JSON para pausas publicitarias directas{#json-object-for-direct-ad-breaks}

El siguiente bloque de código define el objeto JSON de detalles cuando el valor de tipo es pausas publicitarias directas.

El `MetadataNode` devuelto por `IFeedItemAdapter:getStreamMetadata()` contiene una entrada con una clave de tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` y un valor de una representación de cadena del valor del objeto JSON de detalles que aparece a continuación.

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
| `tag` | Cadena que se asigna al campo de etiqueta en `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `time` | Indica la hora de inicio de la pausa publicitaria y se asigna al campo de tiempo en `com.adobe.mediacore.timeline.advertising.AdBreak`. El valor 0 indica un anuncio pre-roll. |
| `replace` | Indica la duración del reemplazo de pausa publicitaria y se asigna al campo `replaceDuration` en `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `ad-list` | Una lista de anuncios que se deben reproducir durante la pausa publicitaria dada, se asigna al campo `List<Ad>` en `com.adobe.mediacore.timeline.advertising.AdBreak`. |

El siguiente bloque de código define el objeto JSON para la matriz de lista de anuncios.

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

