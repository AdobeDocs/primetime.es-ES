---
description: Puede configurar el reproductor para rastrear y analizar el uso del vídeo.
seo-description: Puede configurar el reproductor para rastrear y analizar el uso del vídeo.
seo-title: Inicializar y configurar el análisis de vídeo
title: Inicializar y configurar el análisis de vídeo
uuid: ece5ddc1-3f7b-4878-b1bc-1fec0a459add
translation-type: tm+mt
source-git-commit: 6cb3463be8986d8a1dc718655bd929a0f07ac00d

---


# Inicializar y configurar el análisis de vídeo{#initialize-and-configure-video-analytics}

Puede configurar el reproductor para rastrear y analizar el uso del vídeo.

Antes de activar el seguimiento de vídeo (Video Heartbeat), asegúrese de que dispone de lo siguiente:

* TVSDK para HLS de escritorio
* Información de configuración e inicialización: póngase en contacto con su representante de Adobe para obtener información específica sobre su cuenta de seguimiento de vídeo:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> Extremo del servidor de seguimiento de AppMeasurement </td> 
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
   <td colname="col1"> Extremo del servidor de seguimiento de visitantes </td> 
   <td colname="col2"> Dirección URL del extremo back-end que proporciona un identificador único para el visor de vídeo actual. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Editor </td> 
   <td colname="col2"> Este es el ID de editor que su representante de Adobe proporciona a los clientes. <p>Sugerencia:  Este ID no es sólo una cadena con el nombre de la marca o la televisión. </p> </td> 
  </tr> 
 </tbody> 
</table>

Para configurar el seguimiento de videos en su reproductor:

1. Cree una instancia de la biblioteca VisitorAPI y configúrela.

       Tenga en cuenta la siguiente información:
   
   * La creación de instancias requiere un parámetro de entrada de ID de organización de Marketing Cloud proporcionado por Adobe.

      Es un valor de cadena.
   * La única opción de configuración para la biblioteca VisitorAPI es la dirección URL del extremo back-end que proporciona el identificador único para el usuario actual.
   * La dirección URL del servidor de seguimiento de visitantes es la misma que la del servidor de seguimiento de Analytics.

      Para obtener información sobre la implementación del servicio de ID de visitante, consulte Implementación del servicio de ID de visitante.

   ```
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID"); 
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”; 
   ```

1. Cree una instancia del componente AppMeasurement y configúrela.

   La instancia de AppMeasurement tiene muchas opciones de configuración. Para obtener más información, consulte la documentación para desarrolladores [de](https://microsite.omniture.com/t2/help/en_US/reference/#Developer) Adobe Analytics. Se requieren las opciones del siguiente código de muestra ( `account`, `visitorNamespace`, y `trackingServer`) y Adobe proporciona los valores.

   >[!IMPORTANT]
   >
   >Debe asegurarse de que la cadena de dependencias está correctamente configurada. La instancia de AppMeasurement agrega (depende de) el componente de la API de visitante.

   ```
   // Instantiate and configure AppMeasurement 
   
   // Instantiate AppMeasurement instance only once! 
   if (_appMeasurementObject == null) {  
       _appMeasurementObject = new AppMeasurement(); 
   } 
   
   with (_appMeasurementObject) { 
       account = "ACCOUNT_NAME"; // Also known as RSID 
       trackingServer = "URL_OF_THE_ADOBE_ANALYTICS_TRACKING_SERVER"; 
   
       // Use the same value here as for the Visitor API component 
       visitorNamespace = "MARKETING_CLOUD_ORG_ID"; 
   
       // Attach the Visitor API to the AppMeasurement instance. 
       visitor = _visitor;  
       pageName = "pageName"; 
       charSet = "UTF-8"; 
       currencyCode = "USD"; 
   } 
   ```

   >[!IMPORTANT]
   >
   >En la aplicación, asegúrese de que `appMeasurementObject.visitor` se rellena antes de iniciar el flujo de análisis de vídeo, o bien puede que no obtenga ningún resultado de seguimiento. Estos resultados se indican mediante los mensajes del registro. Puede agregar una llamada de seguimiento vacía ( `appMeasurementObject.track`), sondear la `visitor` propiedad hasta que se rellene e iniciar el análisis de vídeo.

1. Inicialice y configure metadatos de seguimiento de Video Heartbeat.

   >[!IMPORTANT]
   >
   >Puede detener el flujo intermedio del módulo de análisis de vídeo y reinicializarlo de nuevo según sea necesario. Antes de reinicializar el módulo, asegúrese de que los metadatos de análisis de vídeo también se actualizan a los metadatos de contenido correctos. Para volver a crear los metadatos, repita los subpasos 1 y 2.

   1. Cree una instancia de los metadatos de Video Analytics.

      Esta instancia contiene toda la información de configuración necesaria para habilitar el seguimiento de Video Heartbeat. Por ejemplo:

      ```
      private function getVideoAnalyticsTrackingMetadata():VideoAnalyticsMetadata {     
          // Initialize visitor id service and appMeasurement      
          [...] // as shown in the previous steps     
      
          var vaMetadata:VideoAnalyticsMetadata = new VideoAnalyticsMetadata(); 
      
          with (vaMetadata) { 
              trackingServer = "hbTrackingServer"; 
              publisher = "hbPublisher"; 
              channel = "hbChannel";  
              playerName = "hbPlayerName"; 
      
              // this overwrites the ContextData variable a.media.friendlyName 
              videoName = "hbFriendlyName";  
      
              // this will overwrite the ContextData variable a.media.name 
              videoId = "hbName"; 
      
              enableChapterTracking = true; 
      
              // Set these to false for production deployment 
              debugLogging = true;  
              quietMode = false; 
      
          } 
      } 
      ```

   1. Agregue los metadatos de Video Analytics a la instancia de metadatos global.

      Cuando esté listo, establezca la instancia de metadatos global en el recurso de medios o en el elemento del reproductor de medios:

      ```
      var resourceMetadata:Metadata = _player.currentItem.resource.metadata; 
      resourceMetadata.setMetadata(DefaultMetadataKeys.VIDEO_ANALYTICS_METADATA_KEY,  
                                   getVideoAnalyticsTrackingMetadata());
      ```

   1. Inicialice el rastreador de Video Analytics.

      Después de crear una instancia de reproductor de medios, debe crear una instancia de rastreador de Video Analytics y proporcionar una referencia a la instancia de reproductor de medios.

      >[!TIP]
      >
      >Cree siempre una nueva instancia de rastreador para cada sesión de reproducción de contenido y elimine la referencia anterior después de desconectar la instancia de reproductor multimedia.

      ```
      _videoAnalyticsProvider = new VideoAnalyticsProvider(_appMeasurementObject); 
      _videoAnalyticsProvider.attachMediaPlayer(_player);
      ```

   1. Destruya el rastreador de Video Analytics.

      Antes de iniciar una nueva sesión de reproducción de contenido, elimine la instancia anterior del rastreador de vídeo. Después de recibir el evento de finalización de contenido (o notificación), espere unos minutos antes de destruir la instancia del rastreador de vídeo. Destruir la instancia inmediatamente podría interferir con la capacidad del rastreador de Video Analytics para enviar un ping de finalización de vídeo.

      ```
      if (videoAnalyticsTracker) { 
          videoAnalyticsTracker.detachMediaPlayer(); 
          videoAnalyticsTracker = null; 
      }
      ```

   1. Marque manualmente el flujo en directo/lineal como completo.

      Si tiene varios episodios en un flujo en directo, puede marcar manualmente un episodio como completado mediante la API completa. Esto finaliza la sesión de seguimiento de vídeo del episodio de vídeo actual y puede iniciar una nueva sesión de seguimiento del siguiente episodio.

      >[!TIP]
      >
      >Esta API es opcional y no es necesaria para el seguimiento de vídeo de VOD.

