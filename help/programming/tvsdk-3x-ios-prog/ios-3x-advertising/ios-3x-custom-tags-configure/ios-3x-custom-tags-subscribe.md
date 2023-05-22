---
description: TVSDK prepara los objetos PTTimedMetadata para las etiquetas suscritas cada vez que se encuentran estos objetos en el manifiesto de contenido.
title: Suscripción a etiquetas personalizadas
exl-id: 5074e622-8824-4253-a668-485e2f68f156
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Suscripción a etiquetas personalizadas {#subscribe-to-custom-tags}

TVSDK prepara los objetos PTTimedMetadata para las etiquetas suscritas cada vez que se encuentran estos objetos en el manifiesto de contenido.

Antes de que comience la reproducción, debe suscribirse a las etiquetas.
Para recibir notificaciones sobre etiquetas personalizadas en manifiestos HLS:

1. Establezca los nombres de etiquetas de publicidad personalizados de forma global pasando una matriz que contenga las etiquetas personalizadas a `setSubscribedTags` in `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >Debe incluir la variable `#` cuando se trabaja con secuencias HLS.

   Por ejemplo:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```
