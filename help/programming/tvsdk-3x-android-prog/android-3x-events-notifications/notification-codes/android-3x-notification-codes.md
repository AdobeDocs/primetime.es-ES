---
description: El sistema de notificaciones TVSDK genera varios avisos de error, advertencia y de información que proporcionan metadatos de diagnóstico.
seo-description: El sistema de notificaciones TVSDK genera varios avisos de error, advertencia y de información que proporcionan metadatos de diagnóstico.
seo-title: Códigos de notificación
title: Códigos de notificación
uuid: 6babb203-b6d4-4b11-9fae-41e7db7fd570
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Códigos de notificación {#notification-codes}

El sistema de notificaciones TVSDK genera varios avisos de error, advertencia y de información que proporcionan metadatos de diagnóstico.

Los objetos de notificación proporcionan información relacionada con el estado del reproductor. TVSDK proporciona una lista ordenada cronológicamente de objetos de notificación. Cada notificación contiene los metadatos siguientes:

<table frame="all" colsep="1" rowsep="1" id="table_1A32EFFE1834438D8261886EC9D7250D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b> Elemento</b></th> 
   <th colname="2" class="entry"><b> Descripción</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2"> <p>El tipo de notificación. </p> <p>Según la plataforma, esta propiedad es un tipo enumerado con los valores posibles de INFO, WARN y ERROR. Es la agrupación de nivel superior para las notificaciones. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> code</span> </td> 
   <td colname="2"> <p>Las siguientes representaciones numéricas se asignan a las notificaciones: 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">Eventos de notificación de errores, de 100000 a 19999 </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">Eventos de notificación de advertencia, de 20000 a 29999 </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">Eventos de notificación de información, de 300000 a 399999 </li> 
     </ul> </p> <p>Cada rango de nivel superior, como errores, se divide en subintervalos, como 101000 a 101999, que representan errores de reproducción. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">Una cadena que contiene una descripción legible en lenguaje natural del evento de notificación, como <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> metadatos</span> </td> 
   <td colname="2"> <p>Par clave/valor que contienen información relevante adicional sobre la notificación. </p> <p>Por ejemplo, una clave llamada <span class="codeph"> URL</span> proporcionaría un valor que es una dirección URL relacionada con la notificación, como una dirección URL no válida que produjo un error. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>Referencia a otro objeto <span class="codeph"> MediaPlayerNotification</span> que afectó directamente a esta notificación. </p> <p>Un ejemplo puede ser una notificación sobre un error de inserción de publicidad que corresponde directamente a un conflicto de inserción de línea temporal. No todas las notificaciones proporcionan una notificación interna. </p> </td> 
  </tr> 
 </tbody> 
</table>