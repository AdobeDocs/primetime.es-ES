---
description: Puede quitar TimeRanges entre el inicio y el final en localTime de la línea de tiempo.
seo-description: Puede quitar TimeRanges entre el inicio y el final en localTime de la línea de tiempo.
seo-title: Eliminar intervalos
title: Eliminar intervalos
uuid: 2f4afa0d-69e3-4929-8dbd-b553c8a64d96
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# Eliminar rangos{#delete-ranges}

Puede quitar TimeRanges entre el inicio y el final en localTime de la línea de tiempo.

>[!NOTE]
>
>Si sólo desea eliminar ciertos rangos del contenido y el mapa de publicidad debe utilizarse tal como lo define el servidor de publicidad, cree una instancia `CustomRangeMetadata` y especifique el tipo como una operación de DELETE con los rangos personalizados definidos.

Elimine intervalos con una publicidad de Adobe Primetime para la toma de decisiones de publicidad.

```
{   
    "properties": [],
    "stream": {
        "manifests": [
            {
                "url": "https://xyz.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
                "type": "hls"
            }
        ],
     
        "metadata": {
            "time-ranges": {
                "type": "delete",
                "time-range-list": [
                    {
                        "begin": 0,
                        "end": 20000
                    },
                    {
                        "begin": 69000,
                        "end": 99000
                    },
                    {
                        "begin": 251000,
                        "end": 281000
                    },
                    {
                        "begin": 514000,
                        "end": 544000
                    }
                ]
     
            },
            "ad": {
                "targeting": [
                    {
                        "value": "MulAdsAvail12346",
                        "key": "osmfKeyMulAdsAvail12346"
                    }
                ],
                "domain": "sandbox2.auditude.com",
                "mediaid": "psdk_000105",
                "zoneid": "121781"
            }     
        }
    },   
    "title": "VOD - DELETE TimeRange with Primetime ad decisioning Ads",
    "thumbnail": {
        "large": "https://example.com",
        "small": "https://example.com"
    },
    "type": "vod",
    "id": "vod_003"
}
```

