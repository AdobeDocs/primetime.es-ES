---
description: Puede insertar publicidades en el contenido de VOD.
seo-description: Puede insertar publicidades en el contenido de VOD.
seo-title: Reemplazar intervalos de tiempo con una publicidad
title: Reemplazar intervalos de tiempo con una publicidad
uuid: 50cdcc06-7df5-414b-95d4-c684bc68dce3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---


# Reemplazar intervalos de tiempo con una publicidad{#replace-time-ranges-with-an-ad}

Puede insertar publicidades en el contenido de VOD.

En este caso, `TimeRanges` entre `begin` y `end` en `localTime` se eliminan de la línea de tiempo. Se reemplazan por un `AdBreak` de `begin` a `begin+replaceDuration`. Si la duración de sustitución no existe como parámetro, el servidor realiza la determinación en el Adbreak devuelto.

>[!NOTE]
>
>Siempre debe proporcionar una duración de reemplazo específica para los intervalos personalizados. Si no hay anuncios que vayan a reemplazar este intervalo personalizado, proporcione una duración de reemplazo de 0.

Reemplazar intervalos con anuncios de Primetime y decisiones.

```
{   
    "properties": [],
    "stream": {
        "manifests": [ {
            "url": 
              "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
            "type": "hls"
        } ],
                 
        "metadata": {
            "time-ranges": {
                "type": "replace",
                "time-range-list": [ {
                    "begin": 0,
                    "end": 15000,
                    "replacement-duration": 15000 
                },
                {
                    "begin": 69000,
                    "end": 99000,
                    "replacement-duration": 30000
                },
                {
                    "begin": 251000,
                    "end": 281000,
                    "replacement-duration": 30000
                },
                {
                    "begin": 514000,
                    "end": 544000,
                    "replacement-duration": 30000
                } ]
            },
            "ad": {
                "targeting": [ {
                    "value": "MulAdsAvail12346",
                    "key": "osmfKeyMulAdsAvail12346"
                } ],
                "domain": "sandbox2.auditude.com",
                "mediaid": "psdk_000105",
                "zoneid": "121781"
            }     
        }
    },   
    "title": "VOD - Replace TimeRange with Auditude Ads",
    "thumbnail": {
        "large": "https://example.com",
        "small": "https://example.com"
    },
    "type": "vod",
    "id": "vod_003"
}
```

