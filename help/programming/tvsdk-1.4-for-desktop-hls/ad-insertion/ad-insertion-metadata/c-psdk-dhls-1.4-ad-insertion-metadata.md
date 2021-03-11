---
description: Para permitir que funcione la resolución de anuncios, los proveedores de anuncios, como Adobe Primetime y la toma de decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.
title: Metadatos de inserción de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# Metadatos de inserción de publicidad {#ad-insertion-metadata}

Para permitir que funcione la resolución de anuncios, los proveedores de anuncios, como Adobe Primetime y la toma de decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.

TVSDK incluye la biblioteca de Primetime y decisioning. Para que el contenido incluya publicidad del servidor de primetime y decisiones, la aplicación debe proporcionar la siguiente información requerida: `AuditudeSettings`

* `mediaID`, que es un identificador único para el vídeo que se reproducirá.

   El editor asigna el mediaID al enviar contenido de vídeo e información de publicidad al servidor de Adobe Primetime ad decisioning. Primetime ad decisioning utiliza este ID para recuperar información publicitaria relacionada del vídeo del servidor.

* El `zoneID`, que se asigna por Adobe, identifica a su empresa o sitio web.
* Dominio del servidor de publicidad asignado.
* Otros parámetros de segmentación.

   Puede incluir estos parámetros en función de sus necesidades y las necesidades del proveedor de publicidad.

## Configurar metadatos de inserción de publicidad {#set-up-ad-insertion-metadata}

Utilice la clase auxiliar AuditudeSettings , que amplía la clase MetadataNode , para configurar los metadatos de Adobe Primetime y toma de decisiones.

>[!TIP]
>
>Anteriormente, la toma de decisiones de anuncios de Adobe Primetime se conocía como Auditude.

Los metadatos publicitarios están en la propiedad `MediaResource.metadata` . Al iniciar la reproducción de un nuevo vídeo, la aplicación es responsable de configurar los metadatos publicitarios correctos.

1. Cree la instancia `AuditudeSettings`.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. Establezca los parámetros de objetivo opcionales, como mediaID, zoneID, dominio y mediaID de Adobe Primetime ad decisioning.

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
   >TVSDK consume el ID de medios como una cadena, que se convierte en un valor md5 y se utiliza para el valor `u` en la solicitud URL de Primetime y decisioning. Por ejemplo:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Cree una instancia de `MediaResource` utilizando la URL del flujo de medios y los metadatos publicitarios creados anteriormente.

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. Cargue el objeto `MediaResource` mediante el método `MediaPlayer.replaceCurrentResource`.

   El `MediaPlayer` comienza a cargar y procesar el manifiesto de flujo de medios.

1. (Opcional) Consulte la instancia `MediaPlayerItem` para ver si el flujo está activo, independientemente de si tiene pistas de audio alternativas o si el flujo está protegido.

   Esta información puede ayudarle a preparar la interfaz de usuario para la reproducción. Por ejemplo, si sabe que hay dos pistas de audio, puede incluir un control de interfaz de usuario que alterne entre estas pistas.

1. Llame a `MediaPlayer.prepareToPlay` para iniciar el flujo de trabajo de publicidad.

   Una vez que los anuncios se han resuelto y colocado en la cronología, `MediaPlayer` pasa al estado PREPARADO.
1. Llame a `MediaPlayer.play` para iniciar la reproducción.

TVSDK ahora incluye anuncios cuando se reproduce el contenido.