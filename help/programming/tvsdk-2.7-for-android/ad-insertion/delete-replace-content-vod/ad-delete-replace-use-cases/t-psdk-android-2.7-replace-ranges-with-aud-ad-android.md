---
description: Puede insertar publicidades en el contenido de VOD.
seo-description: Puede insertar publicidades en el contenido de VOD.
seo-title: Reemplazar intervalos de tiempo con una publicidad
title: Reemplazar intervalos de tiempo con una publicidad
uuid: 8f09560c-bca3-4662-bc58-6c9cd0892476
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Reemplazar intervalos de tiempo con una publicidad {#replace-time-ranges-with-an-ad}

Puede insertar publicidades en el contenido de VOD.

Los `TimeRanges` valores entre el `begin` y `end` en `localTime` se eliminan de la línea de tiempo. Estos intervalos se reemplazan por un `AdBreak` de `begin` a `begin+replaceDuration`. Si `replacement-duration` no existe como parámetro, el servidor realiza la determinación en el valor devuelto `Adbreak`.

>[!TIP]
>
>Siempre debe proporcionar un valor `replacement-duration` para los rangos personalizados. Si no hay anuncios que vayan a reemplazar este intervalo personalizado, proporcione un `replacement-duration` 0.

1. Para reemplazar los rangos por anuncios de decisiones y Primetime:

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

