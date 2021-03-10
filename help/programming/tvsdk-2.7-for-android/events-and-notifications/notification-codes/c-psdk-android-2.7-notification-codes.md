---
description: El sistema de notificación TVSDK genera varios avisos de error, advertencia e información que proporcionan metadatos de diagnóstico.
title: Códigos de notificación
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Información general {#notification-codes-overview}

El sistema de notificación TVSDK genera varios avisos de error, advertencia e información que proporcionan metadatos de diagnóstico.

Los objetos de notificación proporcionan información relacionada con el estado del reproductor. TVSDK proporciona una lista ordenada cronológicamente de objetos de notificación. Cada notificación contiene los siguientes metadatos:

<table frame="all" colsep="1" rowsep="1" id="table_1A32EFFE1834438D8261886EC9D7250D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Elemento </th> 
   <th colname="2" class="entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2"> <p>El tipo de notificación. </p> <p>En función de la plataforma, esta propiedad es un tipo enumerado con posibles valores de INFO, WARN y ERROR. Es la agrupación de nivel superior para las notificaciones. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> code</span> </td> 
   <td colname="2"> <p>Las siguientes representaciones numéricas se asignan a las notificaciones: 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">Eventos de notificación de errores, de 10000 a 19999 </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">Eventos de notificación de advertencia, de 20000 a 299999 </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">Eventos de notificación de información, de 30000 a 399999 </li> 
     </ul> </p> <p>Cada rango de nivel superior, como los errores, se divide en subintervalos, como 101000 a 101999, que representan errores de reproducción. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">Cadena que contiene una descripción legible en lenguaje natural del evento de notificación, como <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> metadata</span> </td> 
   <td colname="2"> <p>Pares clave/valor que contienen información relevante adicional sobre la notificación. </p> <p>Por ejemplo, una clave llamada <span class="codeph"> URL</span> proporcionaría un valor que es una dirección URL relacionada con la notificación, como una dirección URL no válida que provocó un error. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>Una referencia a otro objeto <span class="codeph"> MediaPlayerNotification</span> que afectó directamente a esta notificación. </p> <p>Un ejemplo podría ser una notificación sobre un error de inserción de publicidad que corresponda directamente a un conflicto de inserción de línea temporal. No todas las notificaciones proporcionan una notificación interna. </p> </td> 
  </tr> 
 </tbody> 
</table>

