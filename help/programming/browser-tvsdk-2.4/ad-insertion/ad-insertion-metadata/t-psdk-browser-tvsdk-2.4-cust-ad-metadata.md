---
description: Puede personalizar los metadatos de inserción de anuncios.
seo-description: Puede personalizar los metadatos de inserción de anuncios.
seo-title: Personalización de los metadatos de inserción de anuncios
title: Personalización de los metadatos de inserción de anuncios
uuid: 047470d3-45bd-48be-82ce-4e9d9fe6ea10
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Personalización de los metadatos de inserción de anuncios{#customize-ad-insertion-metadata}

Puede personalizar los metadatos de inserción de anuncios.

1. Establezca un tiempo de espera en los metadatos de publicidad para las oportunidades sin resolver.

   El valor predeterminado de este tiempo de espera es de 20 segundos.
1. Para cambiar el valor a 10 segundos, introduzca lo siguiente:

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   La `timeout` propiedad se define en la `AdvertisingMetadata` clase y este tiempo de espera se puede establecer para cualquier configuración de publicidad personalizada que se derive de la `AdvertisingMetadata` clase. Por ejemplo, si los usuarios definen la configuración personalizada para una resolución de FreeWheel, pueden establecer un tiempo de espera predeterminado mediante este ajuste.

1. Cree `MediaPlayerItemConfig` con la configuración de publicidad en el paso 2.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. Utilice esta configuración al llamar `replaceCurrentResource` a `MediaPlayer`.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```

