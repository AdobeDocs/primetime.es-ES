---
description: TVSDK prepara los objetos TimedMetadata para las etiquetas suscritas cada vez que se encuentran estos objetos en el manifiesto de contenido.
title: Suscripción a etiquetas personalizadas
exl-id: faefcefb-e52f-4e32-859a-7da4284ca52e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
