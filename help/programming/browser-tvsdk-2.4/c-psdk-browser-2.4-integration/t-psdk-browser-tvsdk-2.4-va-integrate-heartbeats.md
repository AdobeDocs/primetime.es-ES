---
description: Puede configurar el reproductor para rastrear y analizar el uso del vídeo.
seo-description: Puede configurar el reproductor para rastrear y analizar el uso del vídeo.
seo-title: Inicializar y configurar el análisis de vídeo
title: Inicializar y configurar el análisis de vídeo
uuid: 4a582b35-ae92-4557-806d-e174fc878cc5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---


# Inicializar y configurar el análisis de vídeo {#initialize-and-configure-video-analytics}

Puede configurar el reproductor para rastrear y analizar el uso del vídeo.

Antes de activar el seguimiento de vídeo (Video Heartbeat), asegúrese de que dispone de lo siguiente:

* Información de configuración/explorador TVSDK de inicialización: póngase en contacto con el representante de Adobe para obtener la información específica de su cuenta de seguimiento de vídeo:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84">
 <tbody>
  <tr>
   <td colname="col1"> Extremo del servidor de seguimiento de AppMeasurement </td>
   <td colname="col2"> Dirección URL del extremo de la colección back-end de Adobe Analytics (anteriormente SiteCatalyst). </td>
  </tr>
  <tr>
   <td colname="col1"> Extremo del servidor de seguimiento de análisis de vídeo </td>
   <td colname="col2"> Dirección URL del extremo de la colección back-end de análisis de vídeo. Aquí es donde se envían todas las llamadas de seguimiento de Video Heartbeat. <p>Sugerencia:  La dirección URL del servidor de seguimiento de visitante es la misma que la del servidor de seguimiento de Analytics. Para obtener información sobre la implementación del servicio de ID de Visitante, consulte <a href="https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html" format="html" scope="external"> Implementación del servicio de ID </a>. </p> </td>
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
   <td colname="col1"> Extremo del servidor de seguimiento de visitante </td>
   <td colname="col2"> Dirección URL del extremo back-end que proporciona un identificador único para el visor de vídeo actual. </td>
  </tr>
  <tr>
   <td colname="col1"> Editor </td>
   <td colname="col2"> Este es el ID del publicador, que su representante de Adobe proporciona a los clientes. <p>Sugerencia:  Este ID no es sólo una cadena con el nombre de la marca o la televisión. </p> </td>
  </tr>
 </tbody>
</table>

Para configurar el seguimiento de videos en su reproductor:

1. Cree una instancia de la biblioteca VisitorAPI y configúrela.

       Tenga en cuenta la siguiente información:
   
   * La creación de instancias requiere un parámetro de entrada de ID de organización de Marketing Cloud proporcionado por Adobe.

      Es un valor de cadena.
   * La única opción de configuración para la biblioteca VisitorAPI es la dirección URL del extremo back-end que proporciona el identificador único para el usuario actual.
   * La dirección URL del servidor de seguimiento de visitante es la misma que la del servidor de seguimiento de Analytics.

      Para obtener información sobre la implementación del servicio de ID de Visitante, consulte [Implementación del servicio de ID de Visitante](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html).

   ```js
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID");
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”;
   ```

2. Cree una instancia del componente AppMeasurement y configúrela.

   La instancia de AppMeasurement tiene muchas opciones de configuración. Para obtener más información, consulte la documentación de [Adobe Analytics Developer](https://microsite.omniture.com/t2/help/en_US/reference/#Developer). Se requieren las opciones del siguiente código de muestra ( `account`, `visitorNamespace` y `trackingServer`) y los valores se proporcionan mediante Adobe.

   >[!IMPORTANT]
   >
   >Debe asegurarse de que la cadena de dependencias está correctamente configurada. La instancia de AppMeasurement agrega (depende de) el componente API de Visitante.

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = 'URL_OF_THE_ADOBE_ANALYTICS_TRACKING_SERVER';
   appMeasurement.account = 'ACCOUNT_NAME'; // Also known as RSID
   appMeasurement.pageName = 'Sample Page Name';
   appMeasurement.charSet = "UTF-8";
   appMeasurement.visitorID = "test-vid";
   ```

   >[!IMPORTANT]
   >
   >En la aplicación, asegúrese de que `appMeasurementObject.visitor` se rellena antes de iniciar el flujo de análisis de vídeo o de que no obtenga ningún resultado de seguimiento. Estos resultados se indican mediante los mensajes del registro. Puede agregar una llamada de seguimiento vacía ( `appMeasurementObject.track`), sondear la propiedad `visitor` hasta que se rellene e iniciar el análisis de vídeo.

3. Inicialice y configure metadatos de seguimiento de Video Heartbeat.

   >[!IMPORTANT]
   >
   >Puede detener el flujo intermedio del módulo de análisis de vídeo y reinicializarlo de nuevo según sea necesario. Antes de reinicializar el módulo, asegúrese de que los metadatos de análisis de vídeo también se actualizan a los metadatos de contenido correctos. Para volver a crear los metadatos, repita los subpasos 1 y 2.

   1. Cree una instancia de los metadatos de Video Analytics.
Esta instancia contiene toda la información de configuración necesaria para habilitar el seguimiento de Video Heartbeat. Por ejemplo:

      ```js
      function getVideoAnalyticsMetadata() {
          var vaObj = new AdobePSDK.VA.VideoAnalyticsMetadata();
          vaObj.appMeasurement = appMeasurement;
          vaObj.trackingServer = 'hbTrackingServer';
          vaObj.publisher = 'hbPublisher';
          vaObj.channel = 'sample-channel';
          vaObj.playerName = 'TVSDK-HTML';
          vaObj.appVersion = '1.0.0';
          vaObj.videoName = 'hbFriendlyName'; // this will overwrite the ContextData variable a.media.friendlyName
          vaObj.assetDuration = durationInSeconds;
          // use this to override the default asset length of -1 for live streams
          vaObj.debugLogging = false;
          return vaObj;
      }
      ```

   2. Después de crear una instancia de reproductor de medios, cree una instancia de rastreador de Video Analytics y proporcione una referencia a la instancia de reproductor de medios.
Recuerde lo siguiente:

      * Cree siempre una nueva instancia de rastreador para cada sesión de reproducción de contenido y elimine la referencia anterior (después de desasociar la instancia del reproductor multimedia).
      * Los metadatos que se crearon en el subpaso 1 deben proporcionarse en el constructor de Video Analytics Tracker.

         ```js
         var videoAnalyticsMetadata = getVideoAnalyticsMetadata();
         videoAnalyticsProvider = new AdobePSDK.VA.VideoAnalyticsProvider(videoAnalyticsMetadata);
         videoAnalyticsProvider.attachMediaPlayer(player);
         ```
   3. Destruya el rastreador de Video Analytics.
Antes de comenzar una nueva sesión de reproducción de contenido, elimine la instancia anterior del rastreador de vídeo. Después de recibir el evento de finalización de contenido (o notificación), espere unos minutos antes de destruir la instancia del rastreador de vídeo. Destruir la instancia inmediatamente podría interferir con la capacidad del rastreador de Video Analytics para enviar un ping de finalización de vídeo.

      ```js
      if (videoAnalyticsProvider) {
          videoAnalyticsProvider.detachMediaPlayer();
          videoAnalyticsProvider = null;
      ```
   4. Marque manualmente el flujo en directo/lineal como completo.
Si tiene varios episodios en un flujo en directo, puede marcar manualmente un episodio como completado mediante la API completa. Esto finaliza la sesión de seguimiento de vídeo para el episodio de vídeo actual y puede crear un inicio de una nueva sesión de seguimiento para el siguiente episodio.
      >[!TIP]
      >
      >Esta API es opcional y no es necesaria para el seguimiento de vídeo de VOD.

      ```js
      if (videoAnalyticsProvider)
      {
         videoAnalyticsProvider.trackVideoComplete();
      videoAnalyticsProvider.detachMediaPlayer();
      videoAnalyticsProvider = null;
      // Create a new instance of VideoAnalyticsProvider to continue tracking.
      } 
      ```
