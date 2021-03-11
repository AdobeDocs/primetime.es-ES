---
description: Puede insertar anuncios en contenido de VOD.
title: Reemplazar intervalos de tiempo por una publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# Reemplazar intervalos de tiempo por un anuncio {#replace-time-ranges-with-an-ad}

Puede insertar anuncios en contenido de VOD.

Los `TimeRanges` entre `begin` y `end` en `localTime` se eliminan de la cronología. Estos intervalos se sustituyen por un `AdBreak` de `begin` a `begin+replaceDuration`. Si el `replacement-duration` no existe como parámetro, el servidor realiza la determinación en el `Adbreak` devuelto.

>[!TIP]
>
>Siempre debe proporcionar un `replacement-duration` para intervalos personalizados. Si no hay anuncios que vayan a reemplazar este intervalo personalizado, proporcione un `replacement-duration` de 0.

1. Para reemplazar los intervalos con anuncios de Primetime y decisioningads:

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
                   "type": "replace",
                   "time-range-list": [
                       {
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
       "title": "VOD - Replace TimeRange with Auditude Ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_003"
   }
   ```
