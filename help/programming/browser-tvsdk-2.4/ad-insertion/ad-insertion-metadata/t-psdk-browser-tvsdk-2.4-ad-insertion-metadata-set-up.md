---
description: Utilice la clase de ayuda AuditudeSettings para configurar los metadatos de Adobe Primetime y Decisioning.
title: Configuración de metadatos de inserción de publicidad
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Configuración de metadatos de inserción de publicidad{#set-up-ad-insertion-metadata}

Utilice la clase de ayuda AuditudeSettings para configurar los metadatos de Adobe Primetime y Decisioning.

>[!TIP]
>
>Adobe Primetime ad decisioning se conocía anteriormente como Auditude

1. Genere el `AuditudeSettings` ejemplo.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Establezca los parámetros mediaID, zoneID, domain y objetivos opcionales de Adobe Primetime y Decisioning.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. Crear un `MediaResource` mediante la URL del flujo de medios y los metadatos de publicidad creados anteriormente.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. Cargue el `MediaResource` objeto a través de `MediaPlayer.replaceCurrentResource(resource)` método.

   El `MediaPlayer` comienza a cargar y procesar el manifiesto de flujo de medios.

1. Si la variable `MediaPlayer` pasa al estado INITIALIZED, obtenga las características del flujo de medios en forma de `MediaPlayerItem` a través de la `MediaPlayer.CurrentItem` atributo.
1. (Opcional) Consulte la `MediaPlayerItem` para ver si el flujo está activo, independientemente de si tiene pistas de audio alternativas.

   Esta información puede ayudarle a preparar la interfaz de usuario para la reproducción. Por ejemplo, si sabe que hay dos pistas de audio, puede incluir un control de interfaz de usuario que alterne entre estas pistas.

1. Llamada `MediaPlayer.prepareToPlay` para iniciar el flujo de trabajo de publicidad.

   Una vez resueltos los anuncios y colocados en la cronología, la variable `  MediaPlayer ` pasa al estado PREPARADO.
1. Llamada `MediaPlayer.play` para iniciar la reproducción.
El TVSDK del explorador ahora incluye anuncios cuando se reproduce el contenido.
