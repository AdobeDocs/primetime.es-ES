---
description: Puede insertar anuncios en el contenido de VOD.
title: Reemplazo de intervalos de tiempo por un anuncio
exl-id: b341d337-e190-4e2d-bad6-579771bcc577
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Reemplazo de intervalos de tiempo por un anuncio{#replace-time-ranges-with-an-ad}

Puede insertar anuncios en el contenido de VOD.

En este caso, `TimeRanges` entre los `begin` y `end` in `localTime` se eliminan de la cronología. Se sustituyen por una `AdBreak` de `begin` hasta `begin+replaceDuration`. Si la duración de reemplazo no existe como parámetro, el servidor realiza la determinación en el Adbreak devuelto.

>[!NOTE]
>
>Siempre debe proporcionar una duración de reemplazo específica para los intervalos personalizados. Si no se pretende que ningún anuncio sustituya este intervalo personalizado, proporcione una duración de sustitución de 0.

Reemplace rangos por anuncios de Primetime y Decisioning.

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
