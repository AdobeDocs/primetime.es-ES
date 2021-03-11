---
title: Casos de uso especial
description: Casos de uso especial
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# Casos de uso especial{#special-use-cases}

TVSDK prefiere la configuración de intervalos personalizados a la configuración de anuncios estándar. Por ejemplo, si se definen intervalos MARK , se ignora la configuración de inserción de la publicidad. Si se definen intervalos REPLACE, TVSDK utiliza automáticamente el modo de señalización `CustomRanges` .

1. `ReplaceRange` sin duración de reemplazo

   Si falta la duración de la sustitución, el servidor determina la duración real de la sustitución. El número de anuncios colocados en este `AdBreak` también lo determina el servidor.

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

1. MARCA e intervalos de DELETE con duración de reemplazo

   Se ignora la duración de reemplazo adicional.
