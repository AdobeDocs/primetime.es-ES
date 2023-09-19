---
description: Elimine intervalos de tiempo entre inicio y final en localTime de la cronología.
title: Eliminar intervalos con el anuncio de Primetime y Decisioning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '42'
ht-degree: 0%

---

# Eliminar intervalos con el anuncio de Primetime y Decisioning{#delete-ranges-with-primetime-ad-decisioning-ad}

Elimine intervalos de tiempo entre inicio y final en localTime de la cronología.

Eliminar intervalos con un anuncio de frase.

```
{   
    "properties": [],
    "stream": {
        "manifests": [ {
            "url": "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
            "type": "hls"
        } ],

        "metadata": {
            "time-ranges": {
                "type": "delete",
                "time-range-list": [ {
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
    "title": "VOD - DELETE TimeRange with Adobe Primetime ad decisioningxm-replace_text Phrase Ads",
    "thumbnail": {
        "large": "https://example.com",
        "small": "https://example.com"
    },
    "type": "vod",
    "id": "vod_003"
}
```
