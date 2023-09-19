---
description: TVSDK prepara los objetos TimedMetadata para las etiquetas suscritas cada vez que se encuentran estos objetos en el manifiesto de contenido.
title: Suscripción a etiquetas personalizadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Suscripción a etiquetas personalizadas {#subscribe-to-custom-tags}

TVSDK prepara los objetos TimedMetadata para las etiquetas suscritas cada vez que se encuentran estos objetos en el manifiesto de contenido.

Antes de que comience la reproducción, debe suscribirse a las etiquetas. Para recibir notificaciones sobre etiquetas personalizadas en manifiestos HLS:

1. Establezca los nombres de etiquetas de publicidad personalizados de forma global pasando una matriz que contenga las etiquetas personalizadas a `setSubscribedTags` in `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >Debe incluir la variable `#` cuando se trabaja con secuencias HLS.

   Por ejemplo:

   ```java
   String[] array = new String[3]; 
   array[0] = "#EXT-X-ASSET"; 
   array[1] = "#EXT-X-BLACKOUT"; 
   array[2] = "#EXT-OATCLS-SCTE35"; 
   MediaPlayerItemConfig.setSubscribedTags(array);
   ```
