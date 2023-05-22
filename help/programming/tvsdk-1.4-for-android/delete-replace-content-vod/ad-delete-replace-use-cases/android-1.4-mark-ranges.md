---
description: Puede designar intervalos de tiempo en el contenido de VOD como pausas publicitarias.
title: Marcar intervalos
exl-id: cd661327-20b2-4a49-8002-6ecee86c2a2c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Marcar intervalos{#mark-ranges}

Puede designar intervalos de tiempo en el contenido de VOD como pausas publicitarias.

En este caso, `TimeRanges` entre los `begin` y `end` in `localTime` se marcará como una `AdBreak` en la cronología. Se ignoran otras configuraciones de publicidad.

>[!NOTE]
>
>Si solo desea marcar ciertos intervalos del contenido como anuncios (sin inserción de publicidad dinámica), cree un `CustomRangeMetadata` y especifique el tipo como una operación MARK con los intervalos personalizados definidos.

1. Marcar intervalos.

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
                   "type": "mark",
                   "adjust-seek-position" : true,   
                   "time-range-list": [ {
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
                    } ]
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
