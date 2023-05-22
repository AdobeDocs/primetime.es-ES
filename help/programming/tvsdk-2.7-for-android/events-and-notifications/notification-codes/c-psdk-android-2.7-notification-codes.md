---
description: El sistema de notificación de TVSDK produce varios avisos de error, advertencia e información que proporcionan metadatos de diagnóstico.
title: Códigos de notificación
exl-id: 7bf016c6-8651-413b-a478-ac2d24f9453c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Información general {#notification-codes-overview}

El sistema de notificación de TVSDK produce varios avisos de error, advertencia e información que proporcionan metadatos de diagnóstico.

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
   <td colname="2"> <p>El tipo de notificación. </p> <p>Según la plataforma, esta propiedad es un tipo enumerado con posibles valores de INFO, WARN y ERROR. Esta es la agrupación de nivel superior para notificaciones. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> código</span> </td> 
   <td colname="2"> <p>Se asignan las siguientes representaciones numéricas a las notificaciones: 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">Eventos de notificación de error, de 100000 a 199999 </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">Eventos de notificación de advertencia, de 200000 a 299999 </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">Eventos de notificación de información, de 300000 a 399999 </li> 
     </ul> </p> <p>Cada rango de nivel superior, como los errores, se divide en subrangos, como los 101000, a través de 101999 que representan errores de reproducción. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">Una cadena que contiene una descripción legible en lenguaje natural del evento de notificación, como <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> metadatos</span> </td> 
   <td colname="2"> <p>Pares de clave/valor que contienen información relevante adicional acerca de la notificación. </p> <p>Por ejemplo, una clave denominada <span class="codeph"> URL</span> proporcionaría un valor que es una dirección URL relacionada con la notificación, como una dirección URL no válida que provocó un error. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>Una referencia a otra <span class="codeph"> MediaPlayerNotification</span> que afectó directamente a esta notificación. </p> <p>Un ejemplo podría ser una notificación sobre un error de inserción de publicidad que corresponde directamente a un conflicto de inserción de cronología. No todas las notificaciones proporcionan una notificación interna. </p> </td> 
  </tr> 
 </tbody> 
</table>
