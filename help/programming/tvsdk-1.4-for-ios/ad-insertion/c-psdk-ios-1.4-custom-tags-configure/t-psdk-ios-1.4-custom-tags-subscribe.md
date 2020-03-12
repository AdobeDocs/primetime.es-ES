---
description: TVSDK prepara objetos PTTimedMetadata para etiquetas suscritas cada vez que estos objetos se encuentran en el manifiesto de contenido.
seo-description: TVSDK prepara objetos PTTimedMetadata para etiquetas suscritas cada vez que estos objetos se encuentran en el manifiesto de contenido.
seo-title: Suscripción a etiquetas personalizadas
title: Suscripción a etiquetas personalizadas
uuid: de66d3db-46d1-485f-9d3a-6e28495bfb13
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Suscripción a etiquetas personalizadas {#subscribe-to-custom-tags}

TVSDK prepara objetos PTTimedMetadata para etiquetas suscritas cada vez que estos objetos se encuentran en el manifiesto de contenido.

Antes de iniciar la reproducción, debe suscribirse a las etiquetas.
Para recibir notificaciones sobre las etiquetas personalizadas en los manifiestos HLS:

1. Configure los nombres de las etiquetas de publicidad personalizadas de forma global pasando una matriz que contenga las etiquetas personalizadas a `setSubscribedTags` en `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >Debe incluir el `#` prefijo al trabajar con flujos HLS.

   Por ejemplo:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```

