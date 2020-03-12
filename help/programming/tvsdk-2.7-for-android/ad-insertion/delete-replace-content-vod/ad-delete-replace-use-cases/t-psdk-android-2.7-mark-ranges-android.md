---
description: Puede designar intervalos de tiempo en el contenido de VOD como pausas publicitarias.
seo-description: Puede designar intervalos de tiempo en el contenido de VOD como pausas publicitarias.
seo-title: Marcar rangos
title: Marcar rangos
uuid: 6ae2adee-fb7a-4cef-a8e8-ecf671ed3660
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Marcar rangos {#mark-ranges}

Puede designar intervalos de tiempo en el contenido de VOD como pausas publicitarias.

El `TimeRanges` intervalo entre el `begin` y `end` en `localTime` se marcará como `AdBreak` en la línea de tiempo. Se omiten otras configuraciones de publicidad.

>[!TIP]
>
>Si solo desea marcar determinados rangos en el contenido como anuncios, sin inserción de publicidad dinámica, cree una `CustomRangeMetadata` instancia y especifique el tipo como una `MARK` operación con los rangos personalizados definidos.

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

