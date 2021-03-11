---
description: El reproductor TVSDK envía eventos para mostrar el estado de carga de la publicidad personalizada o para ignorar una publicidad que está tardando demasiado en cargarse o que tiene errores. Estos eventos se definen en events.CustomAdEvents.
title: Eventos de publicidad personalizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---


# Eventos de publicidad personalizados{#custom-ad-events}

El reproductor TVSDK envía eventos para mostrar el estado de carga de la publicidad personalizada o para ignorar una publicidad que está tardando demasiado en cargarse o que tiene errores. Estos eventos se definen en events.CustomAdEvents.

<table id="table_718700E0F0B042F882ED131F79E01D4E"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Evento </th> 
   <th colname="col2" class="entry"> Definición </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdClickThru  </span> </td> 
   <td colname="col2"> El número de veces que el visor hizo clic en un anuncio personalizado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdError  </span> </td> 
   <td colname="col2"> Error con el anuncio personalizado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoaded  </span> </td> 
   <td colname="col2"> Se ha cargado el anuncio personalizado.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> Carga de publicidad  </span> </td> 
   <td colname="col2"> Se está cargando el anuncio personalizado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPaused  </span> </td> 
   <td colname="col2"> La publicidad personalizada se ha pausado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdResumed  </span> </td> 
   <td colname="col2"> El anuncio personalizado ha seguido reproduciéndose después de una pausa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> Reproducción de publicidad  </span> </td> 
   <td colname="col2"> Se está reproduciendo el anuncio personalizado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdProgress  </span> </td> 
   <td colname="col2"> <p>El reproductor de publicidad personalizado notifica al reproductor TVSDK sobre el progreso del anuncio personalizado. &amp;nbsp; </p> <p>El <span class="codeph"> currentTime </span> y <span class="codeph"> totalTime </span> del anuncio se pasan con este evento. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStarted </td> 
   <td colname="col2"> El anuncio personalizado ha empezado a reproducirse y se muestra al espectador.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStopped </td> 
   <td colname="col2"> El anuncio personalizado ha terminado de reproducirse. </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->

