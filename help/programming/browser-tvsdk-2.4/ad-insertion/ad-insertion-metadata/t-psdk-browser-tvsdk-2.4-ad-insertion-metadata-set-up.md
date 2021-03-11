---
description: Utilice la clase auxiliar AuditudeSettings para configurar los metadatos de Adobe Primetime y de toma de decisiones.
title: Configurar metadatos de inserción de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Configurar metadatos de inserción de publicidad{#set-up-ad-insertion-metadata}

Utilice la clase auxiliar AuditudeSettings para configurar los metadatos de Adobe Primetime y de toma de decisiones.

>[!TIP]
>
>Anteriormente, la toma de decisiones de anuncios de Adobe Primetime se conocía como Auditude .

1. Cree la instancia `AuditudeSettings`.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Establezca los parámetros de objetivo opcionales, como mediaID, zoneID, dominio y mediaID de Adobe Primetime ad decisioning.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. Cree una instancia de `MediaResource` utilizando la URL del flujo de medios y los metadatos publicitarios creados anteriormente.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. Cargue el objeto `MediaResource` mediante el método `MediaPlayer.replaceCurrentResource(resource)`.

   El `MediaPlayer` comienza a cargar y procesar el manifiesto de flujo de medios.

1. Cuando la `MediaPlayer` transición al estado INITIALIZADO, obtenga las características del flujo de medios en forma de instancia `MediaPlayerItem` a través del atributo `MediaPlayer.CurrentItem`.
1. (Opcional) Consulte la instancia `MediaPlayerItem` para ver si el flujo está activo, independientemente de si tiene pistas de audio alternativas.

   Esta información puede ayudarle a preparar la interfaz de usuario para la reproducción. Por ejemplo, si sabe que hay dos pistas de audio, puede incluir un control de interfaz de usuario que alterne entre estas pistas.

1. Llame a `MediaPlayer.prepareToPlay` para iniciar el flujo de trabajo de publicidad.

   Una vez que los anuncios se han resuelto y colocado en la cronología, `  MediaPlayer ` pasa al estado PREPARADO.
1. Llame a `MediaPlayer.play` para iniciar la reproducción.
El SDK de TVSDK del explorador ahora incluye anuncios cuando se reproduce el contenido.
