---
description: Puede quitar TimeRanges entre el inicio y el final en localTime de la línea de tiempo.
seo-description: Puede quitar TimeRanges entre el inicio y el final en localTime de la línea de tiempo.
seo-title: Eliminar intervalos
title: Eliminar intervalos
uuid: 2aaea7a0-5d52-49a1-901c-f71e4b081d91
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Eliminar intervalos {#delete-ranges}

Puede eliminar `TimeRanges` entre `begin` y `end` en `localTime` la línea de tiempo.

>[!TIP]
>
>Para eliminar únicamente determinados rangos del contenido, cree una `CustomRangeMetadata` instancia y especifique el tipo como una `DELETE` operación con los rangos personalizados definidos.

La asignación de publicidad debe utilizarse tal como la define el servidor de publicidad.

1. Para eliminar intervalos con una publicidad de decisiones de anuncios de Adobe Primetime:

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
