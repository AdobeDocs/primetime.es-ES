---
description: Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.
seo-description: Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.
seo-title: Metadatos de inserción de anuncio
title: Metadatos de inserción de anuncio
uuid: 3eb024c3-4bb5-4bee-943e-fe0c60379e60
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Metadatos de inserción de anuncio {#ad-insertion-metadata}

Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.

TVSDK incluye la biblioteca de decisiones y Primetime. Para que el contenido incluya publicidad del servidor de primetime y de decisiones, la aplicación debe proporcionar la siguiente `AuditudeSettings` información requerida:

* `mediaID`, que es un identificador único para el vídeo que se va a reproducir.

   El editor asigna mediaID al enviar contenido de vídeo e información de publicidad al servidor de decisiones de anuncios de Adobe Primetime. Este ID lo utiliza Primetime y la toma de decisiones para recuperar información de publicidad relacionada para el vídeo desde el servidor.

* El `zoneID`, que es asignado por Adobe, identifica su empresa o sitio web.
* Dominio del servidor de publicidad asignado.
* Otros parámetros de objetivo.

   Puede incluir estos parámetros en función de sus necesidades y las necesidades del proveedor de publicidad.

## Configurar metadatos de inserción de publicidad {#set-up-ad-insertion-metadata}

Utilice la clase auxiliar AuditudeSettings, que amplía la clase MetadataNode, para configurar los metadatos de toma de decisiones y de Adobe Primetime.

>[!TIP]
>
>La toma de decisiones de publicidad de Adobe Primetime se conocía anteriormente como Auditude.

Los metadatos de publicidad están en la `MediaResource.metadata` propiedad. Al iniciar la reproducción de un vídeo nuevo, la aplicación se encarga de configurar los metadatos de publicidad correctos.

1. Cree la `AuditudeSettings` instancia.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. Establezca los parámetros de objetivo opcionales, mediaID, zoneID y dominio de Adobe Primetime y toma de decisiones.

   ```
   auditudeSettings.zoneId = "yourZoneID"; 
   auditudeSettings.mediaId = "media_identifier"; 
   auditudeSettings.domain = "yourAuditudeDomain"; 
   var targetingInfo:Metadata = new Metadata(); 
   targetingInfo.setValue("yourParamName", "yourParamValue"); 
   auditudeSettings.targetingInfo = targetingInfo;
   ```

   >[!TIP]
   >
   >TVSDK consume el ID de medios como una cadena, que se convierte en un valor md5 y se utiliza para el `u` valor en la solicitud de URL de primetime y de decisión. Por ejemplo:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Cree una `MediaResource` instancia utilizando la URL del flujo de medios y los metadatos de publicidad creados anteriormente.

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. Cargue el `MediaResource` objeto a través del `MediaPlayer.replaceCurrentResource` método .

   El `MediaPlayer` inicia la carga y el procesamiento del manifiesto de flujo de medios.

1. (Opcional) Consulte la `MediaPlayerItem` instancia para ver si el flujo está activo, independientemente de si tiene pistas de audio alternativas o de si el flujo está protegido.

   Esta información puede ayudarle a preparar la interfaz de usuario para la reproducción. Por ejemplo, si sabe que hay dos pistas de audio, puede incluir un control de interfaz de usuario que alterne entre estas pistas.

1. Llamar `MediaPlayer.prepareToPlay` para iniciar el flujo de trabajo de publicidad.

   Una vez resueltas y colocadas las publicidades en la línea de tiempo, las `MediaPlayer` transiciones al estado PREPARADO.
1. Llama `MediaPlayer.play` para iniciar la reproducción.

TVSDK ahora incluye anuncios cuando se reproduce el medio.