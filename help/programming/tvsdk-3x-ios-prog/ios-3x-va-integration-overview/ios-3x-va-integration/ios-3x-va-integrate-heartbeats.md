---
description: Puede configurar el reproductor para que rastree y analice el uso del vídeo.
title: Inicialización y configuración de análisis de vídeo
exl-id: 3f108ca4-2562-4400-b4e2-10933bde3254
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# Inicialización y configuración de análisis de vídeo {#initialize-and-configure-video-analytics}

Puede configurar el reproductor para que rastree y analice el uso del vídeo.

Antes de activar el seguimiento de vídeo (latidos de vídeo), asegúrese de que dispone de lo siguiente:

* TVSDK para iOS
* Información de configuración e inicialización: póngase en contacto con su representante de Adobe para obtener la información específica de su cuenta de seguimiento de vídeo:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json </span> </td> 
   <td colname="col2"> <p>Importante: Este nombre de archivo de configuración JSON debe permanecer <span class="codeph"> ADBMobileConfig.json </span>. No se pueden cambiar el nombre y la ruta de acceso de este archivo de configuración. La ruta a este archivo debe ser <span class="codeph"> &lt;source root=""&gt;/AdobeMobile </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AppMeasurement </span> extremo del servidor de seguimiento </td> 
   <td colname="col2"> La dirección URL del extremo de colección del back-end de Adobe Analytics (anteriormente SiteCatalyst). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Extremo del servidor de seguimiento de análisis de vídeo </td> 
   <td colname="col2"> La URL del punto de conexión de la colección del back-end de Video Analytics. Aquí es donde se envían todas las llamadas de seguimiento de Video Heartbeat. <p>Sugerencia: La URL del servidor de seguimiento de visitantes es la misma que la URL del servidor de seguimiento de Analytics. Para obtener información sobre la implementación del servicio de ID de visitante, consulte <a href="https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en" format="html" scope="external"> Implementación del servicio de ID </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Nombre de cuenta </td> 
   <td colname="col2"> También se conoce como ID del grupo de informes (RSID). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> ID de organización de Marketing Cloud </td> 
   <td colname="col2"> Un valor de cadena necesario para crear una instancia del componente Visitante. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Editor </td> 
   <td colname="col2"> Este es el ID del editor que el representante del Adobe proporciona a los clientes. <p>Sugerencia: Este ID no es solo una cadena con el nombre de la marca o televisión. </p> </td> 
  </tr> 
 </tbody> 
</table>

Para configurar el seguimiento de vídeo en el reproductor:

1. Confirme que las opciones de tiempo de carga en la variable `ADBMobileConfig.json` el archivo de recursos es correcto.

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

   Este archivo de configuración con formato JSON está empaquetado como un recurso con TVSDK. El reproductor solo lee estos valores durante la carga y los valores permanecen constantes mientras se ejecuta la aplicación.

   Para configurar las opciones de tiempo de carga:

   1. Confirme que la variable `ADBMobileConfig.json` contiene los valores apropiados proporcionados por el Adobe.
   1. Confirme que este archivo se encuentra en la `AdobeMobile` carpeta.

      Esta carpeta debe estar ubicada en la raíz del árbol de origen de la aplicación.
   1. Compile y cree su aplicación.
   1. Implemente y ejecute la aplicación agrupada.

      Para obtener más información sobre esta configuración de AppMeasurement, consulte [Medición de vídeo en Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=en).
1. Inicialice y configure los metadatos de seguimiento de Video Heartbeat.

   >[!IMPORTANT]
   >
   >Puede detener el módulo de análisis de vídeo en el flujo medio y reiniciarlo de nuevo según sea necesario. Antes de reiniciar el módulo, asegúrese de que los metadatos de análisis de vídeo también se actualicen a los metadatos de contenido correctos. Para volver a crear los metadatos, repita los subpasos 1 y 2.

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

   1. Añada los metadatos de Video Analytics a la instancia de metadatos global.

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

      Después de crear una instancia de reproductor de contenidos, debe crear una instancia de seguimiento de Video Analytics y proporcionar una referencia a la instancia de reproductor de contenidos.

      >[!TIP]
      >
      >Cree siempre una nueva instancia de rastreador para cada sesión de reproducción de contenido y elimine la referencia anterior después de desasociar la instancia del reproductor de contenido.

      ```
      self.videoAnalyticsTracker =  
        [[[PTVideoAnalyticsTracker alloc] initWithMediaPlayer:self.player] autorelease];
      ```

   1. Destruya el rastreador de Video Analytics.

      Antes de comenzar una nueva sesión de reproducción de contenido, destruya la instancia anterior del rastreador de vídeo. Después de recibir el evento de finalización de contenido (o notificación), espere unos minutos antes de destruir la instancia de seguimiento de vídeo. La destrucción inmediata de la instancia podría interferir con la capacidad del rastreador de Video Analytics para enviar un ping de vídeo completo.

      ```
      self.videoAnalyticsTracker = nil;
      ```

   1. Marca de forma manual como completado el flujo en directo/lineal.

      Si tiene varios episodios en un flujo en directo, puede marcar manualmente un episodio como completado mediante la API completa. Esto finaliza la sesión de seguimiento de vídeo del episodio de vídeo actual y puede iniciar una nueva sesión de seguimiento para el episodio siguiente.

      >[!TIP]
      >
      >Esta API es opcional y no es necesaria para el seguimiento de vídeo de VOD.

      ```
      if (self.videoAnalyticsTracker) 
      { 
         [self.videoAnalyticsTracker trackVideoComplete];   
      }
      ```
