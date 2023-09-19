---
description: Puede quitar intervalos de tiempo entre inicio y final en localTime de la cronología.
title: Eliminar intervalos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# Eliminar intervalos {#delete-ranges}

Puede eliminar `TimeRanges` entre `begin` y `end` in `localTime` en la cronología.

>[!TIP]
>
>Para eliminar solo ciertos intervalos del contenido, cree un `CustomRangeMetadata` y especifique el tipo como `DELETE` operación con los intervalos personalizados definidos.

El mapa de anuncios debe utilizarse tal como lo define el servidor de publicidad.

1. Para eliminar intervalos con un anuncio de Adobe Primetime ad Decisioning:

   ```
   {   
       "properties": [],
       "stream": {
           "manifests": [
               {
                   "url": "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
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
       "title": "VOD - DELETE TimeRange with xm-replace_text Phrase Ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_003"
   },
   ```
