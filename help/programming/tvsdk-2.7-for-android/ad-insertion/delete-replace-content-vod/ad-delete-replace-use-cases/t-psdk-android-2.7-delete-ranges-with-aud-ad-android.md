---
description: Puede quitar TimeRanges entre el inicio y el final en localTime de la línea de tiempo.
seo-description: Puede quitar TimeRanges entre el inicio y el final en localTime de la línea de tiempo.
seo-title: Eliminar intervalos
title: Eliminar intervalos
uuid: 637829a7-efa8-4b83-9a04-ef01c043621f
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Eliminar rangos{#delete-ranges}

Puede quitar TimeRanges entre el inicio y el final en localTime de la línea de tiempo.

>[!TIP]
>
>Para eliminar únicamente determinados rangos del contenido, cree una instancia `CustomRangeMetadata` y especifique el tipo como una operación `DELETE` con los rangos personalizados definidos.

La asignación de publicidad debe utilizarse tal como la define el servidor de publicidad.

1. Para eliminar intervalos con una publicidad para la toma de decisiones de publicidad de Adobe Primetime:

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

