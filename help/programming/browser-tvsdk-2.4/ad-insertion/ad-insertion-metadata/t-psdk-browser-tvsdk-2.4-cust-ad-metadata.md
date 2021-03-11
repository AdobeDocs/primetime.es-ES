---
description: Puede personalizar los metadatos de inserción de anuncios.
title: Personalizar metadatos de inserción de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Personalizar metadatos de inserción de publicidad{#customize-ad-insertion-metadata}

Puede personalizar los metadatos de inserción de anuncios.

1. Establezca un tiempo de espera en los metadatos publicitarios para las oportunidades no resueltas.

   El valor predeterminado de este tiempo de espera es de 20 segundos.
1. Para cambiar el valor a 10 segundos, escriba lo siguiente:

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   La propiedad `timeout` se define en la clase `AdvertisingMetadata` y este tiempo de espera se puede establecer para cualquier configuración de publicidad personalizada que se derive de la clase `AdvertisingMetadata`. Por ejemplo, si los usuarios definen la configuración personalizada para una resolución de FreeWheel, pueden establecer un tiempo de espera predeterminado mediante esta configuración.

1. Cree `MediaPlayerItemConfig` con la configuración de publicidad en el paso 2.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. Utilice esta configuración cuando llame a `replaceCurrentResource` en `MediaPlayer`.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```

