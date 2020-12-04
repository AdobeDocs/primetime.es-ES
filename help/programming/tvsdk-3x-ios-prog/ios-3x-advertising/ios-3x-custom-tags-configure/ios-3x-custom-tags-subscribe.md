---
description: TVSDK prepara objetos PTTimedMetadata para etiquetas suscritas cada vez que estos objetos se encuentran en el manifiesto de contenido.
seo-description: TVSDK prepara objetos PTTimedMetadata para etiquetas suscritas cada vez que estos objetos se encuentran en el manifiesto de contenido.
seo-title: Suscripción a etiquetas personalizadas
title: Suscripción a etiquetas personalizadas
uuid: e47076b2-6184-4c20-bae4-ba7ae62cf198
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 1%

---


# Suscripción a etiquetas personalizadas {#subscribe-to-custom-tags}

TVSDK prepara objetos PTTimedMetadata para etiquetas suscritas cada vez que estos objetos se encuentran en el manifiesto de contenido.

Antes de los inicios de reproducción, debe suscribirse a las etiquetas.
Para recibir notificaciones sobre las etiquetas personalizadas en los manifiestos HLS:

1. Configure los nombres de etiquetas de publicidad personalizados de forma global pasando una matriz que contenga las etiquetas personalizadas a `setSubscribedTags` en `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >Debe incluir el prefijo `#` al trabajar con flujos HLS.

   Por ejemplo:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```
