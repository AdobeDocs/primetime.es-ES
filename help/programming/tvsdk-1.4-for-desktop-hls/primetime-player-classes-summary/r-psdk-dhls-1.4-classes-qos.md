---
description: Estas clases proporcionan información que le ayuda a determinar el rendimiento del reproductor.
seo-description: Estas clases proporcionan información que le ayuda a determinar el rendimiento del reproductor.
seo-title: Clases QoS
title: Clases QoS
uuid: c1192474-d183-4995-87ef-839699844b48
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---


# Clases QoS {#qos-classes}

Estas clases proporcionan información que le ayuda a determinar el rendimiento del reproductor.

Paquete: [paquete com.adobe.mediacore.qos](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/package-detail.html) : [com.adobe.mediacore.qos.metrics](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/package-detail.html)

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
   <td colname="2"> Proporciona información sobre cuánto tiempo pasó el reproductor durante el almacenamiento en búfer y la frecuencia con que se produjo un evento de almacenamiento en búfer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/DeviceInformation.html" format="html" scope="external"> DeviceInformation</a></span> </td> 
   <td colname="2">Proporciona información sobre la plataforma y el sistema operativo en los que se ejecuta TVSDK: 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">Versión del SO de la plataforma </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">Número de versión de la biblioteca TVSDK </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">Nombre del modelo del dispositivo </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">Nombre del fabricante del dispositivo </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">UUID de dispositivo </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">Anchura y altura de la pantalla del dispositivo </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/LoadInformation.html" format="html" scope="external"> LoadInformation</a></span> </td> 
   <td colname="2"> Contiene información de QoS sobre la carga de varios recursos (archivos, manifiesto o lista de reproducción, fragmentos/segmentos, pistas, etc.). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/LoadInformationType.html" format="html" scope="external"> LoadInformationType</a></span> </td> 
   <td colname="2"> Clase de lista desglosada que lista los valores posibles para la propiedad type de los objetos LoadInformation. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/PlaybackInformation.html" format="html" scope="external"> PlaybackInformation</a></span> </td> 
   <td colname="2"> Proporciona información sobre el rendimiento de la reproducción. Esto incluye la velocidad de fotogramas, la velocidad de bits de perfil, el tiempo total empleado en el almacenamiento en búfer, el número de intentos de almacenamiento en búfer, el tiempo que tardó en obtenerse el primer byte del primer fragmento de vídeo, el tiempo que tardó en procesarse el primer fotograma, la longitud almacenada en el búfer actualmente y el tiempo de búfer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackLoadMetrics</a></span> </td> 
   <td colname="2"> Proporciona información sobre cuánto tiempo tardó en cargarse el medio, cuánto tardó el reproductor en procesar el primer fotograma o, en caso de error, en fallar. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackMetrics.html" format="html" scope="external"> PlaybackMetrics</a></span> </td> 
   <td colname="2"> Proporciona información sobre el comportamiento de la reproducción. Esto incluye la velocidad de fotogramas, la velocidad de bits, la longitud del búfer, etc. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackSessionMetrics.html" format="html" scope="external"> PlaybackSessionMetrics</a></span> </td> 
   <td colname="2"> Proporciona información sobre cuántos segundos pasó el reproductor durante la reproducción y cuánto tiempo estuvo realmente en pantalla el vídeo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/QOSProvider.html" format="html" scope="external"> QOSProvider</a></span> </td> 
   <td colname="2">
    <pre>
      Proporciona métricas de QoS esenciales tanto para la reproducción como para el dispositivo.
    </pre>
    <pre>
      Clase de proveedor de información QOS.
    </pre> </td> 
  </tr> 
 </tbody> 
</table>

