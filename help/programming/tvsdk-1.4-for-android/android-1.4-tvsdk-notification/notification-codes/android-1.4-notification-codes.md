---
description: El sistema de notificaciones TVSDK genera varios avisos de error, advertencia y de información que proporcionan metadatos de diagnóstico.
seo-description: El sistema de notificaciones TVSDK genera varios avisos de error, advertencia y de información que proporcionan metadatos de diagnóstico.
seo-title: Códigos de notificación
title: Códigos de notificación
uuid: edbce737-28fd-4309-be5a-2e33fcc156b6
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Códigos de notificación{#notification-codes}

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
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2">El tipo de notificación. Según la plataforma, esta propiedad hace referencia a un tipo enumerado con posibles valores de <span class="codeph"> INFO</span>, <span class="codeph"> WARN</span>o <span class="codeph"> ERROR</span>. Es la agrupación de nivel superior para las notificaciones. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> code</span> </td> 
   <td colname="2">Representación numérica asignada a la notificación: 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">Eventos de notificación de errores, de 100000 a 19999 </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">Eventos de notificación de advertencia, de 20000 a 29999 </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">Eventos de notificación de información, de 300000 a 399999 </li> 
    </ul> <p>Cada rango de nivel superior, como errores, se divide en subintervalos, como 101000 a 101999, que representan errores de reproducción. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">Una cadena que contiene una descripción del código legible en lenguaje natural, como <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> metadatos</span> </td> 
   <td colname="2">Par clave/valor que contienen información relevante adicional sobre la notificación. Por ejemplo, una clave llamada <span class="codeph"> URL</span> se emparejaría con un valor que es una dirección URL relacionada con la notificación, como una dirección URL no válida que generara un error. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2">Referencia a otro objeto <span class="codeph"> MediaPlayerNotification</span> que afectó directamente a esta notificación. Un ejemplo puede ser una notificación sobre un error de inserción de publicidad que corresponde directamente a un conflicto de inserción de línea temporal. No todas las notificaciones proporcionan una notificación interna. </td> 
  </tr> 
 </tbody> 
</table>

