---
description: 'null'
seo-description: 'null'
seo-title: Reemplazar intervalos de tiempo con un anuncio de Adobe Primetime y decisiones
title: Reemplazar intervalos de tiempo con un anuncio de Adobe Primetime y decisiones
uuid: 101ac42d-5ba5-4487-af95-483a6594808a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Reemplazar intervalos de tiempo con un anuncio de Adobe Primetime y decisiones{#replace-time-ranges-with-an-adobe-primetime-ad-decisioning-ad}

Elimine `TimeRanges` entre la `begin` y `end` en `localTime` la línea de tiempo. Sustitúyalo por un AdBreak de `begin` a `begin+replaceDuration`.

Reemplazar intervalos con anuncios de Primetime y decisiones.

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

