---
description: Puede designar intervalos de tiempo en el contenido de VOD como pausas publicitarias.
seo-description: Puede designar intervalos de tiempo en el contenido de VOD como pausas publicitarias.
seo-title: Marcar rangos
title: Marcar rangos
uuid: eb99a1c2-6c0c-40a4-bac2-98dce45acfad
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Marcar rangos{#mark-ranges}

Puede designar intervalos de tiempo en el contenido de VOD como pausas publicitarias.

En este caso, `TimeRanges` entre `begin` y `end` en `localTime` se marcará como `AdBreak` en la línea de tiempo. Se omiten otras opciones de configuración de publicidad.

>[!NOTE]
>
>Si solo desea marcar determinados rangos en el contenido como anuncios (sin inserción de publicidad dinámica), cree una instancia `CustomRangeMetadata` y especifique el tipo como una operación MARK con los rangos personalizados definidos.

1. Marcar rangos.

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

