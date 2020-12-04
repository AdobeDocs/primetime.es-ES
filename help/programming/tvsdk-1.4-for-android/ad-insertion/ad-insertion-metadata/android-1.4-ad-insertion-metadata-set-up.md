---
description: Utilice la clase auxiliar AuditudeSettings, que amplía la clase MetadataNode, para configurar los metadatos de decisiones de publicidad de Adobe Primetime.
seo-description: Utilice la clase auxiliar AuditudeSettings, que amplía la clase MetadataNode, para configurar los metadatos de decisiones de publicidad de Adobe Primetime.
seo-title: Configurar metadatos de inserción de publicidad
title: Configurar metadatos de inserción de publicidad
uuid: d96e67c3-4cc7-4309-a2a2-ff5193b46534
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# Configurar metadatos de inserción de publicidad {#set-up-ad-insertion-metadata}

Utilice la clase auxiliar AuditudeSettings, que amplía la clase MetadataNode, para configurar los metadatos de decisiones de publicidad de Adobe Primetime.

>[!TIP]
>
>La toma de decisiones de publicidad de Adobe Primetime se conocía anteriormente como Auditude.

Los metadatos de publicidad están en la propiedad `MediaResource.Metadata`. Al iniciar la reproducción de un vídeo nuevo, la aplicación se encarga de configurar los metadatos de publicidad correctos.

1. Genere la instancia `AuditudeSettings`.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Configure los parámetros de objetivo opcionales, `mediaID`, `zoneID`, `domain` y las decisiones de publicidad de Adobe Primetime.

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
   >TVSDK consume el ID de medios como una cadena, que se convierte en un valor md5 y se utiliza para el valor `u` en la solicitud de URL de Primetime y decisoria. Por ejemplo:
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

1. Cree una instancia `MediaResource` mediante la URL del flujo de medios y los metadatos de publicidad creados anteriormente.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. Cargue el objeto `MediaResource` mediante el método `MediaPlayer.replaceCurrentResource`.

   Los inicios `MediaPlayer` que cargan y procesan el manifiesto del flujo de medios.

1. Cuando `MediaPlayer` transición al estado `INITIALIZED`, obtenga las características del flujo de medios en forma de una instancia `MediaPlayerItem` mediante el método `MediaPlayer.CurrentItem`.
1. (Opcional) Consulta la instancia `MediaPlayerItem` para ver si el flujo está activo, independientemente de si tiene pistas de audio alternativas o de si el flujo está protegido.

   Esta información puede ayudarle a preparar la interfaz de usuario para la reproducción. Por ejemplo, si sabe que hay dos pistas de audio, puede incluir un control de interfaz de usuario que alterne entre estas pistas.

1. Llame a `MediaPlayer.prepareToPlay` para inicio del flujo de trabajo de publicidad.

   Una vez que las publicidades se han resuelto y colocado en la línea de tiempo, la `MediaPlayer` transición al estado `PREPARED`.
1. Llame a `MediaPlayer.play` para inicio de la reproducción.

TVSDK ahora incluye anuncios cuando se reproduce el medio.
