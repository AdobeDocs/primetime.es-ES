---
description: Estas clases proporcionan información que le ayuda a determinar el rendimiento del reproductor.
title: Clases de QoS
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Clases de QoS {#qos-classes}

Estas clases proporcionan información que le ayuda a determinar el rendimiento del reproductor.

Paquete: [com.adobe.mediacore.qos](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/package-detail.html)  Paquete: [com.adobe.mediacore.qos.metrics](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Nombre </th> 
   <th colname="2" class="entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/BufferingMetrics.html" format="html" scope="external"> Métricas de almacenamiento en búfer</a></span> </td> 
   <td colname="2"> Proporciona información sobre cuánto tiempo ha invertido el reproductor en el almacenamiento en búfer y con qué frecuencia se ha producido un evento de almacenamiento en búfer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/DeviceInformation.html" format="html" scope="external"> DeviceInformation</a></span> </td> 
   <td colname="2">Proporciona información sobre la plataforma y el sistema operativo en los que se ejecuta TVSDK: 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">Versión del sistema operativo de la plataforma </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">Número de versión de la biblioteca TVSDK </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">Nombre del modelo del dispositivo </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">Nombre del fabricante del dispositivo </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">UUID del dispositivo </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">Anchura/altura de la pantalla del dispositivo </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/LoadInformation.html" format="html" scope="external"> LoadInformation</a></span> </td> 
   <td colname="2"> Contiene información de QoS variada sobre la carga de varios recursos (archivos, manifiestos o listas de reproducción, fragmentos/segmentos, pistas, etc.). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/LoadInformationType.html" format="html" scope="external"> LoadInformationType</a></span> </td> 
   <td colname="2"> Clase de enumeración que enumera los posibles valores de la propiedad de tipo de los objetos LoadInformation. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/PlaybackInformation.html" format="html" scope="external"> InformaciónDeReproducción</a></span> </td> 
   <td colname="2"> Proporciona información sobre el rendimiento de la reproducción. Esto incluye la velocidad de fotogramas, la velocidad de bits de perfil, el tiempo total empleado en el almacenamiento en búfer, el número de intentos de almacenamiento en búfer, el tiempo que se tardó en obtener el primer byte del primer fragmento de vídeo, el tiempo que se tardó en procesar el primer fotograma, la longitud almacenada actualmente en búfer y el tiempo de búfer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> Métricas de carga de reproducción</a></span> </td> 
   <td colname="2"> Proporciona información sobre cuánto tiempo tardaron los medios en cargarse, cuánto tardó el reproductor en procesar el primer fotograma o, en caso de error, en fallar. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackMetrics.html" format="html" scope="external"> Métricas de reproducción</a></span> </td> 
   <td colname="2"> Proporciona información sobre el comportamiento de la reproducción. Esto incluye la velocidad de fotogramas, la velocidad de bits, la longitud del búfer, etc. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackSessionMetrics.html" format="html" scope="external"> MétricasSesiónReproducción</a></span> </td> 
   <td colname="2"> Proporciona información sobre cuántos segundos el reproductor ha invertido durante la reproducción real y cuánto tiempo ha invertido el vídeo en pantalla. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/QOSProvider.html" format="html" scope="external"> QOSProvider</a></span> </td> 
   <td colname="2">
    <pre>
      Proporciona métricas esenciales de QoS para la reproducción y el dispositivo.
    </pre>
    <pre>
      clase de proveedor de información QOS.
    </pre> </td> 
  </tr> 
 </tbody> 
</table>
