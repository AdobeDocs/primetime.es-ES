---
description: El sistema de notificación TVSDK genera varios avisos de error, advertencia e información que proporcionan metadatos de diagnóstico.
title: Códigos de notificación
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# Información general {#notification-codes-overview}

El sistema de notificación TVSDK genera varios avisos de error, advertencia e información que proporcionan metadatos de diagnóstico.

Los objetos de notificación proporcionan información relacionada con el estado del reproductor. TVSDK proporciona una lista ordenada cronológicamente de objetos de notificación, y cada notificación contiene los siguientes metadatos:

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
   <td colname="2"> El tipo de notificación. Según la plataforma, esta propiedad hace referencia a un tipo enumerado con posibles valores INFO, WARN o ERROR. Es la agrupación de nivel superior para las notificaciones. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> code </td> 
   <td colname="2">La representación numérica asignada a la notificación: 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">Eventos de notificación de errores, de 10000 a 19999 </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">Eventos de notificación de advertencia, de 20000 a 299999 </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">Eventos de notificación de información, de 30000 a 399999 </li> 
    </ul> <p>Cada rango de nivel superior, como los errores, se divide en subintervalos, como 101000 a 101999, que representan errores de reproducción. </p>
    <pre>
     La enumeración 
     <span class="codeph"> mediacore.PSDKErrorCode</span> enumera los valores posibles.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> name </td> 
   <td colname="2">Cadena que contiene una descripción del código legible en lenguaje natural, como <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> metadata </td> 
   <td colname="2">Pares clave/valor que contienen información relevante adicional sobre la notificación. Por ejemplo, una clave llamada <span class="codeph"> URL</span> estaría emparejada con un valor que es una URL relacionada con la notificación, como una URL no válida que provocó un error. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> innerNotification </td> 
   <td colname="2">Una referencia a otro objeto <span class="codeph"> MediaPlayerNotification</span> que afectó directamente a esta notificación. Un ejemplo podría ser una notificación sobre un error de inserción de publicidad que corresponda directamente a un conflicto de inserción de línea temporal. No todas las notificaciones proporcionan una notificación interna. </td> 
  </tr> 
 </tbody> 
</table>

