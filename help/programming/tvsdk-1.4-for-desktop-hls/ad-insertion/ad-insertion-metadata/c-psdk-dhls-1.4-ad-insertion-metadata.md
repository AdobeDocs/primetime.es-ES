---
description: Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y Decisioning, requieren valores de configuración para habilitar la conexión con el proveedor.
title: Metadatos de inserción de publicidad
exl-id: 83c0fd25-dbc3-4529-b81a-16ff78012c80
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# Metadatos de inserción de publicidad {#ad-insertion-metadata}

Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y Decisioning, requieren valores de configuración para habilitar la conexión con el proveedor.

TVSDK incluye la biblioteca de Primetime y Decisioning. Para que el contenido incluya publicidad del servidor de decisiones de publicidad de Primetime, la aplicación debe proporcionar los siguientes datos necesarios `AuditudeSettings` información:

* `mediaID`, que es un identificador único para el vídeo que se va a reproducir.

   El publicador asigna el ID de medios al enviar contenido de vídeo e información de publicidad al servidor de Adobe Primetime ad Decisioning. Primetime ad decisioning utiliza este ID para recuperar del servidor información publicitaria relacionada para el vídeo.

* Su `zoneID`, que se asigna por Adobe, identifica su empresa o sitio web.
* El dominio del servidor de publicidad asignado.
* Otros parámetros de segmentación.

   Puede incluir estos parámetros según sus necesidades y las necesidades del proveedor de publicidad.

## Configuración de metadatos de inserción de publicidad {#set-up-ad-insertion-metadata}

Utilice la clase de ayuda AuditudeSettings , que amplía la clase MetadataNode, para configurar metadatos de Adobe Primetime y Decisioning.

>[!TIP]
>
>Adobe Primetime Ad Decisioning se conocía anteriormente como Auditude.

Los metadatos de publicidad se encuentran en `MediaResource.metadata` propiedad. Al iniciar la reproducción de un nuevo vídeo, la aplicación es responsable de configurar los metadatos de publicidad correctos.

1. Genere el `AuditudeSettings` ejemplo.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. Establezca los parámetros mediaID, zoneID, domain y objetivos opcionales de Adobe Primetime y Decisioning.

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
   >TVSDK consume el ID de medios como una cadena, que se convierte en un valor md5 y se utiliza para `u` en la solicitud de URL de Primetime y Decisioning. Por ejemplo:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Crear un `MediaResource` mediante la URL del flujo de medios y los metadatos de publicidad creados anteriormente.

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. Cargue el `MediaResource` objeto a través de `MediaPlayer.replaceCurrentResource` método.

   El `MediaPlayer` comienza a cargar y procesar el manifiesto de flujo de medios.

1. (Opcional) Consulte la `MediaPlayerItem` para ver si el flujo está activo, independientemente de si tiene pistas de audio alternativas o si está protegido.

   Esta información puede ayudarle a preparar la interfaz de usuario para la reproducción. Por ejemplo, si sabe que hay dos pistas de audio, puede incluir un control de interfaz de usuario que alterne entre estas pistas.

1. Llamada `MediaPlayer.prepareToPlay` para iniciar el flujo de trabajo de publicidad.

   Una vez resueltos los anuncios y colocados en la cronología, la variable `MediaPlayer` pasa al estado PREPARADO.
1. Llamada `MediaPlayer.play` para iniciar la reproducción.

TVSDK ahora incluye anuncios cuando se reproduce el contenido.
