---
description: Estas clases proporcionan información que le ayuda a determinar el rendimiento del reproductor.
title: Clases de QoS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# Clases de QoS {#qos-classes}

Estas clases proporcionan información que le ayuda a determinar el rendimiento del reproductor.

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>Nombre</b></th> 
   <th colname="2" class="entry"><b>Descripción</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTDeviceInformation.html" format="html" scope="external"> PTDeviceInformation</a> </td> 
   <td colname="2">Proporciona información sobre la plataforma y el sistema operativo en los que se ejecuta TVSDK: 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">Versión del sistema operativo de la plataforma </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">Número de versión de la biblioteca TVSDK </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">Nombre del modelo del dispositivo </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">Nombre del fabricante del dispositivo </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">UUID del dispositivo </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">Anchura y altura de la pantalla del dispositivo </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTPlaybackInformation.html" format="html" scope="external"> PTPlaybackInformation</a> </td> 
   <td colname="2"> Proporciona información sobre el rendimiento de la reproducción. Esto incluye la velocidad de fotogramas, la velocidad de bits del perfil, el tiempo total empleado en el almacenamiento en búfer, el número de intentos de almacenamiento en búfer, el tiempo que se tardó en obtener el primer byte del primer fragmento de vídeo, el tiempo que se tardó en procesar el primer fotograma, la longitud en búfer y el tiempo de búfer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTQoSProvider.html" format="html" scope="external"> PTQoSProvider</a> </td> 
   <td colname="2">
    <pre>
      Proporciona métricas de QoS esenciales para la reproducción y el dispositivo.
    </pre>
    <pre>
      Clase del proveedor de información QOS.
    </pre> </td> 
  </tr> 
 </tbody> 
</table>