---
description: Utilice la clase de ayuda AuditudeSettings, que amplía la clase MetadataNode, para configurar metadatos de Adobe Primetime y Decisioning.
title: Configuración de metadatos de inserción de publicidad
exl-id: da5bfdc1-2c55-45f2-b2a8-3e32450cb30d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Configuración de metadatos de inserción de publicidad {#set-up-ad-insertion-metadata}

Utilice la clase de ayuda AuditudeSettings, que amplía la clase MetadataNode, para configurar metadatos de Adobe Primetime y Decisioning.

>[!TIP]
>
>Adobe Primetime Ad Decisioning se conocía anteriormente como Auditude.

Los metadatos de publicidad se encuentran en `MediaResource.Metadata` propiedad. Al iniciar la reproducción de un nuevo vídeo, la aplicación es responsable de configurar los metadatos de publicidad correctos.

1. Genere el `AuditudeSettings` ejemplo.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Configuración de Adobe Primetime y Decisioning `mediaID`, `zoneID`, `<ph conkeyref="phrases/primetime-sdk-name"/>`y los parámetros de segmentación opcionales.

   ```java
   auditudeSettings.setZoneId("yourZoneId"); 
   auditudeSettings.setMediaId("yourVideoId"); 
   auditudeSettings.setDefaultMediaId("defVideoId"); 
   auditudeSettings.setDomain("yourAuditudeDomain"); 
   
   // Optionally set user agent  
   auditudeSettings.setUserAgent("yourUserAgent"); 
   
   Metadata targetingParameters = new Metadata(); 
   targetingParameters.setValue("desired_param", "desired_value"); 
   auditudeSettings.setTargetingParameters(targetingParameters);
   ```

   >[!TIP]
   >
   >TVSDK consume el ID de medios como una cadena, que se convierte en un valor md5 y se utiliza para `u` en la solicitud de URL de Primetime y Decisioning. Por ejemplo:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Crear un `MediaResource` mediante la URL del flujo de medios y los metadatos de publicidad creados anteriormente.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. Cargue el `MediaResource` objeto a través de `MediaPlayer.replaceCurrentResource` método.

   El `MediaPlayer` comienza a cargar y procesar el manifiesto de flujo de medios.

1. Si la variable `MediaPlayer` pasa al estado INITIALIZED, obtenga las características del flujo de medios en forma de `MediaPlayerItem` a través de la `MediaPlayer.CurrentItem` método.
1. (Opcional) Consulte la `MediaPlayerItem` para ver si el flujo está activo, independientemente de si tiene pistas de audio alternativas o si el flujo está protegido.

   Esta información puede ayudarle a preparar la interfaz de usuario para la reproducción. Por ejemplo, si sabe que hay dos pistas de audio, puede incluir un control de interfaz de usuario que alterne entre estas pistas.

1. Llamada `MediaPlayer.prepareToPlay` para iniciar el flujo de trabajo de publicidad.

   Una vez resueltos los anuncios y colocados en la cronología, la variable `MediaPlayer` transiciones a la `PREPARED` estado.
1. Llamada `MediaPlayer.play` para iniciar la reproducción.

TVSDK ahora incluye anuncios cuando se reproduce el contenido.
