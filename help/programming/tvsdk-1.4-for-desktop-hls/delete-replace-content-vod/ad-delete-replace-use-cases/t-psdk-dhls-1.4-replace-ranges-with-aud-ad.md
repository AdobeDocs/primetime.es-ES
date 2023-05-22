---
title: Reemplazo de intervalos de tiempo con un anuncio de Adobe Primetime ad Decisioning
description: Reemplazo de intervalos de tiempo con un anuncio de Adobe Primetime ad Decisioning
copied-description: true
exl-id: 263274b7-4602-4be0-b0ad-040f6f0f2fae
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---

# Reemplazo de intervalos de tiempo con un anuncio de Adobe Primetime ad Decisioning{#replace-time-ranges-with-an-adobe-primetime-ad-decisioning-ad}

Eliminar `TimeRanges` entre los `begin` y `end` in `localTime` en la cronología. Sustitúyala por un AdBreak de `begin` hasta `begin+replaceDuration`.

Reemplace rangos por anuncios de Primetime y Decisioning.

```
{   
    "properties": [],
    "stream": {
        "manifests": [ {
            "url": "https://. . ./cloudfront_vod_hls_tos_30fps.m3u8",
            "type": "hls"
        } ],
        "metadata": {
            "time-ranges": {
                "type": "replace",
                "time-range-list": [ {
                    "begin": 0,
                    "end": 15000,
                    "replace-duration": 15000
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
