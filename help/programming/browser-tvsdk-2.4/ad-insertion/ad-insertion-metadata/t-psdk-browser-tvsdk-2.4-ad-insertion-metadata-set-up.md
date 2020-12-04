---
description: Utilice la clase auxiliar AuditudeSettings para configurar los metadatos de decisiones de anuncios de Adobe Primetime.
seo-description: Utilice la clase auxiliar AuditudeSettings para configurar los metadatos de decisiones de anuncios de Adobe Primetime.
seo-title: Configurar metadatos de inserción de publicidad
title: Configurar metadatos de inserción de publicidad
uuid: fc37e0ae-6acf-4a78-a468-f7b5b123b45e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Configurar metadatos de inserción de publicidad{#set-up-ad-insertion-metadata}

Utilice la clase auxiliar AuditudeSettings para configurar los metadatos de decisiones de anuncios de Adobe Primetime.

>[!TIP]
>
>La toma de decisiones de publicidad de Adobe Primetime se conocía anteriormente como Auditude.

1. Genere la instancia `AuditudeSettings`.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Establezca los parámetros de destino opcionales, mediaID, zoneID, dominio y media de decisión de publicidad de Adobe Primetime.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. Cree una instancia `MediaResource` mediante la URL del flujo de medios y los metadatos de publicidad creados anteriormente.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. Cargue el objeto `MediaResource` mediante el método `MediaPlayer.replaceCurrentResource(resource)`.

   Los inicios `MediaPlayer` que cargan y procesan el manifiesto del flujo de medios.

1. Cuando la `MediaPlayer` transición al estado INITIALIZED, obtenga las características del flujo de medios en forma de una instancia `MediaPlayerItem` a través del atributo `MediaPlayer.CurrentItem`.
1. (Opcional) Consulta la instancia `MediaPlayerItem` para ver si el flujo está activo, independientemente de si tiene pistas de audio alternativas.

   Esta información puede ayudarle a preparar la interfaz de usuario para la reproducción. Por ejemplo, si sabe que hay dos pistas de audio, puede incluir un control de interfaz de usuario que alterne entre estas pistas.

1. Llame a `MediaPlayer.prepareToPlay` para inicio del flujo de trabajo de publicidad.

   Una vez que las publicidades se han resuelto y colocado en la línea de tiempo, las `  MediaPlayer ` transiciones al estado PREPARADO.
1. Llame a `MediaPlayer.play` para inicio de la reproducción.
TVSDK del explorador ahora incluye anuncios cuando se reproduce el medio.
