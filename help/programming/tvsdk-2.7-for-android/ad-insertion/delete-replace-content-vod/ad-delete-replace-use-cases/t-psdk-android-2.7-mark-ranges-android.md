---
description: Puede designar intervalos de tiempo en el contenido de VOD como pausas publicitarias.
title: Marcar rangos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---


# Marcar rangos {#mark-ranges}

Puede designar intervalos de tiempo en el contenido de VOD como pausas publicitarias.

El `TimeRanges` entre `begin` y `end` en `localTime` se marcará como un `AdBreak` en la cronología. Se ignoran otras configuraciones de publicidad.

>[!TIP]
>
>Si solo desea marcar ciertos intervalos en el contenido como anuncios, sin inserción de publicidad dinámica, cree una instancia `CustomRangeMetadata` y especifique el tipo como una operación `MARK` con los intervalos personalizados definidos.

1. Marca los intervalos:

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
                   "type": "mark",
               "adjust-seek-position" : true,   
                   "time-range-list": [
                     {
                        "begin": 0,
                        "end": 15000
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
   
                 }
            }           
       },   
       "title": "VOD - MARK TimeRanges and no ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
          },
       "type": "vod",
       "id": "vod_004"
   }
   ```

