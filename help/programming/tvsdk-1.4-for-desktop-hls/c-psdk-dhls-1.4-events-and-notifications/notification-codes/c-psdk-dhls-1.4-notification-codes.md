---
description: El sistema de notificaciones TVSDK genera varios avisos de error, advertencia y de información que proporcionan metadatos de diagnóstico.
seo-description: El sistema de notificaciones TVSDK genera varios avisos de error, advertencia y de información que proporcionan metadatos de diagnóstico.
seo-title: Códigos de notificación
title: Códigos de notificación
uuid: a7b77a5c-9873-45cf-8499-aa00270a7ad6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Información general {#notification-codes-overview}

El sistema de notificaciones TVSDK genera varios avisos de error, advertencia y de información que proporcionan metadatos de diagnóstico.

Los objetos de notificación proporcionan información relacionada con el estado del reproductor. TVSDK proporciona una lista ordenada cronológicamente de objetos de notificación y cada notificación contiene los metadatos siguientes:

<table frame="all" colsep="1" rowsep="1" id="table_DBA8CACF02DB4AF2B053E560850B49CE"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Elemento </th> 
   <th colname="2" class="entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> type </td> 
   <td colname="2"> El tipo de notificación. Según la plataforma, esta propiedad hace referencia a un tipo enumerado con posibles valores de INFO, WARN o ERROR. Es la agrupación de nivel superior para las notificaciones. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> code </td> 
   <td colname="2">Representación numérica asignada a la notificación: 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">Eventos de notificación de errores, de 100000 a 19999 </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">Eventos de notificación de advertencia, de 20000 a 29999 </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">Eventos de notificación de información, de 300000 a 399999 </li> 
    </ul> <p>Cada rango de nivel superior, como errores, se divide en subintervalos, como 101000 a 101999, que representan errores de reproducción. </p>
    <ph>
     La enumeración <span class="codeph"> mediacore.PSDKErrorCode</span> enumera los valores posibles.
    </ph> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> name </td> 
   <td colname="2">Una cadena que contiene una descripción del código legible en lenguaje natural, como <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> metadatos </td> 
   <td colname="2">Par clave/valor que contienen información relevante adicional sobre la notificación. Por ejemplo, una clave llamada <span class="codeph"> URL</span> se emparejaría con un valor que es una dirección URL relacionada con la notificación, como una dirección URL no válida que generara un error. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> innerNotification </td> 
   <td colname="2">Referencia a otro objeto <span class="codeph"> MediaPlayerNotification</span> que afectó directamente a esta notificación. Un ejemplo puede ser una notificación sobre un error de inserción de publicidad que corresponde directamente a un conflicto de inserción de línea temporal. No todas las notificaciones proporcionan una notificación interna. </td> 
  </tr> 
 </tbody> 
</table>

