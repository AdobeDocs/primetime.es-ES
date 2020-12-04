---
description: 'null'
seo-description: 'null'
seo-title: Inicializar y configurar el análisis de vídeo
title: Inicializar y configurar el análisis de vídeo
uuid: 98017a20-4997-42f7-9b03-fd9c4b6ccd92
translation-type: tm+mt
source-git-commit: 1985694f99c548284aad6e6b4e070bece230bdf4
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---


# Inicializar y configurar el análisis de vídeo {#initialize-and-configure-video-analytics}

Puede configurar el reproductor para rastrear y analizar el uso del vídeo.
Antes de activar el seguimiento de vídeo (Video Heartbeat), asegúrese de que dispone de lo siguiente:

* TVSDK 2.5 para Android.
* Información de configuración e inicialización

   Póngase en contacto con su representante de Adobe para obtener información específica sobre su cuenta de seguimiento de vídeo:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json  </span> </td> 
   <td colname="col2"> <p>Importante:  Este nombre de archivo de configuración JSON debe permanecer <span class="filepath"> ADBMobileConfig.json </span>. No se puede cambiar el nombre y la ruta de este archivo de configuración. La ruta a este archivo debe ser <span class="filepath"> &lt;raíz de origen&gt;/assets </span>. </p> </td> 
  </tr> 
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
 </tbody> 
</table>

Para configurar el seguimiento de videos en su reproductor:

1. Confirme que las opciones de tiempo de carga en el archivo de recursos `ADBMobileConfig.json` son correctas.

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


   1. Confirme que el archivo `ADBMobileConfig.json` contiene los valores adecuados (proporcionados por Adobe).
   1. Confirme que este archivo se encuentra en la carpeta `assets/`.

      Esta carpeta debe estar ubicada en la raíz del árbol de origen de la aplicación.

   1. Compile y cree su aplicación.
   1. Implemente y ejecute la aplicación compilada.

      Para obtener más información sobre esta configuración de AppMeasurement, consulte [Medición de vídeo en Adobe Analytics](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/).

1. Inicialice y configure metadatos de seguimiento de Video Heartbeat.

   >[!IMPORTANT]
   >
   >Puede detener el flujo intermedio del módulo de análisis de vídeo y reinicializarlo de nuevo según sea necesario. Antes de reinicializar el módulo, asegúrese de que los metadatos de análisis de vídeo también se actualizan a los metadatos de contenido correctos. Para volver a crear los metadatos, repita los dos primeros pasos a continuación (subpasos **a** y **b**).

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

      Después de crear una instancia de reproductor de medios, debe crear una instancia de proveedor de Video Analytics y proporcionarle el contexto de la aplicación.

      >[!TIP]
      >
      >Cree siempre una nueva instancia de proveedor para cada sesión de reproducción de contenido y elimine la referencia anterior después de desconectar la instancia de reproductor de medios.

      ```java
      VideoAnalyticsProvider videoAnalyticsProvider = new VideoAnalyticsProvider(appContext); 
      ```

   1. Defina los metadatos de Video Analytics en la instancia `videoAnalyticsProvider`.

      ```java
      videoAnalyticsProvider.setVideoAnalyticsMetadata(vaMetadata);
      ```

   1. Adjunte la instancia del reproductor multimedia a la instancia `videoAnalyticsProvider`:

      ```java
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. Destruya el proveedor de Video Analytics.

      Antes de iniciar una nueva sesión de reproducción de contenido, elimine la instancia anterior del proveedor de vídeo. Después de recibir el evento de finalización de contenido (o notificación), espere unos minutos antes de destruir la instancia del proveedor de análisis de vídeo. La destrucción inmediata de la instancia podría interferir con la capacidad del proveedor de Video Analytics para enviar un ping de &quot;vídeo completado&quot;.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.detachMediaPlayer(); 
          videoAnalyticsProvider = null; 
      }
      ```

   1. Marque manualmente el flujo en directo/lineal como completo.

      Si tiene varios episodios en un flujo en directo, puede marcar manualmente un episodio como completado mediante la API completa. Esto finaliza la sesión de seguimiento de vídeo para el episodio de vídeo actual y puede crear un inicio de una nueva sesión de seguimiento para el siguiente episodio.

      >[!TIP]
      >
      >Esta API es opcional y no funciona para el seguimiento de vídeo VOD.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.trackVideoComplete();    
      }
      ```

