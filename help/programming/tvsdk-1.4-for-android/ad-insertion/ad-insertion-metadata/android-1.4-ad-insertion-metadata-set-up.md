---
description: Utilice la clase auxiliar AuditudeSettings, que amplía la clase MetadataNode, para configurar los metadatos de toma de decisiones y de Adobe Primetime.
seo-description: Utilice la clase auxiliar AuditudeSettings, que amplía la clase MetadataNode, para configurar los metadatos de toma de decisiones y de Adobe Primetime.
seo-title: Configurar metadatos de inserción de publicidad
title: Configurar metadatos de inserción de publicidad
uuid: d96e67c3-4cc7-4309-a2a2-ff5193b46534
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f

---


# Configurar metadatos de inserción de publicidad {#set-up-ad-insertion-metadata}

Utilice la clase auxiliar AuditudeSettings, que amplía la clase MetadataNode, para configurar los metadatos de toma de decisiones y de Adobe Primetime.

>[!TIP]
>
>La toma de decisiones de publicidad de Adobe Primetime se conocía anteriormente como Auditude.

Los metadatos de publicidad están en la `MediaResource.Metadata` propiedad. Al iniciar la reproducción de un vídeo nuevo, la aplicación se encarga de configurar los metadatos de publicidad correctos.

1. Cree la `AuditudeSettings` instancia.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Defina los parámetros de toma de decisiones `mediaID``zoneID`, `domain`y objetivos opcionales de Adobe Primetime.

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
   >TVSDK consume el ID de medios como una cadena, que se convierte en un valor md5 y se utiliza para el `u` valor en la solicitud de URL de primetime y de decisión. Por ejemplo:
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

1. Cree una `MediaResource` instancia utilizando la URL del flujo de medios y los metadatos de publicidad creados anteriormente.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. Cargue el `MediaResource` objeto a través del `MediaPlayer.replaceCurrentResource` método .

   El `MediaPlayer` inicia la carga y el procesamiento del manifiesto de flujo de medios.

1. Cuando las `MediaPlayer` transiciones al `INITIALIZED` estado, obtenga las características del flujo de medios en forma de `MediaPlayerItem` instancia a través del `MediaPlayer.CurrentItem` método .
1. (Opcional) Consulte la `MediaPlayerItem` instancia para ver si el flujo está activo, independientemente de si tiene pistas de audio alternativas o de si el flujo está protegido.

   Esta información puede ayudarle a preparar la interfaz de usuario para la reproducción. Por ejemplo, si sabe que hay dos pistas de audio, puede incluir un control de interfaz de usuario que alterne entre estas pistas.

1. Llamar `MediaPlayer.prepareToPlay` para iniciar el flujo de trabajo de publicidad.

   Una vez resueltas y colocadas las publicidades en la línea de tiempo, las `MediaPlayer` transiciones al `PREPARED` estado.
1. Llama `MediaPlayer.play` para iniciar la reproducción.

TVSDK ahora incluye anuncios cuando se reproduce el medio.
