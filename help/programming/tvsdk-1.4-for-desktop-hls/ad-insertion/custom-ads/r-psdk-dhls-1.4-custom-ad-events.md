---
description: El reproductor de TVSDK distribuye eventos para mostrar el estado de carga de la publicidad personalizada o para ignorar una publicidad que tarda demasiado en cargarse o que tiene errores. Estos eventos se definen en events.CustomAdEvents.
seo-description: El reproductor de TVSDK distribuye eventos para mostrar el estado de carga de la publicidad personalizada o para ignorar una publicidad que tarda demasiado en cargarse o que tiene errores. Estos eventos se definen en events.CustomAdEvents.
seo-title: Eventos de publicidad personalizados
title: Eventos de publicidad personalizados
uuid: 78e2ccf4-5943-4c60-84be-623182d9a300
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Eventos de publicidad personalizados{#custom-ad-events}

El reproductor de TVSDK distribuye eventos para mostrar el estado de carga de la publicidad personalizada o para ignorar una publicidad que tarda demasiado en cargarse o que tiene errores. Estos eventos se definen en events.CustomAdEvents.

<table id="table_718700E0F0B042F882ED131F79E01D4E"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Evento </th> 
   <th colname="col2" class="entry"> Definición </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdClickThru </span> </td> 
   <td colname="col2"> El número de veces que el visor hizo clic en una publicidad personalizada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdError </span> </td> 
   <td colname="col2"> Se produjo un error con la publicidad personalizada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoaded </span> </td> 
   <td colname="col2"> Se cargó la publicidad personalizada.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoading </span> </td> 
   <td colname="col2"> Se está cargando la publicidad personalizada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPaused </span> </td> 
   <td colname="col2"> La publicidad personalizada se ha pausado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdResumed </span> </td> 
   <td colname="col2"> La publicidad personalizada ha seguido reproduciéndose después de una pausa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> Reproducción de publicidad </span> </td> 
   <td colname="col2"> Se está reproduciendo la publicidad personalizada. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdProgress </span> </td> 
   <td colname="col2"> <p>El reproductor de publicidad personalizado notifica al reproductor de TVSDK el progreso de la publicidad personalizada. &amp;nbsp; </p> <p>Con este evento se pasan el <span class="codeph"> tiempo </span> actual y el <span class="codeph"> tiempo total </span> de la publicidad. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStarted </td> 
   <td colname="col2"> La publicidad personalizada ha comenzado a reproducirse y se muestra al visor.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStopped </td> 
   <td colname="col2"> La publicidad personalizada ha terminado de reproducirse. </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->

