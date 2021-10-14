---
description: Puede configurar el reproductor para rastrear y analizar el uso de vídeo.
title: Inicializar y configurar Video Analytics
exl-id: e0bf461b-a431-4fba-bd3d-c38be307a92f
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# Inicializar y configurar Video Analytics {#initialize-and-configure-video-analytics}

Puede configurar el reproductor para rastrear y analizar el uso de vídeo.

Antes de activar el seguimiento de vídeo (latidos de vídeo), asegúrese de que dispone de lo siguiente:

* Información de inicialización de TVSDK de configuración/navegador: Póngase en contacto con su representante de Adobe para obtener información específica sobre su cuenta de seguimiento de vídeo:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84">
 <tbody>
  <tr>
   <td colname="col1"> Punto final del servidor de seguimiento de AppMeasurement </td>
   <td colname="col2"> La dirección URL del extremo de recopilación back-end de Adobe Analytics (anteriormente SiteCatalyst). </td>
  </tr>
  <tr>
   <td colname="col1"> Punto final del servidor de seguimiento de Video Analytics </td>
   <td colname="col2"> Dirección URL del extremo de recopilación back-end de video analytics. Aquí es donde se envían todas las llamadas de seguimiento de Video Heartbeat. <p>Sugerencia:  La dirección URL del servidor de seguimiento de visitantes es la misma que la dirección URL del servidor de seguimiento de Analytics. Para obtener información sobre la implementación del servicio de ID de visitante, consulte <a href="https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en" format="html" scope="external"> Implementación del servicio de ID </a>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"> Nombre de la cuenta </td>
   <td colname="col2"> También conocido como ID de grupo de informes (RSID). </td>
  </tr>
  <tr>
   <td colname="col1"> ID de organización de Marketing Cloud </td>
   <td colname="col2"> Un valor de cadena necesario para crear una instancia del componente Visitante. </td>
  </tr>
  <tr>
   <td colname="col1"> Punto final del servidor de seguimiento de visitantes </td>
   <td colname="col2"> Dirección URL del extremo back-end que proporciona un identificador único para el visor de vídeo actual. </td>
  </tr>
  <tr>
   <td colname="col1"> Editor </td>
   <td colname="col2"> Este es el ID del editor que su representante de Adobe proporciona a los clientes. <p>Sugerencia:  Este ID no es solo una cadena con el nombre de marca o televisión. </p> </td>
  </tr>
 </tbody>
</table>

Para configurar el seguimiento de vídeo en el reproductor:

1. Cree una instancia de la biblioteca VisitorAPI y configúrela.

       Tenga en cuenta la siguiente información:
   
   * La creación de instancias requiere un parámetro de entrada de ID de organización de Marketing Cloud proporcionado por el Adobe.

      Es un valor de cadena.
   * La única opción de configuración para la biblioteca VisitorAPI es la URL del extremo back-end que proporciona el identificador único para el usuario actual.
   * La dirección URL del servidor de seguimiento de visitantes es la misma que la dirección URL del servidor de seguimiento de Analytics.

      Para obtener información sobre la implementación del servicio de ID de visitante, consulte [Implementación del servicio de ID de visitante](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en).

   ```js
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID");
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”;
   ```

2. Cree una instancia del componente AppMeasurement y configúrelo.

   La instancia de AppMeasurement tiene muchas opciones de configuración. Para obtener más información, consulte la documentación de [Adobe Analytics Developer](https://microsite.omniture.com/t2/help/en_US/reference/#Developer). Las opciones del siguiente código de muestra ( `account`, `visitorNamespace` y `trackingServer`) son necesarias y los valores se proporcionan mediante Adobe.

   >[!IMPORTANT]
   >
   >Debe asegurarse de que la cadena de dependencias esté correctamente configurada. La instancia de AppMeasurement agrega (depende de) el componente de API de visitante.

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
   >En la aplicación, asegúrese de que `appMeasurementObject.visitor` se rellena antes de iniciar el flujo de análisis de vídeo o de que no se obtengan resultados de seguimiento. Estos resultados se indican mediante los mensajes del registro. Puede agregar una llamada de seguimiento vacía ( `appMeasurementObject.track`), sondear la propiedad `visitor` hasta que se rellene e iniciar Video Analytics.

3. Inicialice y configure metadatos de seguimiento de Video Heartbeat.

   >[!IMPORTANT]
   >
   >Puede detener el flujo intermedio del módulo de análisis de vídeo y reiniciarlo de nuevo según sea necesario. Antes de reiniciar el módulo, asegúrese de que los metadatos de Video Analytics también se actualicen a los metadatos de contenido correctos. Para volver a crear los metadatos, repita los subpasos 1 y 2.

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

   2. Después de crear una instancia de reproductor de medios, cree una instancia de rastreador de Video Analytics y proporcione una referencia a la instancia del reproductor de medios.
Recuerde lo siguiente:

      * Cree siempre una nueva instancia de seguimiento para cada sesión de reproducción de contenido y elimine la referencia anterior (después de separar la instancia del reproductor de medios).
      * Los metadatos creados en el subpaso 1 deben proporcionarse en el constructor de Video Analytics Tracker.

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

   4. Marca de forma manual como completado el flujo en directo/lineal.
Si tiene varios episodios en una emisión en directo, puede marcar manualmente un episodio como completo mediante la API completa. Esto finaliza la sesión de seguimiento de vídeo del episodio de vídeo actual y puede iniciar una nueva sesión de seguimiento para el episodio siguiente.
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
