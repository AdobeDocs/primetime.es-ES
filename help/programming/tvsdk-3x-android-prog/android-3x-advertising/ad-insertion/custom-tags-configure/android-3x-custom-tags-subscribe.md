---
description: TVSDK prepara objetos TimedMetadata para etiquetas suscritas cada vez que estos objetos se encuentran en el manifiesto de contenido.
seo-description: TVSDK prepara objetos TimedMetadata para etiquetas suscritas cada vez que estos objetos se encuentran en el manifiesto de contenido.
seo-title: Suscripción a etiquetas personalizadas
title: Suscripción a etiquetas personalizadas
uuid: f1a934bd-772e-435f-84b5-cb48db23c06e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Suscripción a etiquetas personalizadas {#subscribe-to-custom-tags}

TVSDK prepara objetos TimedMetadata para etiquetas suscritas cada vez que estos objetos se encuentran en el manifiesto de contenido.

Antes de iniciar la reproducción, debe suscribirse a las etiquetas. Para recibir notificaciones sobre las etiquetas personalizadas en los manifiestos HLS:

1. Configure los nombres de las etiquetas de publicidad personalizadas de forma global pasando una matriz que contenga las etiquetas personalizadas a `setSubscribedTags` en `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >Debe incluir el `#` prefijo al trabajar con flujos HLS.

   Por ejemplo:

   ```java
   String[] array = new String[3]; 
   array[0] = "#EXT-X-ASSET"; 
   array[1] = "#EXT-X-BLACKOUT"; 
   array[2] = "#EXT-OATCLS-SCTE35"; 
   MediaPlayerItemConfig.setSubscribedTags(array);
   ```
