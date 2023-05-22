---
description: El sistema de notificación de TVSDK produce varios avisos de error, advertencia e información que proporcionan metadatos de diagnóstico.
title: Códigos de notificación
exl-id: 615de4e4-fb42-4159-b572-da7866df4ce3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Códigos de notificación{#notification-codes}

El sistema de notificación de TVSDK produce varios avisos de error, advertencia e información que proporcionan metadatos de diagnóstico.

Los objetos de notificación proporcionan información relacionada con el estado del reproductor. TVSDK proporciona una lista ordenada cronológicamente de objetos de notificación y cada notificación contiene los siguientes metadatos:

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
   <td colname="2">El tipo de notificación. Según la plataforma, esta propiedad hace referencia a un tipo enumerado con posibles valores de <span class="codeph"> INFORMACIÓN</span>, <span class="codeph"> ADVERTIR</span>, o <span class="codeph"> ERROR</span>. Esta es la agrupación de nivel superior para notificaciones. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> código</span> </td> 
   <td colname="2">La representación numérica asignada a la notificación: 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">Eventos de notificación de error, de 100000 a 199999 </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">Eventos de notificación de advertencia, de 200000 a 299999 </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">Eventos de notificación de información, de 300000 a 399999 </li> 
    </ul> <p>Cada rango de nivel superior, como los errores, se divide en subrangos, como los 101000, a través de 101999 que representan errores de reproducción. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">Una cadena que contiene una descripción del código legible en lenguaje natural, como <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> metadatos</span> </td> 
   <td colname="2">Pares de clave/valor que contienen información relevante adicional acerca de la notificación. Por ejemplo, una clave denominada <span class="codeph"> URL</span> estaría emparejado con un valor que es una URL relacionada con la notificación, como una URL no válida que provocó un error. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2">Una referencia a otra <span class="codeph"> MediaPlayerNotification</span> objeto que afectó directamente a esta notificación. Un ejemplo podría ser una notificación sobre un error de inserción de publicidad que corresponde directamente a un conflicto de inserción de cronología. No todas las notificaciones proporcionan una notificación interna. </td> 
  </tr> 
 </tbody> 
</table>
