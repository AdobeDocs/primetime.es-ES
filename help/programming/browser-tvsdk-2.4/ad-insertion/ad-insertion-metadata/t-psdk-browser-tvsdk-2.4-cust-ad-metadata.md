---
description: Puede personalizar los metadatos de inserción de publicidad.
title: Personalizar metadatos de inserción de publicidad
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Personalizar metadatos de inserción de publicidad{#customize-ad-insertion-metadata}

Puede personalizar los metadatos de inserción de publicidad.

1. Establezca un tiempo de espera en los metadatos de publicidad para las oportunidades sin resolver.

   El valor predeterminado para este tiempo de espera es 20 segundos.
1. Para cambiar el valor a 10 segundos, introduzca lo siguiente:

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   El `timeout` La propiedad se define en `AdvertisingMetadata` y este tiempo de espera se puede establecer para cualquier configuración de publicidad personalizada que se derive de la `AdvertisingMetadata` clase. Por ejemplo, si los usuarios definen una configuración personalizada para una resolución de FreeWheel, pueden establecer un tiempo de espera predeterminado usando esta configuración.

1. Crear `MediaPlayerItemConfig` con la configuración de publicidad del paso 2.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. Utilice esta configuración al llamar a `replaceCurrentResource` el `MediaPlayer`.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```
