---
description: Puede configurar el reproductor para rastrear y analizar el uso del vídeo.
seo-description: Puede configurar el reproductor para rastrear y analizar el uso del vídeo.
seo-title: Inicializar y configurar el análisis de vídeo
title: Inicializar y configurar el análisis de vídeo
uuid: 99c65d0b-ec3b-4a93-8dae-ef612112e510
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Inicializar y configurar el análisis de vídeo{#initialize-and-configure-video-analytics}

Puede configurar el reproductor para rastrear y analizar el uso del vídeo.

Antes de activar el seguimiento de vídeo (Video Heartbeat), asegúrese de que dispone de lo siguiente:

* TVSDK para iOS
* Información de configuración e inicialización: póngase en contacto con su representante de Adobe para obtener información específica sobre su cuenta de seguimiento de vídeo:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json </span> </td> 
   <td colname="col2"> <p>Importante:  Este nombre de archivo de configuración JSON debe ser <span class="codeph"> ADBMobileConfig.json </span>. No se puede cambiar el nombre y la ruta de este archivo de configuración. La ruta de este archivo debe ser <span class="codeph"> &lt;raíz de origen&gt;/AdobeMobile </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> Extremo del servidor de seguimiento de AppMeasurement </span> </td> 
   <td colname="col2"> Dirección URL del extremo de la colección back-end de Adobe Analytics (anteriormente SiteCatalyst). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Extremo del servidor de seguimiento de análisis de vídeo </td> 
   <td colname="col2"> Dirección URL del extremo de la colección back-end de análisis de vídeo. Aquí es donde se envían todas las llamadas de seguimiento de Video Heartbeat. <p>Sugerencia:  La dirección URL del servidor de seguimiento de visitantes es la misma que la del servidor de seguimiento de Analytics. Para obtener información sobre la implementación del servicio de ID de visitante, consulte <a href="https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html" format="html" scope="external"> Implementación del servicio de ID </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Nombre de la cuenta </td> 
   <td colname="col2"> También se conoce como ID del grupo de informes (RSID). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> ID de organización de Marketing Cloud </td> 
   <td colname="col2"> Un valor de cadena necesario para crear instancias del componente Visitante. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Editor </td> 
   <td colname="col2"> Este es el ID de editor que su representante de Adobe proporciona a los clientes. <p>Sugerencia:  Este ID no es sólo una cadena con el nombre de la marca o la televisión. </p> </td> 
  </tr> 
 </tbody> 
</table>

Para configurar el seguimiento de videos en su reproductor:

1. Confirme que las opciones de tiempo de carga del archivo de `ADBMobileConfig.json` recursos son correctas.

   ```
   { 
       "version" : "1.1", 
       "analytics" : { 
           "rsids" : "adobedevelopment", 
           "server" : "10.131.129.149:3000", 
           "charset" : "UTF-8", 
           "ssl" : false, 
           "offlineEnabled" : false, 
           "lifecycleTimeout" : 5, 
           "batchLimit" : 50, 
           "privacyDefault" : "optedin", 
           "poi" : [] 
       }, 
       "marketingCloud": { 
           "org": "ADOBE PROVIDED VALUE"  
       }, 
       "target" : { 
           "clientCode" : "", 
           "timeout" : 5 
       }, 
       "audienceManager" : { 
           "server" : "" 
       } 
   }
   ```

   Este archivo de configuración con formato JSON se incluye como un recurso con TVSDK. El reproductor lee estos valores solo en el momento de la carga y los valores permanecen constantes mientras se ejecuta la aplicación.

   Para configurar las opciones de tiempo de carga:

   1. Confirme que el `ADBMobileConfig.json` archivo contiene los valores adecuados proporcionados por Adobe.
   1. Confirme que este archivo se encuentra en la `AdobeMobile` carpeta.

      Esta carpeta debe estar ubicada en la raíz del árbol de origen de la aplicación.
   1. Compile y cree su aplicación.
   1. Implemente y ejecute la aplicación compilada.

      Para obtener más información sobre esta configuración de AppMeasurement, consulte [Medición de vídeo en Adobe Analytics](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/).
1. Inicialice y configure metadatos de seguimiento de Video Heartbeat.

   >[!IMPORTANT]
   >
   >Puede detener el flujo intermedio del módulo de análisis de vídeo y reinicializarlo de nuevo según sea necesario. Antes de reinicializar el módulo, asegúrese de que los metadatos de análisis de vídeo también se actualizan a los metadatos de contenido correctos. Para volver a crear los metadatos, repita los subpasos 1 y 2.

   1. Cree una instancia de los metadatos de Video Analytics.

      Esta instancia contiene toda la información de configuración necesaria para habilitar el seguimiento de Video Heartbeat. Por ejemplo:

      ```
      - (PTVideoAnalyticsTrackingMetadata *)getVideoAnalyticsTrackingMetadata 
      { 
          PTVideoAnalyticsTrackingMetadata *vaTrackingMetadata =  
            [[[PTVideoAnalyticsTrackingMetadata alloc]  
                 initWithTrackingServer:@"example.com" 
                 publisher:@"sample-publisher"] autorelease]; 
      
          // Set these to NO for production deployment. 
          vaTrackingMetadata.debugLogging = YES;  
          vaTrackingMetadata.quietMode = NO; 
      
          vaTrackingMetadata.channel = @"test-channel"; 
          vaTrackingMetadata.videoName = @"myvideo"; 
          vaTrackingMetadata.videoId = @"myvideoid"; 
          vaTrackingMetadata.playerName = @"PSDK Player"; 
          vaTrackingMetadata.enableChapterTracking = YES; 
          vaTrackingMetadata.useSSL = NO; 
          // use this API to override the default asset length -1 for live streams 
          vaTrackingMetadata.assetDuration = SAMPLE_ASSET_DURATION; 
      
      }
      ```

   1. Agregue los metadatos de Video Analytics a la instancia de metadatos global.

      Cuando esté listo, establezca la instancia de metadatos global en el recurso de medios o en el elemento del reproductor de medios:

      ```
      - (PTMetadata *)createMetadata 
      { 
          PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
      
          [metadata setMetadata:[self getVideoAnalyticsTrackingMetadata]  
            forKey:PTVideoAnalyticsTrackingMetadataKey]; 
      
          return metadata; 
      } 
      
      PTMetadata *metadata = [self createMetadata]; 
      
      PTMediaPlayerItem *item =  
        [[[PTMediaPlayerItem alloc] initWithUrl:[[[NSURL alloc]  
          initWithString:@"media-url"] autorelease] 
          mediaId:@"media-id" metadata:metadata] autorelease];
      ```

   1. Inicialice el rastreador de Video Analytics.

      Después de crear una instancia de reproductor de medios, debe crear una instancia de rastreador de Video Analytics y proporcionar una referencia a la instancia de reproductor de medios.

      >[!TIP]
      >
      >Cree siempre una nueva instancia de rastreador para cada sesión de reproducción de contenido y elimine la referencia anterior después de desconectar la instancia de reproductor multimedia.

      ```
      self.videoAnalyticsTracker =  
        [[[PTVideoAnalyticsTracker alloc] initWithMediaPlayer:self.player] autorelease];
      ```

   1. Destruya el rastreador de Video Analytics.

      Antes de iniciar una nueva sesión de reproducción de contenido, elimine la instancia anterior del rastreador de vídeo. Después de recibir el evento de finalización de contenido (o notificación), espere unos minutos antes de destruir la instancia del rastreador de vídeo. Destruir la instancia inmediatamente podría interferir con la capacidad del rastreador de Video Analytics para enviar un ping de finalización de vídeo.

      ```
      self.videoAnalyticsTracker = nil;
      ```

   1. Marque manualmente el flujo en directo/lineal como completo.

      Si tiene varios episodios en un flujo en directo, puede marcar manualmente un episodio como completado mediante la API completa. Esto finaliza la sesión de seguimiento de vídeo del episodio de vídeo actual y puede iniciar una nueva sesión de seguimiento del siguiente episodio.

      >[!TIP]
      >
      >Esta API es opcional y no es necesaria para el seguimiento de vídeo de VOD.

      ```
      if (self.videoAnalyticsTracker) 
      { 
         [self.videoAnalyticsTracker trackVideoComplete];   
      }
      ```

