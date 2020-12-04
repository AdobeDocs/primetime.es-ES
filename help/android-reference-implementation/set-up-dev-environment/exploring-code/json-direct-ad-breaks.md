---
seo-title: Objeto JSON para saltos de publicidad directos
title: Objeto JSON para saltos de publicidad directos
uuid: ffb901f4-0a8b-40fe-b6ba-5ffebc324cf2
description: Detalles del objeto JSON cuando el valor de tipo es directo y saltos de publicidad
seo-description: Detalles del objeto JSON cuando el valor de tipo es directo y saltos de publicidad
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# Objeto JSON para saltos de publicidad directos{#json-object-for-direct-ad-breaks}

El siguiente bloque de código define los detalles del objeto JSON cuando el valor de tipo es saltos de publicidad directos.

El `MetadataNode` devuelto por `IFeedItemAdapter:getStreamMetadata()` contiene una entrada con una clave de tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` y un valor de una representación de cadena de los detalles del valor del objeto JSON debajo.

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
| `time` | Indica el tiempo de inicio de la pausa publicitaria y se asigna al campo de tiempo en `com.adobe.mediacore.timeline.advertising.AdBreak`. Un valor de 0 indica un anuncio previo. |
| `replace` | Indica la duración del reemplazo de pausa publicitaria, se asigna al campo `replaceDuration` en `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `ad-list` | Una lista de publicidades que se reproducirán durante una pausa publicitaria determinada, se asigna al campo `List<Ad>` en `com.adobe.mediacore.timeline.advertising.AdBreak`. |

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
| `url` | La dirección URL del contenido de la publicidad se asigna al campo de dirección URL en `com.adobe.mediacore.timeline.advertising.Ad`. |
| `duration` | La duración de la publicidad se asigna al campo de duración en `com.adobe.mediacore.timeline.advertising.Ad`. |
| `tag` | Una cadena de descripción. |

