---
description: Utilice la clase auxiliar AuditudeSettings para configurar los metadatos de toma de decisiones y de Adobe Primetime.
seo-description: Utilice la clase auxiliar AuditudeSettings para configurar los metadatos de toma de decisiones y de Adobe Primetime.
seo-title: Configurar metadatos de inserción de publicidad
title: Configurar metadatos de inserción de publicidad
uuid: fc37e0ae-6acf-4a78-a468-f7b5b123b45e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Configurar metadatos de inserción de publicidad{#set-up-ad-insertion-metadata}

Utilice la clase auxiliar AuditudeSettings para configurar los metadatos de toma de decisiones y de Adobe Primetime.

>[!TIP]
>
>La toma de decisiones de publicidad de Adobe Primetime se conocía anteriormente como Auditude.

1. Cree la `AuditudeSettings` instancia.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Establezca los parámetros de objetivo opcionales, mediaID, zoneID y dominio de Adobe Primetime y toma de decisiones.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. Cree una `MediaResource` instancia utilizando la URL del flujo de medios y los metadatos de publicidad creados anteriormente.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. Cargue el `MediaResource` objeto a través del `MediaPlayer.replaceCurrentResource(resource)` método .

   El `MediaPlayer` inicia la carga y el procesamiento del manifiesto de flujo de medios.

1. Cuando las `MediaPlayer` transiciones al estado INITIALIZADO, obtenga las características del flujo de medios en forma de una `MediaPlayerItem` instancia a través del `MediaPlayer.CurrentItem` atributo.
1. (Opcional) Consulte la `MediaPlayerItem` instancia para ver si el flujo está activo, independientemente de si tiene pistas de audio alternativas.

   Esta información puede ayudarle a preparar la interfaz de usuario para la reproducción. Por ejemplo, si sabe que hay dos pistas de audio, puede incluir un control de interfaz de usuario que alterne entre estas pistas.

1. Llamar `MediaPlayer.prepareToPlay` para iniciar el flujo de trabajo de publicidad.

   Una vez resueltas y colocadas las publicidades en la línea de tiempo, las `  MediaPlayer ` transiciones al estado PREPARADO.
1. Llama `MediaPlayer.play` para iniciar la reproducción.
TVSDK del explorador ahora incluye anuncios cuando se reproduce el medio.
