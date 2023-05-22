---
title: Casos de uso especiales
description: Casos de uso especiales
copied-description: true
exl-id: 33aad8cc-5939-4890-bc89-32d6bbf1fa4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# Casos de uso especiales{#special-use-cases}

TVSDK prefiere la configuración de intervalo personalizado a la configuración de anuncio estándar. Por ejemplo, si se definen intervalos MARK, se ignoran los ajustes de inserción del anuncio. Si se definen intervalos REPLACE, TVSDK utiliza automáticamente la variable `CustomRanges` modo de señalización.

1. `ReplaceRange` sin duración de reemplazo

   Si falta la duración de reemplazo, el servidor determina la duración real de reemplazo. El número de anuncios colocados en este `AdBreak` también lo determina el servidor.

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

1. Intervalos de MARCA y DELETE con duración de sustitución

   Se ignora la duración de reemplazo adicional.
