---
description: Utilice la clase auxiliar AuditudeSettings, que amplía la clase MetadataNode , para configurar los metadatos de Adobe Primetime y toma de decisiones.
title: Configurar metadatos de inserción de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Configurar metadatos de inserción de publicidad {#set-up-ad-insertion-metadata}

Utilice la clase auxiliar AuditudeSettings, que amplía la clase MetadataNode , para configurar los metadatos de Adobe Primetime y toma de decisiones.

>[!TIP]
>
>Anteriormente, la toma de decisiones de anuncios de Adobe Primetime se conocía como Auditude.

Los metadatos publicitarios están en la propiedad `MediaResource.Metadata` . Al iniciar la reproducción de un nuevo vídeo, la aplicación es responsable de configurar los metadatos publicitarios correctos.

1. Cree la instancia `AuditudeSettings`.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Establezca los parámetros de objetivo opcionales `mediaID`, `zoneID`, `domain` y de toma de decisiones de publicidad de Adobe Primetime.

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
   >TVSDK consume el ID de medios como una cadena, que se convierte en un valor md5 y se utiliza para el valor `u` en la solicitud URL de Primetime y decisioning. Por ejemplo:
   >
   >
   ```
   >https://ad.auditude.com/adserver?
   >u=c76d04ee31c91c4ce5c8cee41006c97d
   >   &z=114100 
   >   &l=20150206141527 
   >   &of=1.4 
   >   &tm=15 
   >   &g=1000002
   >```

1. Cree una instancia de `MediaResource` utilizando la URL del flujo de medios y los metadatos publicitarios creados anteriormente.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. Cargue el objeto `MediaResource` mediante el método `MediaPlayer.replaceCurrentResource`.

   El `MediaPlayer` comienza a cargar y procesar el manifiesto de flujo de medios.

1. Cuando `MediaPlayer` pasa al estado `INITIALIZED`, obtenga las características del flujo de medios en forma de instancia `MediaPlayerItem` mediante el método `MediaPlayer.CurrentItem`.
1. (Opcional) Consulte la instancia `MediaPlayerItem` para ver si el flujo está activo, independientemente de si tiene pistas de audio alternativas o si el flujo está protegido.

   Esta información puede ayudarle a preparar la interfaz de usuario para la reproducción. Por ejemplo, si sabe que hay dos pistas de audio, puede incluir un control de interfaz de usuario que alterne entre estas pistas.

1. Llame a `MediaPlayer.prepareToPlay` para iniciar el flujo de trabajo de publicidad.

   Una vez que los anuncios se han resuelto y colocado en la cronología, la `MediaPlayer` transición al estado `PREPARED`.
1. Llame a `MediaPlayer.play` para iniciar la reproducción.

TVSDK ahora incluye anuncios cuando se reproduce el contenido.
