---
description: 'null'
seo-description: 'null'
seo-title: Casos de uso especial
title: Casos de uso especial
uuid: 066bc256-4fdf-4083-b23e-0a916b3b532f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Casos de uso especial{#special-use-cases}

TVSDK favorece la configuración de intervalo personalizado en lugar de la configuración de publicidad estándar. Por ejemplo, si se definen intervalos MARK, se ignora la configuración de inserción de la publicidad. Si se definen intervalos REPLACE, TVSDK utiliza automáticamente el modo de `CustomRanges` señalización.

1. `ReplaceRange` sin duración de reemplazo

   Si falta la duración de reemplazo, el servidor determina la duración de reemplazo real. El servidor también determina el número de publicidades colocadas en este `AdBreak` .

   ```
   {
       "properties": [],
       "stream": {
           "manifests": [ {
               "url": "https://. . ./vanilla/index.m3u8",
               "type": "hls"
           } ],
           "metadata": {
               "signaling-mode": "custom time ranges",
               "time-ranges": {
                   "type": "replace",
                   "adjust-seek-position": true,
                   "time-range-list": [{
                   "begin": 0,
                   "end": 30000
               }, {
                   "begin": 60000,
                   "end": 75000
               }, {
                   "begin": 255000,
                   "end": 300000
               } ]
               },
               "ad": {             
                   "domain": "sandbox2.auditude.com",
                   "mediaid": "psdk_000105",
                   "zoneid": "121781"
               }     
           }
       },
       "title": "Verify 30Sec Pre-Roll, 15 Sec Mid roll Ad and 
       45 second Post-Roll can be replaced in one shot.",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_001"
   }
   ```

1. MARCAR y ELIMINAR intervalos con la duración de reemplazo

   Se ignora la duración de reemplazo adicional.
