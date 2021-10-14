---
title: Inicializar y configurar Video Analytics
description: Inicializar y configurar Video Analytics
copied-description: true
exl-id: 26bdc11e-b8f6-414f-a3e9-53bc895d25ce
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Inicializar y configurar Video Analytics {#initialize-and-configure-video-analytics}

Puede configurar el reproductor para rastrear y analizar el uso de vídeo.
Antes de activar el seguimiento de vídeo (latidos de vídeo), asegúrese de que dispone de lo siguiente:

* TVSDK 3.0 para Android.
* Información de configuración/inicialización

   Póngase en contacto con su representante de Adobe para obtener información específica sobre su cuenta de seguimiento de vídeo:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json  </span> </td> 
   <td colname="col2"> <p>Importante:  Este nombre de archivo de configuración JSON debe permanecer <span class="filepath"> ADBMobileConfig.json </span>. El nombre y la ruta de este archivo de configuración no se pueden cambiar. La ruta a este archivo debe ser <span class="filepath"> &lt;source root&gt;/assets </span>. </p> </td> 
  </tr> 
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
 </tbody> 
</table>

Para configurar el seguimiento de vídeo en el reproductor:

1. Confirme que las opciones de tiempo de carga del archivo de recursos `ADBMobileConfig.json` son correctas.

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

   Este archivo de configuración con formato JSON está empaquetado como un recurso con TVSDK. El reproductor lee estos valores solo en el momento de la carga y los valores permanecen constantes mientras se ejecuta la aplicación.

   Para configurar las opciones de tiempo de carga:


   1. Confirme que el archivo `ADBMobileConfig.json` contiene los valores adecuados (proporcionados por el Adobe).
   1. Confirme que este archivo se encuentra en la carpeta `assets/`.

      Esta carpeta debe estar ubicada en la raíz del árbol de origen de la aplicación.

   1. Compile y cree la aplicación.
   1. Implemente y ejecute la aplicación agrupada.

      Para obtener más información sobre esta configuración de AppMeasurement, consulte [Medición de vídeo en Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=en).

1. Inicialice y configure metadatos de seguimiento de Video Heartbeat.

   >[!IMPORTANT]
   >
   >Puede detener el flujo intermedio del módulo de análisis de vídeo y reiniciarlo de nuevo según sea necesario. Antes de reiniciar el módulo, asegúrese de que los metadatos de Video Analytics también se actualicen a los metadatos de contenido correctos. Para volver a crear los metadatos, repita los dos primeros pasos a continuación (subpasos **a** y **b**).

   1. Cree una instancia de los metadatos de Video Analytics.

      Esta instancia contiene toda la información de configuración necesaria para habilitar el seguimiento de Video Heartbeat. Por ejemplo:

      ```java
      private VideoAnalyticsMetadata getVideoAnalyticsTrackingMetadata() { 
          VideoAnalyticsMetadata vaMetadata = new VideoAnalyticsMetadata(); 
      
          vaMetadata.setTrackingServer("example.com"); 
          vaMetadata.setChannel("test-channel"); 
          vaMetadata.setVideoName("myvideo"); 
          vaMetadata.setVideoId("myvideoid"); 
          vaMetadata.setPlayerName("PSDK Player"); 
          vaMetadata.setUseSSL(false); 
          vaMetadata.debugLogging = true; // Set to NO for production deployment. 
          vaMetadata.setEnableChapterTracking(true); 
          // use this API to override the default asset length -1 for live streams 
          vaMetadata.setAssetDuration(SAMPLE_ASSET_DURATION); 
      
          return vaMetadata; 
      }
      ```

   1. Inicialice el proveedor de Video Analytics.

      Después de crear una instancia de reproductor de medios, debe crear una instancia de proveedor de Video Analytics y proporcionar el contexto de la aplicación.

      >[!TIP]
      >
      >Cree siempre una instancia de proveedor nueva para cada sesión de reproducción de contenido y elimine la referencia anterior después de separar la instancia del reproductor de medios.

      ```java
      VideoAnalyticsProvider videoAnalyticsProvider = new VideoAnalyticsProvider(appContext); 
      ```

   1. Configure los metadatos de Video Analytics en la instancia `videoAnalyticsProvider` .

      ```java
      videoAnalyticsProvider.setVideoAnalyticsMetadata(vaMetadata);
      ```

   1. Adjunte la instancia del reproductor de medios a la instancia `videoAnalyticsProvider` :

      ```java
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. Destruya el proveedor de Video Analytics.

      Antes de comenzar una nueva sesión de reproducción de contenido, elimine la instancia anterior del proveedor de vídeo. Después de recibir el evento de finalización de contenido (o notificación), espere unos minutos antes de destruir la instancia del proveedor de análisis de vídeo. Destruir la instancia inmediatamente podría interferir con la capacidad del proveedor de Video Analytics para enviar un ping de &quot;vídeo completado&quot;.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.detachMediaPlayer(); 
          videoAnalyticsProvider = null; 
      }
      ```

   1. Marca de forma manual como completado el flujo en directo/lineal.

      Si tiene varios episodios en una emisión en directo, puede marcar manualmente un episodio como completo mediante la API completa. Esto finaliza la sesión de seguimiento de vídeo del episodio de vídeo actual y puede iniciar una nueva sesión de seguimiento para el episodio siguiente.

      >[!TIP]
      >
      >Esta API es opcional y no funciona para el seguimiento de vídeo de VOD.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.trackVideoComplete();    
      }
      ```
